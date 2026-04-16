# TTAI Slack Bridge

> Node.js Slack Bolt app that routes Andy's Slack replies to the correct employee routine API endpoint. Deployed on Railway free tier.
> Last updated: 2026-04-16

## What It Does

The bridge listens for Andy's messages in #ttai-employees and fires the correct employee's Claude Code Routine API endpoint with the message as the `text` field. This enables two-way interaction: employees post reports to Slack, Andy replies in Slack, the bridge routes the reply back to the employee.

## Architecture

```
Andy replies in #ttai-employees
  ↓
Slack Bolt app (Socket Mode -- no public URL required)
  ↓
Identifies target employee (by name prefix or thread context)
  ↓
POST to correct routine's /fire endpoint with message as text field
  ↓
Employee routine runs in follow-up mode, responds in Slack
```

## Deployment

- **Platform:** Railway (free tier)
- **Runtime:** Node.js
- **Connection:** Slack Socket Mode (no public URL, no ngrok)
- **Repo:** Separate GitHub repo (not the wiki repo). Auto-deploys on push.
- **Env vars:** Slack tokens + per-employee routine API endpoints and tokens

## Adding a New Employee

1. Deploy the employee's Claude Code Routine with API trigger enabled
2. Add the routine's API endpoint URL and token to the bridge's env vars on Railway
3. Update the bridge's routing logic to recognise the employee's name prefix
4. Redeploy (auto on push)

## Current Routing

| Employee | Name Prefix | Status |
|----------|-------------|--------|
| Wiki | "wiki" or "Wiki" | Live (2026-04-15) |
| Fred | "fred" or "Fred" | Pending migration |
| Mark-Lite | "mark-lite" or "Mark-Lite" | Pending migration |

## Dependencies

- Slack workspace: Think Through AI
- Channel: #ttai-employees (C0AT4K9KJFQ, public)
- Railway account (free tier)
- Claude Code Routines API endpoints for each employee

## Known Constraints

- Slack connector requires **public** channels for discovery. Private channels not reachable on initial setup.
- Socket Mode means no webhook URL -- the app maintains a persistent WebSocket connection from Railway.
- Railway free tier has sleep/wake cycles -- first message after idle may have slight latency.

## Links

- [[employee-framework]] -- Universal employee model
- [[wiki-agent-SKILL]] -- First employee routed through this bridge
- [[claude-code-routines]] -- Platform the bridge connects to
- [[connectors-beat-computer-use]] -- Principle: connectors over browser automation

## Sources

- Wiki Agent migration session (2026-04-15)
- Wiki ingest file: "Wiki Agent Migrated to Routines + Slack Bridge Deployed"
