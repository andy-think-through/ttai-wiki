# TTAI Slack Bridge

> Node.js Slack Bolt app that routes Andy's Slack replies in #ttai-employees to the correct employee routine's API endpoint. Deployed on Railway free tier.
> Last updated: 2026-04-16

## What It Does

The bridge listens for messages in #ttai-employees and routes them to the correct autonomous employee's Claude Code Routine via API trigger:

```
Andy posts in #ttai-employees
  → Bridge detects target employee (name prefix or thread context)
  → Bridge fires /fire endpoint for that employee's routine
  → Routine runs in follow-up mode (text field = Andy's message)
  → Employee responds in Slack
```

## Architecture

- **Framework:** Node.js + Slack Bolt SDK
- **Connection:** Socket Mode (no public URL required)
- **Hosting:** Railway free tier, auto-deploys from GitHub on push
- **Repository:** Separate GitHub repo (not the wiki repo)

## Configuration

Each employee needs:
- A routine API endpoint URL
- An API token for the `/fire` endpoint
- These are stored as environment variables in Railway

### Current Employees Routed

| Employee | Routing | Status |
|----------|---------|--------|
| **Wiki** | Name prefix "Wiki" or "wiki" in message, or thread reply to Wiki's post | Active |
| **Fred** | Not yet configured | Pending migration to Routines |
| **Mark-Lite** | Not yet configured | Pending migration to Routines |

## Deployment

- Push to the bridge's GitHub repo triggers auto-deploy on Railway
- Socket Mode means no webhook URL to configure -- the app connects outbound to Slack's servers
- Railway free tier is sufficient for current message volume

## Adding a New Employee

1. Create the employee's Claude Code Routine (schedule + API triggers)
2. Add the routine's API endpoint URL and token as Railway env vars
3. Add routing logic to the bridge code (name detection + thread context)
4. Deploy (auto on push)
5. Test with a direct message in #ttai-employees

## Known Constraints

- Railway free tier has usage limits (sufficient for current volume)
- Slack connector requires public channels for MCP tool discovery
- Bridge only monitors #ttai-employees -- no other channels

## Links

- [[wiki-agent-SKILL]] -- Wiki employee (active, routed)
- [[fred-autostrategy-employee-SKILL]] -- Fred employee (pending migration)
- [[employee-framework]] -- Universal employee model
- [[claude-code-routines]] -- Platform documentation

## Sources

- Wiki Agent migration conversation (2026-04-15)
- Ingest file: 2026-04-16-wiki-agent-migration-routines-slack-bridge.md
