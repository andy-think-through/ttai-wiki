# Claude Code Routines

> Platform for running TTAI's autonomous employees. Cloud-based, API-triggerable, connector-first.
> Last updated: 2026-04-16

## What It Is

Claude Code Routines is the infrastructure layer beneath TTAI's employee SKILL files. Each routine is a Claude Code session that runs on Anthropic's cloud, triggered on schedule or via API. It replaces Cowork scheduled tasks for autonomous employees.

## Trigger Types

| Type | Use Case | TTAI Usage |
|------|----------|------------|
| **Schedule** | Recurring tasks (daily, every other day) | Employee daily/scheduled runs |
| **API** | On-demand, event-driven | Follow-up mode via [[ttai-slack-bridge]] |
| **GitHub Events** | Repo activity (push, PR, issue) | Not currently used by employees |

## How Employees Use Routines

Each employee is a single routine with both schedule and API triggers:

- **Schedule trigger:** Fires the employee's full operational loop (80% exploitation + 20% exploration)
- **API trigger:** Fires with a `text` field containing Andy's Slack reply. Employee runs in follow-up mode -- reads the message, responds, does any required work.

This is the **dual-mode prompt pattern**: same prompt handles both modes via a branch on whether `text` is present. See [[employee-framework]].

## Key Characteristics

- **Ephemeral sessions:** Each run starts fresh. No conversation memory between runs.
- **Persistent state via repos:** All state must live in connected GitHub repos, Google Sheets, or other external stores. See [[repos-are-employee-memory]].
- **Connector-first:** Information comes via Slack connector, Google Drive, filesystem (repo clone) -- not Computer Use. See [[connectors-beat-computer-use]].
- **Daily run cap:** Account-level limit on routine runs per day. Relevant for scheduling multiple employees.

## Current Employee Routines

| Employee | Schedule | API Trigger | Status |
|----------|----------|-------------|--------|
| Wiki | Every other day | Via Slack bridge | **Live** (2026-04-15) |
| Fred | Daily | Via Slack bridge | **Pending migration** (still Cowork) |
| Mark-Lite | Daily | Via Slack bridge | **Pending migration** (still Cowork) |

## Migration Path (Cowork to Routines)

For each employee:

1. Restructure the SKILL.md prompt to the dual-mode pattern (check `text` field)
2. Replace Computer Use information gathering with connector-based sources (Slack, Google Drive, inbox)
3. Change reporting from email to Slack #ttai-employees
4. Deploy as Claude Code Routine with schedule + API triggers
5. Add API endpoint and token to [[ttai-slack-bridge]] env vars
6. Test end-to-end: scheduled run posts to Slack, Andy replies, bridge fires API, follow-up posts back

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Routes Slack replies to routine API endpoints
- [[wiki-agent-SKILL]] -- First employee migrated to Routines
- [[fred-autostrategy-employee-SKILL]] -- Pending migration
- [[cowork-pipeline]] -- Previous platform (being phased out)
- [[connectors-beat-computer-use]] -- Core design principle
- [[repos-are-employee-memory]] -- Core design principle

## Sources

- Wiki Agent migration session (2026-04-15)
- Wiki ingest file: "Wiki Agent Migrated to Routines + Slack Bridge Deployed"
