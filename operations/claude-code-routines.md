# Claude Code Routines

> Platform for TTAI's autonomous AI employees. Runs on Anthropic cloud infrastructure. Supports schedule, API, and GitHub event triggers.
> Last updated: 2026-04-16

## What It Is

Claude Code Routines is the execution platform that replaced Cowork scheduled tasks for TTAI's autonomous employees. Each employee is a Routine with a prompt (the SKILL file), connected tools (MCP servers), and one or more triggers.

## Trigger Types

| Type | Use | Example |
|------|-----|---------|
| **Schedule** | Recurring cadence (daily, every other day) | Wiki runs every other day; Fred runs daily |
| **API** | On-demand via HTTP POST to `/fire` endpoint | Slack bridge sends Andy's replies |
| **GitHub events** | Repo activity (push, PR, issue) | Not currently used by employees |

Employees use **schedule + API** triggers. Schedule handles the daily operational loop; API handles follow-up interactions from Andy via [[ttai-slack-bridge]].

## Key Properties

- **Ephemeral sessions:** Each run starts fresh with no memory of prior runs. All persistent state must live in connected repos, trackers, or external tools. See [[repos-are-employee-memory]].
- **Connector-first:** Information gathering via MCP connectors (Slack, Google Drive, Gmail, GitHub) rather than Computer Use. See [[connectors-beat-computer-use]].
- **Daily run cap:** Account-level limit on total runs per day. Relevant when multiple employees share an account.
- **Cloud execution:** Runs on Anthropic infrastructure. No dependency on Andy's local machine.

## Dual-Mode Prompt Pattern

All employee prompts follow the same structure:

1. Check whether the API trigger passed a `text` field with input
2. If no text: **Scheduled Run** -- execute the full operational loop
3. If text present: **Follow-Up** -- respond to the specific message, do targeted work

This pattern is universal across all employees. See [[employee-framework]].

## Current Employee Status

| Employee | Platform | Schedule | API |
|----------|----------|----------|-----|
| Wiki | Routines | Every other day | Live (via Slack bridge) |
| Mark-Lite | Routines | Daily | Live (via Slack bridge) |
| Fred | Cowork (pending migration) | Daily | Not yet |

## Migration from Cowork

See [[cowork-pipeline]] for the phase-out status. Key differences:

| Aspect | Cowork | Routines |
|--------|--------|----------|
| Execution | Andy's machine (Cowork orchestrator) | Anthropic cloud |
| Information | Computer Use (Min browser) | MCP connectors |
| Interaction | One-way (email reports) | Two-way (Slack + API trigger) |
| State | Local filesystem | GitHub repos + Google Sheets |
| Cost | Computer Use tokens (expensive) | Connector calls (cheap) |

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Routes Slack replies to Routine API endpoints
- [[wiki-agent-SKILL]] -- Wiki employee (first migrated)
- [[cowork-pipeline]] -- Previous platform (being phased out)
- [[connectors-beat-computer-use]] -- Principle from migration
- [[repos-are-employee-memory]] -- Principle from migration

## Sources

- Andy's Slack ingest message (2026-04-16): "Wiki Agent Migrated to Routines + Slack Bridge Deployed"
