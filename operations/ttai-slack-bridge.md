# TTAI Slack Bridge

> Node.js Slack Bolt app on Railway. Routes Andy's Slack replies in #ttai-employees to the correct employee routine's API endpoint.
> Last updated: 2026-04-16

## What It Does

The bridge connects Slack (where Andy reads and replies) to Claude Code Routines (where employees run). When Andy posts a message in #ttai-employees, the bridge identifies which employee it's for and fires that employee's routine API endpoint with the message as the `text` field. This triggers a follow-up run in the employee's dual-mode prompt.

## Architecture

```
Andy posts in #ttai-employees
  |
  v
Slack Bridge (Node.js Bolt app, Socket Mode)
  |
  +--> Identifies target employee (name prefix or thread context)
  |
  +--> POST /fire to correct routine API endpoint
       with { "text": "Andy's message" }
  |
  v
Employee routine runs in follow-up mode
  |
  v
Employee posts response back to #ttai-employees
```

## Technical Details

| Property | Value |
|----------|-------|
| Framework | Slack Bolt (Node.js) |
| Connection | Socket Mode (no public URL required) |
| Hosting | Railway (free tier) |
| Deployment | Auto-deploys from GitHub on push |
| Repo | Separate GitHub repo (not the wiki repo) |

### Employee Routing

The bridge identifies the target employee by:
1. **Name prefix** -- Messages starting with "Wiki," "Fred," or "Mark-Lite" route to that employee
2. **Thread context** -- Replies in a thread started by an employee's report route back to that employee

### Environment Variables

Each employee needs two env vars in the bridge:
- `[EMPLOYEE]_ROUTINE_ID` -- The routine's ID for the /fire endpoint
- `[EMPLOYEE]_API_TOKEN` -- Authentication token for the routine API

### Current Employee Status

| Employee | Bridge Connected | Notes |
|----------|-----------------|-------|
| Wiki | Yes | Proven end-to-end 2026-04-15 |
| Fred | Not yet | Awaiting migration to Routines |
| Mark-Lite | Not yet | Awaiting migration to Routines |

## Slack Workspace

- **Workspace:** Think Through AI
- **Channel:** #ttai-employees (ID: C0AT4K9KJFQ, public)
- **Why public:** Slack MCP connector cannot discover private channels on initial setup. See [[known-failure-modes]].

## Dependencies

- Slack workspace with Bot token (xoxb) and App-level token (xapp)
- Railway account (free tier)
- Claude Code Routine API endpoints for each employee
- Employee routine API tokens

## Links

- [[employee-framework]] -- Universal employee operating model
- [[claude-code-routines]] -- Platform that employees run on
- [[wiki-agent-SKILL]] -- First employee connected via bridge
- [[fred-autostrategy-employee-SKILL]] -- Pending migration
- [[mark-lite-employee-SKILL]] -- Pending migration
- [[known-failure-modes]] -- Slack public channel gotcha documented here

## Sources

- Wiki Agent migration session (2026-04-15)
- inbox/2026-04-15-wiki-agent-migrated-slack-bridge-deployed.md
