# Browser Agent Architecture

> Practical how-to: setting up, running, and optimizing visual browser agents for SaaS automation. Viewport constraints, cost controls, and known gotchas.
> Last updated: 2026-04-08

## Quick Start

### Prerequisites

```bash
export ANTHROPIC_API_KEY=sk-...
```

### Launch Agent

```bash
cd /Users/andyallen/Documents/Claude-Code/browser-agent/
npm run workflow -- --workflow hike-keyword-audit
# Or single task:
npm run task -- --task "Read this page and extract all keyword assignments"
```

### First Run: Manual Login

```bash
npm run workflow -- --workflow hike-keyword-audit --wait-for-login
# Browser opens. Manually authenticate in Hike.
# Once logged in, press Enter in terminal.
# Session is now persistent in ~/.browser-agent/chromium-profile/
```

Subsequent runs use cached cookies/session automatically.

## The Core Agent Loop

**Location:** `src/anthropic/loop.ts`

The agent runs this cycle repeatedly until completion or bail-out:

```
1. Capture screenshot (1280×800 default)
   └─ Downscale to 832×520 (0.65x) for Claude
   └─ Save full-res to disk
   └─ Hash screenshot, compare to previous 3

2. Send to Claude (via computer_20251124 tool)
   └─ System prompt + task description
   └─ Screenshot as tool input
   └─ Full message history (compressed, keeping last 3 screenshots)

3. Claude responds with action
   └─ left_click at (x, y)
   └─ type text
   └─ key (including F6, Ctrl+L, Ctrl+W)
   └─ scroll up/down/left/right
   └─ take screenshot

4. Execute action via Playwright
   └─ Click at exact viewport coordinates
   └─ Type text into focused element
   └─ Press key combination
   └─ Scroll element into view

5. Capture new screenshot
   └─ Return as tool_result
   └─ Repeat from step 1
```

**Iteration tracking:** Counter increments on each cycle. Run terminates when limit reached.

**Message compression:** After 5+ screenshots, older ones are replaced with text summaries (`"Screenshot N (hash): [description]"`). Keeps context window reasonable while preserving enough history for Claude to reason about page changes.

## The Viewport Constraint (Critical)

The tool definition tells Claude: **"This screen is 1280×800 pixels."** Claude reasons in those exact coordinates. The Playwright browser MUST have the same viewport, or clicks land in wrong places.

### Testing Viewport Alignment

```bash
# Check active viewport in ~/.browser-agent/chromium-profile/ (Playwright sets it)
# Take a screenshot from the agent loop
# Verify: screenshot dimensions = 1280×800
# If misaligned: clicks will be off by a consistent factor
```

### Why 1280×800?

- Standard breakpoint for web apps (neither too wide nor too mobile)
- Leaves room for browser UI chrome without hitting edge cases
- Matches Anthropic's tool definition spec

### Coordinate Mapping in Downscaling

When screenshot is downscaled to 832×520 (0.65x), Claude automatically maps coordinates back to 1280×800 space. **You don't need to convert.** If Claude sees a button at (600, 300) in the downscaled image, it sends `left_click` at (600, 300) in 1280×800 space, and Playwright executes correctly.

This is not magic — Claude understands the zoom factor from the image dimensions and reasons accordingly.

## Cost Controls (Load-Bearing)

These are not optional. Without them, a confused iteration can cost hundreds of dollars or navigate to attacker-controlled domains.

### Cost Ceiling

**Default:** $2.00 per run

**Location:** `src/config/index.ts` → `maxCostPerRunUsd`

**How it works:**
- Token count tracked on every API response
- Cost estimated: `(inputTokens × $0.003 + outputTokens × $0.015) / 1000`
- Running total accumulated
- If total exceeds ceiling, run terminates with status code `cost_ceiling`

**Override per workflow:**
```typescript
// In workflow config
export const config = {
  maxCostPerRunUsd: 5.00  // Raise for complex execution phases
}
```

### Why Token Counting?

Screenshots are the dominant cost. Typical run:
- 60–70% of input tokens = screenshot data
- 25–30% = task prompt + message history
- 5–10% = tool responses (action results)

A 25-iteration run at 0.65x scale: ~15,000–20,000 input tokens. At $0.003 per 1k tokens = $0.045–$0.060 per run, plus output tokens (typically $0.20–$0.30 for longer runs).

## Bail-Out Conditions

Run terminates and logs status code when any condition is hit:

| Condition | Code | Threshold | Recovery |
|-----------|------|-----------|----------|
| Max iterations | `max_iterations` | 25 (default) | Increment counter in phase config |
| Timeout | `timeout` | 5 min (default) | Re-run picks up where it left off if state persisted |
| Stuck loop | `stuck_loop` | 3 identical actions | Usually indicates page element is unfindable; check coordinates |
| Stuck screenshot | `stuck_screenshot` | 3 unchanged screenshots | Page isn't responding; may need longer wait or different approach |
| Domain blocked | `domain_blocked` | URL not in allowlist | Add domain to workflow config's `allowedDomains` |
| Cost ceiling | `cost_ceiling` | $2.00 default | Raise `maxCostPerRunUsd` or reduce screenshots |
| Error | `error` | Any exception | Check logs in `runs/<run-id>/run.json` |

### Stuck Detection Deep Dive

**Stuck-loop (coordinate duplicate detection):**
- Tracks last 3 actions
- If Claude clicks at (640, 300) three times in a row, flag as `stuck_loop`
- Common cause: button is unclickable or coordinates are wrong

**Stuck-screenshot (visual hash detection):**
- Computes perceptual hash of each screenshot
- If 3 consecutive screenshots have identical hash (within tolerance), flag as `stuck_screenshot`
- Common cause: page hasn't loaded, element isn't responding, or loading spinner is permanent

**Recovery approach:** When either detector fires, review the run artifacts:
- `runs/<run-id>/screenshots/` — see what the agent was looking at
- `runs/<run-id>/actions.jsonl` — trace the final actions before termination
- `runs/<run-id>/run.json` — full structured log with error message

## Phase Lifecycle

Each phase is a separate agent run with its own orchestration:

### Phase Configuration

```typescript
// In workflow phase file (e.g., phase1-research.ts)
export const phase1Task = {
  task: `[Task description for agent]`,
  config: {
    screenshotScale: 0.65,           // Default; raise to 1.0 for precision clicking
    temperature: 0.5,
    maxIterations: 25,               // For research; raise to 50 for execution
    maxCostPerRunUsd: 2.00,          // For research; raise to $5 for execution
    stuckScreenshotThreshold: 3,     // For normal phases; raise to 6 for slow-loading
    allowedDomains: [
      'my.hike.marketing',
      'hike.marketing',
      'customer-site-here.com'
    ]
  }
}
```

### Phase State Persistence

After each run, `runs/<workflow-name>.state.json` is updated with:
- Completed phases
- Extracted data (titles, keywords, page assignments)
- Next phase to run
- Errors and retry counts

**Auto-resume:** If Phase 2 hits iteration limit and extracts data from pages 1–3 of 9, next run automatically resumes from page 4. No manual state editing required.

## The F6 Shortcut (Token Saver)

**F6 extracts all page text via `page.innerText('body')`** instead of taking a screenshot.

**Cost:** ~100–500 tokens (vs ~650–1,000 for a screenshot).

### When to Use F6

- Reading data-heavy pages (keyword lists, search results, data tables)
- Extracting text content that doesn't require visual interaction
- Avoiding unnecessary screenshots in research phases

### When NOT to Use F6

- Clicking buttons or filling forms (you need the visual to locate elements)
- Cross-domain pages (some may not populate correctly with innerText)
- Dynamic content that requires reading rendered positions

### Example Task

```
You are auditing a customer's blog posts in Hike. 
You've already navigated to https://my.hike.marketing/content/topic/create.

STEP 1: Press F6 to extract all visible blog titles and post count.
(Do NOT take a screenshot here — F6 is much cheaper.)

STEP 2: Read the extracted text and identify the blog post with the most internal links.

STEP 3: [Then click/interact if needed — now use screenshots]
```

## Domain Allowlist (Security Boundary)

**Location:** `src/session/browser.ts`

Page content is untrusted input. Without an allowlist, prompt injection on a malicious website could redirect the agent to attacker-controlled domains.

### Adding a Domain

```typescript
// In workflow phase config
allowedDomains: [
  'my.hike.marketing',
  'onsiteoptimizer.com',    // New domain added
  'customer-website.com'
]
```

Navigation to unlisted domains terminates the run with status `domain_blocked`.

### Cross-Domain Gotcha: Evolution MX

Evolution MX (accounting software) has a **cross-domain redirect + cookie authentication** that caused Chrome extension timeouts. Playwright doesn't have the same sandbox constraints, so the Playwright-based browser agent handles this fine. But be aware: some tools may not work across domain boundaries.

## Browser Session Management

### Profile Location

```
~/.browser-agent/chromium-profile/
├── Default/
│   ├── Cookies      ← Persisted between runs
│   ├── Cache/       ← Page caches
│   └── ...
├── SingletonLock    ← Lock file (can cause startup failures)
└── ...
```

### Cleaning Up Lock Files

If browser fails to start (usually "Already another Chromium running"):

```bash
rm -f ~/.browser-agent/chromium-profile/SingletonLock
pkill -f chromium 2>/dev/null
npm run workflow -- --workflow hike-keyword-audit
```

### Session Persistence

Cookies and localStorage are automatically preserved. Subsequent runs reuse the authenticated session. **This is intentional and safe** — the agent only navigates to domains in the workflow's allowlist.

To force re-authentication:

```bash
# Either:
# 1. Delete cookies manually in ~/.browser-agent/chromium-profile/
# 2. Or add --wait-for-login flag to next run
npm run workflow -- --workflow hike-keyword-audit --wait-for-login
```

## Run Artifacts

Every run produces structured outputs in `runs/<run-id>/`:

### Files

```
runs/<run-id>/
├── meta.json              Run metadata (model, task, config, start time)
├── state.json             Live state snapshot (updated every iteration)
├── run.json               Full structured log (written at end)
├── actions.jsonl          One JSON line per action (click, type, key, screenshot)
├── requests.jsonl         One JSON line per API request
├── responses.jsonl        One JSON line per response (includes cost, tokens)
└── screenshots/
    ├── step-000-*.png              Full-resolution screenshot
    ├── step-000-*-scaled.png       Downscaled (sent to Claude)
    └── step-000-*.json             Metadata (hash, dimensions, scale)
```

### Analyzing Failures

To investigate why a run failed:

```bash
# 1. Check status code and final error
jq '.status, .error' runs/<run-id>/meta.json

# 2. Review last actions
jq -s '.[-5:]' runs/<run-id>/actions.jsonl

# 3. View final screenshot
open "runs/<run-id>/screenshots/step-$(ls runs/<run-id>/screenshots/*.png | wc -l)*.png"

# 4. Check message history
jq '.messages[-3:]' runs/<run-id>/run.json
```

## Environment Variables

### Required

```bash
export ANTHROPIC_API_KEY=sk-...
```

### Optional Overrides

```bash
export SCREENSHOT_SCALE=1.0        # Full resolution (tokens cost more)
export HEADLESS=true               # Run Chromium headless (can't watch agent)
export MAX_COST_USD=5.00           # Override cost ceiling
export DEBUG=true                  # Verbose logging
```

## Navigation Best Practices

### Rule 1: No Dropdown Menus

**Always navigate directly via URL. Never use dropdowns.**

```javascript
// ❌ WRONG (will fail intermittently)
// "Click Strategy, then click Keyword Research"

// ✅ RIGHT (reliable)
key "ctrl+l"
type "https://my.hike.marketing/keywords/ideas"
key "Return"
```

Dropdowns fail because:
- Hover states required
- Menu can close before click lands
- Pixel-based agent can't predict timing

### Rule 2: Hardcode Known URLs

```typescript
// In workflow phase config
const HIKE_URLS = {
  DASHBOARD: 'https://my.hike.marketing/dash',
  KEYWORD_IDEAS: 'https://my.hike.marketing/keywords/ideas',
  KEYWORD_TRACKER: 'https://my.hike.marketing/keywords',
  KEYWORD_SCAN: 'https://my.hike.marketing/keyword-scan',
  SITEMAP: 'https://my.hike.marketing/sitemap',
  ONSITE_OPTIMIZER: 'https://my.hike.marketing/onsite-optimizer',
  CONTENT_SCRAPBOARD: 'https://my.hike.marketing/content/topic/create',
  ACTIONS: 'https://my.hike.marketing/actions'
}
```

Update this table as new URLs are discovered. Every phase prompt must use these, not menu navigation.

### Rule 3: Hardcode Stable Coordinates

If testing confirms that a button is always at the same position (e.g., SEO Settings modal title field at (640, 266)), embed those coordinates in the prompt or config.

**Cost of hardcoding:** One initial screenshot to verify, then zero screenshots for that element forever.

**Cost of dynamic discovery:** Every phase takes a screenshot to find the button.

## Prompt Engineering for Visual Agents

### Prescriptive > Goal-Oriented

```
❌ "Navigate to the keyword research page"
✅ "Press Ctrl+L, type https://my.hike.marketing/keywords/ideas, press Enter"
```

The agent needs explicit action sequences, not abstract goals.

### Constraint Instructions

```
"Do NOT take a screenshot at this step — proceed directly to the next action."
"Do NOT scroll down to find the button — it is always at pixel coordinates (640, 594)."
"Do NOT use the navigation menu — it is unreliable. Use the direct URL instead."
```

Explicit prohibitions save significant tokens.

### Front-Load Known Data

If Phase 1 already extracted titles and keyword assignments:

```
"Phase 1 identified these page titles: [list]
 Phase 1 assigned these keywords: [list]
 
 Your task (Phase 2): [new task using this data]
 
 Do NOT re-extract titles or re-read the sitemap — use the data above."
```

### Coordinate Embeds

```
"The SEO Settings modal has these stable coordinates (confirmed via testing):
 - Title field: (640, 266)
 - Meta description field: (640, 590)
 - Save button: (640, 594)
 
 Click these coordinates directly. Do NOT take a screenshot to find the button."
```

## Cost Optimization Checklist

- [ ] Are you taking screenshots when F6 would suffice?
- [ ] Are you navigating via menus instead of direct URLs?
- [ ] Are you discovering coordinates dynamically instead of hardcoding them?
- [ ] Are you extracting the same data twice in different phases?
- [ ] Can you move this to a direct API call instead of the browser?

Each "yes" is a cost reduction opportunity.

## Known Gotchas

### Loading Spinner Loops
Some pages show loading spinners that never fully disappear. Stuck-screenshot detection will flag this. **Fix:** Raise `stuckScreenshotThreshold` to 6 or higher for slow-loading pages.

### Cross-Domain Authentication
Evolution MX uses cookie-based auth via redirect. **Fix for Playwright:** Works fine (no sandbox constraints). For Chrome extension tools: may timeout — use human discovery instead.

### Modal Z-Index Issues
Some modals overlap incorrectly or don't render fully. **Fix:** Scroll within the modal, or re-check if modal is actually clickable at the coordinates.

### Floating Elements That Move on Scroll
Some sticky headers or floating toolbars move when you scroll. Hard-coded coordinates may no longer be valid. **Fix:** Test coordinates empirically before hardcoding. Verify they don't change on scroll.

### Tab Management (Ctrl+T, Ctrl+W)
The agent can open and close tabs, but avoid it unless necessary. **Gotcha:** If you close the wrong tab, the browser doesn't error — it just switches tabs silently. Coordinates may no longer match.

### Paste Operations (Clipboard)
Some apps restrict clipboard access. Playwright can type directly, which is more reliable. **Avoid:** `key "cmd+v"` if you can just `type` instead.

## Further Reading

- [[agent-browser]] — Product overview and use cases
- [[autoresearch]] — Parameter optimization methodology
- [[autostrategy]] — Strategy optimization framework
- `src/config/index.ts` — All tunable parameters
- `src/workflows/hike-keyword-audit/` — Complete working example
- `docs/prompts/` — Step-by-step task definitions
