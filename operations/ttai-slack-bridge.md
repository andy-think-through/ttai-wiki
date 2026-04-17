# TTAI Slack Bridge

> Node.js Slack Bolt app on Railway free tier. Routes Andy's Slack replies in #ttai-employees to the correct employee routine API endpoint.
> Last updated: 2026-04-16

## What It Does

The bridge listens for Andy's messages in #ttai-employees and fires the correct employee's Routine API endpoint with the message as the `text` field. This enables two-way interaction: employees post reports to Slack, Andy replies, the bridge triggers a follow-up run.

## Architecture

```
Andy posts in #ttai-employees
  → Slack event (message.channels)
  → Bridge identifies target employee (name prefix or thread context)
  → POST to Routine /fire endpoint with { text: "Andy's message" }
  → Employee runs in follow-up mode
  → Employee posts response to #ttai-employees
```

## Technical Details

- **Runtime:** Node.js Slack Bolt app
- **Hosting:** Railway free tier (auto-deploys from GitHub on push)
- **Connection:** Socket Mode (no public URL required)
- **Repo:** Separate GitHub repo from the wiki
- **Channel:** #ttai-employees (C0AT4K9KJFQ, public)

## Employee Routing

Each employee has an API endpoint and token configured in the bridge's environment variables. The bridge matches Andy's message to the correct employee by name prefix (e.g., "Wiki, ..." or "Fred, ...") or by thread context.

## Current Employees Connected

| Employee | Status |
|----------|--------|
| Wiki | Connected (2026-04-15) |
| Mark-Lite | Connected (2026-04-16) |
| Fred | Pending migration to Routines |

## Links

- [[employee-framework]] -- Universal employee operating model
- [[wiki-agent-SKILL]] -- Wiki's job spec
- [[claude-code-routines]] -- Platform documentation

## Sources

- Wiki Agent migration session (2026-04-15)
- Slack bridge deployment (2026-04-15)
