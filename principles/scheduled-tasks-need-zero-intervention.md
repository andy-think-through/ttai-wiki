# Scheduled Tasks Need Zero Intervention
> Scheduled skills must work at 8am with nobody at the keyboard.
> Last updated: 2026-04-08

## The Principle
Automated systems fail silently when they depend on human intervention or interactive approval. [[Computer Use]] calls timeout when the user is not present; browser auth requires user interaction. Scheduled [[cowork]] skills must be architected to never need real-time approval or presence.

## Where Discovered
AutoStrategy daily ops — scheduled skill attempted to use [[Computer Use]] to log into Betfair and place bets. When Andy was not at the keyboard at 8am, the Computer Use call timed out. The system crashed silently and bets were not placed.

## Reliability Ranking (Most to Least Reliable)
1. **Local files** — read/write .xlsx, .csv via openpyxl or pandas (always available)
2. **Desktop Commander scripts** — Python scripts that run in sandbox, no user approval needed
3. **Chrome MCP** — requires logged-in browser session but no per-action approval
4. **Computer Use** — requires user presence and per-action approval

## Where It Applies
- [[cowork]] daily betting ops — must use local files + API calls, never Computer Use for critical path
- Any scheduled [[scheduled-tasks]] — all external dependencies must be pre-authenticated
- [[autostrategy]] — result fetching, model training, briefing generation all need to be zero-touch

## How to Implement
- Store credentials in environment variables or secure vaults (not in code)
- Use APIs directly (Betfair API, Google Sheets API via Desktop Commander) instead of UI automation
- Test scheduled run without user at keyboard
- Build retry logic and error logging so failures are visible

## Exceptions
- One-off, manually-triggered skills (not scheduled) can use Computer Use and interactive approval
- Low-criticality tasks can tolerate occasional failures
- High-latency tasks (that run overnight and complete before business hours) have more flexibility

## Links
- [[cowork]]
- [[autostrategy]]
- [[Computer Use]]
- [[scheduled-tasks]]
- [[cowork-pipeline]]
- [[tool-routing]]

## Sources
- raw/autostrategy/daily-skill-lessons-learned.md
- raw/autostrategy/autostrategy_STATUS.md
