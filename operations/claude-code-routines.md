# Claude Code Routines

> Platform for TTAI's autonomous AI employees. Runs on Anthropic cloud infrastructure. Replaces Cowork scheduled tasks.
> Last updated: 2026-04-16

## What It Is

Claude Code Routines is the execution platform for TTAI's autonomous employees. Each employee is a Routine with a prompt, connected tools (Slack, Google Drive, GitHub, etc.), and triggers.

## Trigger Types

| Type | How It Works | Used For |
|------|-------------|----------|
| **Schedule** | Cron-based (daily, every other day, etc.) | Regular operational loops |
| **API** | HTTP POST to /fire endpoint with optional `text` field | Follow-up responses via [[ttai-slack-bridge]] |
| **GitHub Events** | Triggered by repo activity (push, PR, issue) | Not currently used by TTAI employees |

## Key Properties

- **Ephemeral sessions:** Each run starts fresh with no memory of prior runs. All persistent state must live in repos, trackers, or external tools. See [[repos-are-employee-memory]].
- **Connector-first:** Data access via MCP connectors (Slack, Google Drive, Gmail, GitHub) rather than Computer Use browser automation. See [[connectors-beat-computer-use]].
- **Dual-mode prompts:** The same prompt handles both scheduled runs and API follow-ups by checking whether the `text` field is present.
- **Daily run cap:** There is an account-level daily limit on routine runs.

## TTAI Employee Migration Status

| Employee | Previous Platform | Routines Status | Notes |
|----------|------------------|----------------|-------|
| Wiki | Cowork + Computer Use | Migrated (2026-04-15) | Fully operational |
| Mark-Lite | Cowork | Pending | Needs dual-mode prompt restructure |
| Fred | Cowork | Pending | Priority -- NBA playoffs need daily attention |

## Advantages Over Cowork

- No Computer Use overhead (faster, cheaper, more reliable)
- Runs on cloud (no dependency on Andy's laptop being on)
- API trigger enables two-way Slack interaction
- Connector-based data access is structured and predictable

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Routes Slack replies to routine API endpoints
- [[cowork-pipeline]] -- Previous platform (being phased out)
- [[connectors-beat-computer-use]] -- Migration principle
- [[repos-are-employee-memory]] -- Memory architecture principle

## Sources

- Wiki Agent migration session (2026-04-15)
