# Claude Code Routines

> Platform documentation for Claude Code Routines -- the infrastructure layer beneath TTAI's autonomous employees. Replaced Cowork scheduled tasks as of April 2026.
> Last updated: 2026-04-16

## What It Is

Claude Code Routines is Anthropic's cloud-based execution platform for recurring Claude Code sessions. Each routine is a self-contained prompt that runs on a schedule or in response to an API trigger. Sessions are ephemeral -- no state carries between runs.

TTAI uses Routines as the runtime for its autonomous employees (Wiki, Fred, Mark-Lite).

## Trigger Types

| Type | How It Fires | Use Case |
|------|-------------|----------|
| **Schedule** | Cron-like schedule (daily, every other day, etc.) | Employee's core operational loop |
| **API** | POST to `/fire` endpoint with optional `text` field | Follow-up responses to Slack messages (via TTAI Slack Bridge) |
| **GitHub Events** | Push, PR, issue events on connected repos | Not currently used by TTAI employees |

## How Employees Use Routines

Each employee is a single routine with two triggers:

1. **Schedule trigger** -- Fires the employee's main loop (scan, update, report)
2. **API trigger** -- Fires when Andy replies in Slack (routed via [[ttai-slack-bridge]])

The employee's prompt contains a dual-mode branch:
- If `text` field is empty → Scheduled Run (full loop)
- If `text` field has content → Follow-Up (respond to the specific message)

This dual-mode prompt pattern is universal across all employees.

## Key Characteristics

### Ephemeral Sessions
Each run starts with a fresh context. No memory of previous runs. Persistent state must live in:
- **GitHub repos** -- Wiki pages, code, config (see [[repos-are-employee-memory]])
- **Google Sheets** -- Trackers, data stores
- **Slack** -- Message history readable via connector

### Connectors (MCP Servers)
Routines can connect to external tools via MCP:
- **Slack** -- Read/write messages in channels
- **GitHub** -- Read/write repo files, create PRs
- **Google Drive** -- Read/write documents
- **Gmail** -- Read/send emails
- **Google Sheets** -- Read/write spreadsheet data

### Daily Run Limits
Anthropic applies a daily run cap per account. Current volume (Wiki every other day + Fred daily + Mark-Lite daily) is well within limits.

## Advantages Over Cowork

| Aspect | Cowork | Routines |
|--------|--------|----------|
| **Infrastructure** | Andy's Mac must be on | Anthropic cloud |
| **Information gathering** | Computer Use / Min browser (slow, fragile) | MCP connectors (fast, reliable) |
| **Two-way interaction** | One-way (email report) | Slack + API trigger loop |
| **Cross-employee visibility** | None (separate email threads) | Shared Slack channel |
| **Cost** | Computer Use tokens + session time | Routine tokens only (no browser overhead) |
| **Reliability** | Browser timeouts, sandbox restrictions | Clean tool calls |

## Current TTAI Routines

| Routine | Employee | Schedule | API | Status |
|---------|----------|----------|-----|--------|
| Wiki Agent | Wiki | Every other day | Active | Live since 2026-04-15 |
| Fred AutoStrategy | Fred | Daily | Not yet | Pending migration from Cowork |
| Mark-Lite Campaign | Mark-Lite | Daily | Not yet | Pending migration from Cowork |

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Slack-to-Routine routing
- [[wiki-agent-SKILL]] -- First employee migrated to Routines
- [[cowork-pipeline]] -- Predecessor platform (being phased out)
- [[connectors-beat-computer-use]] -- Principle discovered during migration
- [[repos-are-employee-memory]] -- Principle discovered during migration

## Sources

- Wiki Agent migration conversation (2026-04-15)
- Ingest file: 2026-04-16-wiki-agent-migration-routines-slack-bridge.md
