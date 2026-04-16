# TTAI Slack Bridge

> Node.js Slack Bolt app routing Andy's Slack replies to the correct employee Routine API endpoint. Deployed on Railway free tier.
> Last updated: 2026-04-16

## What It Does

The bridge listens for Andy's messages in #ttai-employees and routes them to the correct autonomous employee's Routine API endpoint. This enables two-way interaction: employees post reports to Slack, Andy replies in Slack, the bridge fires the employee's follow-up mode.

## Architecture

```
Andy types in #ttai-employees
  -> Slack Bolt app (Socket Mode, Railway)
  -> Identifies target employee (name prefix or thread context)
  -> Fires /fire endpoint on correct Routine with message as `text` field
  -> Employee runs in follow-up mode
  -> Employee posts response back to #ttai-employees
```

## Technical Details

- **Framework:** Node.js Slack Bolt
- **Connection:** Socket Mode (no public URL required)
- **Hosting:** Railway free tier, auto-deploys from GitHub on push
- **Repo:** Separate GitHub repo (not the wiki repo)
- **Routing logic:** Name prefix matching (e.g., "Wiki," triggers Wiki routine; "Fred," triggers Fred routine) or thread-based context

## Environment Variables

- Slack Bot Token + App Token (Socket Mode)
- Routine API endpoints + tokens for each employee (Wiki, Fred, Mark-Lite)

## Current State

- Wiki: routed and working (2026-04-15)
- Mark-Lite: routed and working (2026-04-16)
- Fred: not yet connected (paused, migration pending)

## Links

- [[employee-framework]] -- Universal employee operating model
- [[wiki-agent-SKILL]] -- Wiki employee spec
- [[claude-code-routines]] -- Platform documentation

## Sources

- Wiki migration session (2026-04-15)
