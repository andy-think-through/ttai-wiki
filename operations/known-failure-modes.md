# Known Failure Modes
> Common failures in AutoStrategy operations and mitigations.
> Last updated: 2026-04-08

## Failure Modes by Category

### 1. Computer Use Timeouts (CRITICAL)

**Symptom:** Scheduled skill runs at 8am and Computer Use call never returns; bets are not placed; no error logged.

**Root Cause:** Computer Use requires user approval at the browser. When no one is at the keyboard, the call times out after 30s.

**Applies To:**
- [[cowork-pipeline]] bet placement (currently using Computer Use)
- Any scheduled task that uses Computer Use on the critical path

**Mitigation:**
- ✅ Keep Betfair browser pre-logged-in
- ✅ Use screenshot-based odds fetching (passive, not interactive)
- ✅ Never automate bet placement; only automate data fetch and briefing generation
- ✅ **LONG-TERM:** Integrate Betfair API (eliminate Computer Use entirely)

---

### 2. Cowork Sandbox Network Blocks (MODERATE)

**Symptom:** Script in Cowork skill fails with connection timeout to `googleapis.com`.

**Root Cause:** Cowork sandbox applies network filtering; certain domains are blocked for security.

**Affected Services:**
- Google Sheets API (`googleapis.com`)
- Google Docs API (`docs.google.com`)

**Applies To:**
- Crypto monitoring via Google Sheets update
- Any step that directly calls Google APIs from Cowork

**Mitigation:**
- ✅ Move Google API calls to Desktop Commander Python scripts (sandbox allows googleapis.com)
- ✅ Use `.gsheet` shortcut files that are exported to local .xlsx (read via openpyxl)
- ✅ Call Google Sheets API from Claude Code environment (sandbox allows it there)

---

### 3. Google Sheets as Shortcut Files (MODERATE)

**Symptom:** Python script tries to `open()` a `.gsheet` file; returns "Not a real file" or IO error.

**Root Cause:** `.gsheet` files are pointers to Google Drive; they're not real files on the local filesystem.

**Applies To:**
- Betting tracker if stored as `.gsheet` shortcut
- Crypto monitoring data if in Google Sheets

**Mitigation:**
- ✅ Export the Google Sheet to `.xlsx` and store both (shortcut for browsing, .xlsx for scripts)
- ✅ Use Google Sheets API (not local file read) to access the sheet directly
- ✅ Sync .xlsx periodically (e.g., nightly) via Python script

---

### 4. Computer Use Not Suitable for Automated Scheduled Tasks (CRITICAL)

**Symptom:** 8am scheduled skill uses Computer Use to log into Betfair and place bets. It fails silently because no one is at the keyboard.

**Root Cause:** Computer Use is interactive; it requires user approval for sensitive actions (window focus, form filling).

**Applies To:**
- Any [[scheduled-tasks]] that use Computer Use on the critical path
- Automation that runs when user is not present

**Mitigation:**
- ✅ Architecture all scheduled tasks to be zero-touch (see [[scheduled-tasks-need-zero-intervention]])
- ✅ Move interactive steps to manual or browser-based (Chrome MCP, pre-logged-in session)
- ✅ For Betfair: either keep browser logged in + screenshot odds, or use Betfair API

---

### 5. Browser Account Confusion (MODERATE)

**Symptom:** Desktop Commander tries to log into Google and gets the wrong account; or Betfair login uses stale session from different account.

**Root Cause:** Multiple Google accounts in browser history; Betfair session cookies from a previous user.

**Applies To:**
- Any script that relies on pre-logged-in browser session
- Google API calls that need specific account authorization

**Mitigation:**
- ✅ Before running scripts, explicitly log out of irrelevant accounts
- ✅ Use Chrome MCP to explicitly log into the correct account
- ✅ Store account identifier in script config (so you can verify it's the right one)

---

### 6. Path Differences Across Contexts (MODERATE)

**Symptom:** Script works on Mac but fails in sandbox; local path `/Users/andyallen/...` doesn't exist in sandbox environment.

**Root Cause:** Different OSes, different mount points for cloud drives, different sandboxed root directories.

**Applies To:**
- Any hard-coded file paths
- Google Drive access (`/Volumes/My Drive/` on Mac vs cloud API in sandbox)

**Mitigation:**
- ✅ Use absolute paths consistently; test in both Mac and sandbox
- ✅ Document both paths: `/Users/andyallen/.../file.xlsx` (Mac) and `/home/claude/.../file.xlsx` (sandbox)
- ✅ Use environment variables or config files for paths that change per context

---

### 7. Stale Data During Live Events (MODERATE)

**Symptom:** Screenshot-based odds are 5–10s stale during NBA/Tennis live matches; market has moved by the time bet is placed.

**Root Cause:** Time lag between screenshot capture and bet placement; fast market movement during live events.

**Applies To:**
- Live NBA betting
- Live Tennis in-play betting
- Any live sport with volatile odds

**Mitigation:**
- ✅ Re-capture odds immediately before placement (not 5min earlier)
- ✅ Accept small slippage (< 0.05 on decimal odds); don't abandon bets for minor movement
- ✅ For critical bets: Andy manually checks current odds on Betfair before confirming
- ✅ **LONG-TERM:** Use Betfair API for real-time odds (no latency)

---

### 8. Tennis Data Requires Manual Collation (MODERATE)

**Symptom:** Model runs but has no matchup context (seeding, H2H history); predictions are generic.

**Root Cause:** ATP public APIs don't expose all tournament matchup data; must be manually collected from ATP website.

**Applies To:**
- [[tennis-atp]] model input pipeline
- Pre-match predictions

**Mitigation:**
- ✅ Build ATP scraper (parse ATP website for seeding, H2H data)
- ✅ Subscribe to a tennis data provider (e.g., Tennis Explorer, Flashscore API)
- ✅ For now: manually collate daily and feed to model as JSON

---

### 9. Model Drift & Stale Predictions (MODERATE)

**Symptom:** ROI drops from +8% to -2% mid-season; model was trained on preseason data and doesn't adapt to mid-season reality.

**Root Cause:** Predictive models degrade when distribution shift occurs (e.g., teams acquire new players, injury patterns change, coaching staff changes).

**Applies To:**
- [[nba]] season progression
- [[tennis-atp]] clay → grass transition
- Any multi-month sport

**Mitigation:**
- ✅ Retrain models weekly or bi-weekly
- ✅ Monitor ROI per week; alert if drops > 2 percentage points
- ✅ Keep versioned model artifacts (v1, v2, v3) and compare
- ✅ Use holdout validation set to detect when model has drifted

---

### 10. Feature Leakage in Model Training (CRITICAL)

**Symptom:** Model reports +72% ROI in backtest but collapses to -6.5% in live trading.

**Root Cause:** Features calculated from full dataset (including future data). Model is cheating; it's not actually predictive.

**Applies To:**
- Any new sport model
- [[horse-racing]] (historically vulnerable)
- Feature engineering that uses aggregate statistics

**Mitigation:**
- ✅ Implement forward-only feature calculation (only use data available at prediction time)
- ✅ Use paper-trading audits to validate backtests before live betting
- ✅ Separate train/validation/test sets; never touch holdout set during training
- ✅ Document data cutoff times for all features

---

### 11. Majority-Class Coasting (MODERATE)

**Symptom:** Model claims 90% accuracy on tennis but predicts 0 upsets in 50 prediction opportunities (when upsets happen 10% of the time).

**Root Cause:** Model learns to always predict the favorite (majority class) because it maximizes accuracy.

**Applies To:**
- [[tennis-atp]] upset detection
- [[nba]] come-from-behind betting
- Any imbalanced classification

**Mitigation:**
- ✅ Enforce minority-class metrics (recall, precision, F1 on minority)
- ✅ Use weighted loss functions that penalize minority-class misses
- ✅ Check: does model make any upset predictions? If not, it's coasting
- ✅ Use [[results-diagnostic]] to decompose performance by outcome class

---

### 12. Betfair Availability & API Limits (LOW)

**Symptom:** Betfair site goes down; screenshots fail; API calls return 429 (rate limit).

**Root Cause:** Betfair maintenance windows; high request volume; IP blocks.

**Applies To:**
- [[cowork-pipeline]] odds fetching
- Scheduled model execution

**Mitigation:**
- ✅ Implement retry logic with exponential backoff
- ✅ Cache odds locally; use stale odds if real-time fetch fails
- ✅ Monitor Betfair status page
- ✅ Space out API calls to stay below rate limits

---

## Quick Checklist Before Running Scheduled Tasks

- [ ] Betfair browser is logged in and unlocked
- [ ] Google account (if needed) is logged in on correct account
- [ ] All file paths are absolute and exist
- [ ] Model artifacts are in Claude Code environment
- [ ] Betting tracker spreadsheet is accessible
- [ ] No Computer Use calls on critical path (use Chrome MCP or APIs instead)
- [ ] Test the full pipeline manually once before scheduling
- [ ] Log failures visibly (write to file, don't fail silently)

## Links
- [[cowork-pipeline]]
- [[tool-routing]]
- [[scheduled-tasks-need-zero-intervention]]
- [[data-leakage-silent-killer]]
- [[majority-class-trap]]

## Sources
- raw/autostrategy/daily-skill-lessons-learned.md
- raw/autostrategy/autostrategy_STATUS.md
