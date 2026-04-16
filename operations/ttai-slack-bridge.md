# TTAI Slack Bridge

> Node.js Slack Bolt app on Railway free tier. Routes Andy's Slack replies in #ttai-employees to the correct employee routine API endpoint.
> Last updated: 2026-04-16

## What It Does

The bridge closes the two-way loop between Andy and autonomous employees:

1. Employee posts report to #ttai-employees (via Slack connector)
2. Andy replies in Slack (thread or channel message)
3. Bridge detects the reply, identifies target employee (by name prefix or thread context)
4. Bridge fires the correct Routine's `/fire` endpoint with the message as `text` field
5. Employee runs in follow-up mode, processes the message, responds in Slack

## Architecture

```
Andy types in Slack
    |
TTAI Slack Bridge (Railway)
    |
    v
Identifies target employee
    |
    v
POST /fire to Routine API endpoint
(text = Andy's message)
    |
    v
Employee Routine runs in follow-up mode
    |
    v
Posts response back to #ttai-employees
```

## Technical Details

- **Runtime:** Node.js + Slack Bolt SDK
- **Connection:** Socket Mode (no public URL required)
- **Hosting:** Railway free tier (auto-deploys from GitHub on push)
- **Repo:** Separate GitHub repo (not the wiki repo)
- **Config:** Employee name prefixes + Routine API endpoints + tokens in env vars

## Employee Routing

| Prefix / Thread | Target | API Endpoint |
|----------------|--------|-------------|
| "Wiki" or thread reply to Wiki message | Wiki Agent | Wiki routine `/fire` |
| "Fred" or thread reply to Fred message | Fred (AutoStrategy) | Fred routine `/fire` (pending migration) |
| "Mark-Lite" or thread reply to Mark-Lite message | Mark-Lite | Mark-Lite routine `/fire` (pending migration) |

## Deployment

- Push to the bridge GitHub repo triggers automatic Railway deployment
- To add a new employee: add their name prefix, API endpoint URL, and token to Railway env vars
- No code changes needed for new employees -- just config

## Links

- [[employee-framework]] -- Universal employee operating model
- [[wiki-agent-SKILL]] -- First employee to use the bridge
- [[claude-code-routines]] -- Platform the bridge connects to

## Sources

- Andy's Slack ingest message (2026-04-16): "Wiki Agent Migrated to Routines + Slack Bridge Deployed"
