# Claude Code Routines

> Platform layer for TTAI's autonomous employees. Replaced Cowork scheduled tasks in April 2026.
> Last updated: 2026-04-16

## What This Is

Claude Code Routines run on Anthropic's cloud infrastructure. They replace the previous Cowork scheduled tasks that required Computer Use and a local machine. Each routine is a prompt that runs on a schedule or responds to API triggers.

## Trigger Types

| Type | Use Case | How It Works |
|------|----------|--------------|
| **Schedule** | Daily/periodic operational loop | Cron-like. Wiki runs every other day. Fred and Mark-Lite run daily. |
| **API** | Follow-up replies, ad-hoc queries | POST to /fire endpoint with `text` field. Used by [[ttai-slack-bridge]] to route Andy's Slack replies. |
| **GitHub Events** | CI/CD, PR activity | Not currently used by employees. Available for future use. |

## Architecture

```
Anthropic Cloud (Routine runtime)
  ↓
Claude Code (model + tools)
  ↓
Connectors (Slack, Gmail, Google Drive, GitHub)
  ↓
Repos (employee memory -- wiki, autostrategy, mark-lite)
```

## Dual-Mode Prompt Pattern

Every employee prompt checks whether the API trigger passed a `text` field:

- **No text (scheduled run):** Full operational loop -- gather info, do work, report to Slack
- **Text present (follow-up):** Parse the message, respond to the specific request, post response to Slack

Same prompt handles both modes. This is the universal pattern for all TTAI employees.

## Key Constraints

- **Ephemeral sessions:** Each run starts fresh with no memory of previous runs. Persistent state must live in connected repos or trackers.
- **Daily run cap:** Account-level limit on routine executions per day.
- **Connector access:** Tools available depend on which MCP servers are configured (Slack, Gmail, Google Drive, Google Sheets, GitHub).
- **Branch assignment:** Each run gets a unique branch name. If multiple runs trigger in the same window, they create parallel branches that can't see each other's work.

## Migration from Cowork

| Aspect | Cowork (old) | Routines (new) |
|--------|-------------|----------------|
| Runtime | Andy's laptop | Anthropic cloud |
| Data access | Computer Use (browser) | Connectors (API-based) |
| Reporting | Email | Slack #ttai-employees |
| Speed | 15-30 min | 5-15 min |
| Reliability | Fragile (browser timeouts) | Robust (structured tool calls) |
| Two-way comms | One-way (email) | Two-way (Slack -> bridge -> API) |

## Current Employee Status

| Employee | Platform | Status |
|----------|----------|--------|
| **Wiki** | Routines | Live since 2026-04-15 |
| **Mark-Lite** | Routines | Live since 2026-04-16 |
| **Fred** | Cowork | Migration pending. Last reported 2026-04-13. |

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Routes Slack replies to routine API endpoints
- [[cowork-pipeline]] -- Predecessor system (being phased out)
- [[connectors-beat-computer-use]] -- Principle driving this migration

## Sources

- Wiki ingest: "Wiki Agent Migrated to Routines + Slack Bridge Deployed" (2026-04-15)
- Mark-Lite Slack reports (2026-04-16)
