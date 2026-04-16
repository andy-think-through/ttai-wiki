# Claude Code Routines

> Platform for running TTAI's autonomous employees. Replaced Cowork scheduled tasks as of 2026-04-15.
> Last updated: 2026-04-16

## What It Is

Claude Code Routines run on Anthropic's cloud infrastructure. They provide three trigger types:

1. **Schedule** -- cron-style triggers (daily, every other day, etc.)
2. **API** -- HTTP endpoint that accepts a `text` field (enables follow-up mode)
3. **GitHub events** -- triggered by repo activity (not currently used by TTAI employees)

TTAI employees use schedule + API triggers. The dual-mode prompt pattern checks whether `text` is present to determine scheduled run vs follow-up.

## Key Properties

- **Ephemeral sessions:** Each run starts fresh with no conversation memory. Persistent state must live in connected repos, trackers, or Slack history.
- **Connectors:** Slack, Google Drive, Gmail, Google Sheets (varies by employee). These replace Computer Use for data access.
- **Daily run cap:** Account-level limit applies. Plan around it when running multiple employees.
- **Branch assignment:** Each run gets a branch name. For personal repos, pushing to main directly avoids orphaned work.

## TTAI Employee Migration Status

| Employee | Previous | Current | Status |
|----------|----------|---------|--------|
| Wiki | Cowork + Computer Use | Routines + Slack/Drive connectors | Migrated (2026-04-15) |
| Mark-Lite | Cowork + Computer Use | Routines + Slack/Gmail/Drive connectors | Migrated (2026-04-16) |
| Fred | Cowork + Computer Use | Pending | Paused; migration priority (NBA playoffs live) |

## Architectural Pattern

```
Routine (scheduled or API-triggered)
  -> Reads state from repo + Slack + connectors
  -> Does work (updates files, reads data, generates analysis)
  -> Commits changes to repo
  -> Posts report to Slack #ttai-employees
  -> (If API-triggered) responds to Andy's specific question
```

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Bridge routing Slack replies to Routine endpoints
- [[cowork-pipeline]] -- Previous platform (being phased out)
- [[connectors-beat-computer-use]] -- Why connectors won
- [[repos-are-employee-memory]] -- Why repos matter

## Sources

- Wiki migration session (2026-04-15)
