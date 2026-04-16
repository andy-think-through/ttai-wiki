# TTAI Slack Bridge

> Node.js Slack Bolt app that routes Andy's Slack replies to the correct employee routine API endpoint.
> Last updated: 2026-04-16

## What It Does

The bridge listens for Andy's messages in #ttai-employees. When Andy replies, it identifies the target employee (by name prefix or thread context) and fires the correct routine's `/fire` endpoint with the message as the `text` field. This enables two-way interaction: employees post reports, Andy replies, the bridge triggers a follow-up run, and the employee responds in Slack.

## Architecture

```
Andy posts in #ttai-employees
  ↓
Slack Bridge (Socket Mode listener)
  ↓ identifies target employee
Claude Code Routine API /fire endpoint
  ↓ text = Andy's message
Employee runs in follow-up mode
  ↓
Response posted back to #ttai-employees
```

## Technical Details

- **Framework:** Node.js Slack Bolt (Socket Mode -- no public URL required)
- **Hosting:** Railway free tier, auto-deploys from GitHub on push
- **Repo:** Separate GitHub repo (not the wiki repo)
- **Config:** Employee API endpoints and tokens stored as Railway env vars

## Adding a New Employee

When migrating Fred or Mark-Lite to Routines:
1. Create the routine and note the API endpoint + token
2. Add the endpoint and token to the bridge's Railway env vars
3. Update the bridge's routing logic to recognise the new employee name
4. Test with a direct message in #ttai-employees

## Dependencies

- Slack workspace: Think Through AI
- Channel: #ttai-employees (C0AT4K9KJFQ, public)
- Railway account (free tier)
- Claude Code Routine API endpoints for each employee

## Links

- [[wiki-agent-SKILL]] -- First employee using this bridge
- [[employee-framework]] -- Universal employee model
- [[claude-code-routines]] -- Platform the bridge connects to
- [[connectors-beat-computer-use]] -- Principle: structured APIs over visual automation

## Sources

- Wiki Agent migration session (2026-04-15)
