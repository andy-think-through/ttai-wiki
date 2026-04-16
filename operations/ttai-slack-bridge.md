# TTAI Slack Bridge

> Node.js Slack Bolt app that routes Andy's Slack replies to the correct employee routine API endpoint. Deployed on Railway free tier.
> Last updated: 2026-04-16

## What This Is

The bridge closes the two-way communication loop between Andy and the autonomous employees. Employees post reports to Slack. Andy replies in Slack. The bridge detects the reply, identifies which employee it's for, and fires that employee's routine API endpoint with the message as input.

## Architecture

```
Andy replies in #ttai-employees
  ↓
Slack Bridge (Node.js, Socket Mode)
  ↓
Identifies target employee (name prefix or thread context)
  ↓
POST /fire to correct routine API endpoint (text = Andy's message)
  ↓
Employee routine runs in follow-up mode
  ↓
Employee posts response back to #ttai-employees
```

## Technical Details

- **Runtime:** Node.js Slack Bolt app
- **Connection:** Socket Mode (no public URL required)
- **Hosting:** Railway free tier, auto-deploys from GitHub on push
- **Repo:** Separate GitHub repo (not in the wiki repo)
- **Channel:** #ttai-employees (C0AT4K9KJFQ, public)

## Configuration

Environment variables per employee:
- `WIKI_ROUTINE_API_ENDPOINT` -- Wiki's /fire URL
- `WIKI_ROUTINE_API_TOKEN` -- Wiki's API auth token
- `MARKLITE_ROUTINE_API_ENDPOINT` -- Mark-Lite's /fire URL
- `MARKLITE_ROUTINE_API_TOKEN` -- Mark-Lite's API auth token
- `FRED_ROUTINE_API_ENDPOINT` -- (pending migration)
- `FRED_ROUTINE_API_TOKEN` -- (pending migration)

## Employee Routing

The bridge identifies the target employee by:
1. **Name prefix** -- Message starts with "WIKI", "MARK-LITE", "FRED"
2. **Thread context** -- Reply in a thread started by an employee

## Known Constraints

- Only routes messages from Andy (by user ID)
- Only listens in #ttai-employees
- Railway free tier has sleep/wake cycles -- first message after idle may have a delay

## Links

- [[claude-code-routines]] -- Platform these endpoints run on
- [[employee-framework]] -- Universal employee operating model
- [[connectors-beat-computer-use]] -- Design principle

## Sources

- Wiki ingest: "Wiki Agent Migrated to Routines + Slack Bridge Deployed" (2026-04-15)
