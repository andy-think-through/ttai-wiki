# TTAI Slack Bridge

> Node.js Slack Bolt app that routes Andy's Slack replies to the correct employee routine API endpoint. Deployed on Railway.
> Last updated: 2026-04-16

## What It Does

The bridge listens for Andy's messages in #ttai-employees, identifies which employee is being addressed (by name prefix or thread context), and fires the correct Claude Code Routine's `/fire` endpoint with the message as the `text` field. This enables two-way interaction: employees post reports to Slack, Andy replies, the bridge triggers a follow-up run, and the employee responds in Slack.

## Architecture

```
Andy posts in #ttai-employees
  |
  v
Slack Bridge (Railway) listens via Socket Mode
  |
  v
Identifies target employee (name prefix or thread)
  |
  v
POST to employee's Routine /fire endpoint with text payload
  |
  v
Employee Routine runs in follow-up mode
  |
  v
Employee posts response to #ttai-employees
```

## Infrastructure

- **Platform:** Railway (free tier)
- **Runtime:** Node.js
- **Slack integration:** Slack Bolt SDK, Socket Mode (no public URL required)
- **Repo:** Separate GitHub repo (auto-deploys on push)
- **Channel:** #ttai-employees (C0AT4K9KJFQ, public)

## Configuration

Each employee needs:
- A Routine API endpoint URL
- A Routine API token
- These are stored as environment variables in the Railway deployment

### Current Employee Routing

| Employee | Status | Endpoint Configured |
|----------|--------|-------------------|
| Wiki | Live | Yes |
| Fred | Pending migration | No |
| Mark-Lite | Pending migration | No |

## Key Design Decisions

- **Socket Mode** -- No public URL needed. Simpler deployment, no webhook management.
- **Single channel** -- All employees share #ttai-employees. The bridge disambiguates by message content.
- **Auto-deploy** -- Push to GitHub triggers Railway redeploy. No manual deployment steps.

## Failure Modes

- **Railway free tier limits** -- May have cold starts or downtime. Slack messages sent during downtime won't trigger follow-ups. Andy can re-post or trigger the routine API directly.
- **Employee routing ambiguity** -- If Andy's message doesn't clearly target an employee, the bridge may route to the wrong one or fail to route. Use name prefix ("Wiki, ..." or "Fred, ...") for reliable routing.

## Links

- [[wiki-agent-SKILL]] -- Wiki employee (first migrated)
- [[fred-autostrategy-employee-SKILL]] -- Fred employee (pending migration)
- [[employee-framework]] -- Universal employee model
- [[claude-code-routines]] -- Platform documentation
- [[connectors-beat-computer-use]] -- Principle: connectors over browser automation

## Sources

- Wiki Agent migration session (2026-04-15)
- Wiki-ingest file: "Wiki Agent Migrated to Routines + Slack Bridge Deployed"
