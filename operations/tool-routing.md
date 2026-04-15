# Tool Routing
> Which tool for which task in AutoStrategy operations.
> Last updated: 2026-04-08

## Quick Reference Table

| Task | Data Source | Primary Tool | Details |
|------|-------------|--------------|---------|
| Fetch Betfair odds | Betfair UI | **Computer Use** (screenshot) | Requires logged-in session; fallback: Min browser via Chrome MCP |
| Update betting tracker | Local .xlsx | **openpyxl** (Python, Desktop Commander) | Preserves formatting; most reliable for local storage |
| Run predictive models | Pre-trained artifacts | **Claude Code (Sonnet)** | Model execution; stored in Claude Code environment |
| Fetch NBA/Tennis/Snooker schedules | Public APIs / websites | **Claude Code** (HTTP client) or **Desktop Commander** (python requests) | Try public API first; fallback to web scraping |
| Generate briefing (markdown) | Model outputs + odds | **Cowork** skill | Orchestrates all steps; generates briefing document |
| Sync Google Sheets | Google Sheets | **Desktop Commander** (Python googleapiclient) | Sandbox BLOCKS direct API calls; use Python script wrapper |
| Monitor crypto | VPS state | **Google Sheets** (Telegram bot integration) | Updates Sheets via bot; visible on Andy's phone |
| Place bets manually | Betfair | **Browser** (Andy's hands) | Never automate; always manual confirmation |
| Log results after event | .xlsx tracker | **openpyxl** (Desktop Commander Python) | Update after bets close/settle |

## Tool Reliability by Category

### For Local File Operations
✅ **openpyxl** (Python via Desktop Commander) — reads/writes .xlsx, best for betting tracker  
✅ **pandas** (Python) — CSV/Excel analysis  
❌ **Google Sheets API** (direct) — Cowork sandbox blocks googleapis.com  
⚠️ **Google Sheets sync** — Use Desktop Commander Python script that calls API in sandbox

### For Browser/UI Interaction
✅ **Computer Use** — when Andy is at keyboard, for high-stakes manual steps  
✅ **Chrome MCP** (Min browser) — for reading public data, navigation, clicking (no auth approval needed once logged in)  
❌ **Computer Use** — for scheduled 8am tasks when user not present (TIMEOUT)  

### For Model Execution
✅ **Claude Code (Sonnet)** — runs numpy/pandas/sklearn models  
✅ **Desktop Commander** — Python script execution in sandbox  

### For API Calls
✅ **Claude Code** — simple HTTP calls, JSON parsing  
✅ **Desktop Commander** (Python) — complex API workflows, retry logic  
❌ **Cowork sandbox** — blocks outbound HTTPS to googleapis.com, docs.google.com  

### For Scheduled/Automated Tasks
✅ **Desktop Commander scripts** — zero-touch, sandbox-safe  
✅ **Claude Code background jobs** — model training, data fetching  
❌ **Computer Use** — requires user presence, times out  
❌ **Interactive approval** — can't work at 8am unattended  

## Known Restrictions & Workarounds

### Cowork Sandbox Network Restrictions
The Cowork sandbox blocks outbound HTTPS to:
- `googleapis.com` (Google APIs)
- `docs.google.com` (Google Docs)

**Workaround:** Use **Desktop Commander** to run Python scripts that call these APIs. The Desktop Commander sandbox allows googleapis.com calls.

### Google Sheets as Shortcut Files
.gsheet shortcut files point to Google Drive; they cannot be opened and read directly via local filesystem.

**Workaround:** 
1. Export Google Sheet to .xlsx locally
2. Read/write via openpyxl
3. Re-upload to Google Drive via Desktop Commander

Or: Use Google Sheets API via Desktop Commander Python script (not direct openpyxl).

### Computer Use Timeouts
Computer Use calls block until the user approves (or after 30s timeout if no approval). This fails for scheduled tasks.

**Workaround for scheduled tasks:** Pre-authenticate (keep browser logged in); use Chrome MCP or screenshots for odds fetching; never place bets automatically.

### Path Differences Across Contexts
- **Mac Desktop Commander:** `/Users/andyallen/...`
- **Google Drive Shortcuts:** `/Volumes/My Drive/...` (via Finder) or full Drive URL
- **Sandbox:** `/home/claude/...`

**Practice:** Always use absolute paths; note both Mac and sandbox paths when possible.

### Account Confusion Across Google Accounts
If Andy has multiple Google accounts, Google Sheets sync can get confused about which account to use.

**Workaround:** Explicitly authenticate with the correct account before running scripts; log out of irrelevant accounts.

## In-Play/Stale Data Handling

### Odds Staleness
Screenshot-based odds can be 5–10s stale during live events. Market moves quickly.

**Mitigation:**
- Take screenshots immediately before placement
- Manually confirm odds match what Andy sees
- Accept small slippage (< 0.05 in decimal odds)
- For large bets, use API-based real-time odds if available

### Result Timing
Sports results come in at different times:
- NBA: typically available within 30min of final buzzer
- Tennis: within 10min
- Snooker: within 5min

**Practice:** Fetch results with a 1-hour delay buffer; batch daily updates into evening or next-morning runs.

### Model Staleness
Predictive models can drift if trained on outdated data (e.g., season to date, preseason vs. mid-season).

**Mitigation:**
- Retrain models weekly or bi-weekly
- Monitor ROI per week; flag if ROI drops > 2 percentage points
- Keep model artifacts versioned

## Priority Ranking for New Tools
1. **Stable local files** (openpyxl, pandas) — use first if possible
2. **Public APIs** (ESPN, ATP, NBA stats) — prefer over scraping
3. **Browser automation** (Chrome MCP, Computer Use) — only for UI that has no API
4. **Betfair API** — should be prioritized if credentials obtained (solves all Computer Use problems)

## Links
- [[cowork-pipeline]]
- [[known-failure-modes]]
- [[scheduled-tasks-need-zero-intervention]]
- [[autostrategy]]

## Sources
- raw/autostrategy/daily-skill-lessons-learned.md
- raw/autostrategy/autostrategy_STATUS.md
