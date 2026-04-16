# Claude Code Routines

> The infrastructure platform that runs TTAI's autonomous employees. Replaced Cowork scheduled tasks starting 2026-04-15.
> Last updated: 2026-04-16

## What It Is

Claude Code Routines run on Anthropic's cloud infrastructure. Each routine is a Claude Code session that can be triggered on a schedule, via API, or by GitHub events. TTAI uses routines as the execution layer for autonomous employees -- each employee is a routine with a specific prompt and connected tools.

## Trigger Types

| Type | How It Works | TTAI Use Case |
|------|-------------|---------------|
| **Schedule** | Runs at defined intervals (daily, every other day, etc.) | Employee's regular operational loop |
| **API** | POST to /fire endpoint with optional `text` field | Follow-up mode -- Andy's Slack replies via [[ttai-slack-bridge]] |
| **GitHub Events** | Triggered by repo events (push, PR, issue) | Not currently used by employees |

## Dual-Mode Prompt Pattern

All TTAI employees use the same prompt structure:

```
1. Check whether API trigger passed a `text` field
2. If no text → Mode 1: Scheduled Run (full daily loop)
3. If text present → Mode 2: Follow-Up (respond to the specific message)
```

This pattern is universal across employees. It enables:
- Scheduled autonomous work (the core job)
- Reactive follow-ups from Andy via Slack
- Cross-employee messaging (future: employees triggering each other)

## Key Properties

- **Ephemeral sessions:** Each routine run starts fresh with no memory of prior runs. Persistent state must live in connected repos, Google Sheets, or other external stores. See [[repos-are-employee-memory]].
- **Connected tools:** Slack, Google Drive, Gmail, GitHub repos -- accessed via MCP connectors, not Computer Use.
- **Daily run cap:** Account-level limit on daily routine executions. Plan employee cadences accordingly.

## Current Employees on Routines

| Employee | Routine Status | Cadence | Connected Repo |
|----------|---------------|---------|----------------|
| Wiki | Live (2026-04-15) | Every other day + API | `andy-think-through/ttai-wiki` |
| Fred | Pending migration | Daily (planned) | `autostrategy` repo (TBD) |
| Mark-Lite | Pending migration | Daily (planned) | `mark-lite` repo (TBD) |

## Migration from Cowork

Cowork scheduled tasks were the previous platform. Key differences:

| Aspect | Cowork | Routines |
|--------|--------|----------|
| Execution | Andy's local machine | Anthropic cloud |
| Information gathering | Computer Use (Min browser) | Connectors (Slack, Drive, repo) |
| Reporting | Email | Slack #ttai-employees |
| Interaction | One-way (email out) | Two-way (Slack reply -> API trigger -> follow-up) |
| Runtime | 15-30 min (browser overhead) | 5-15 min (connector-based) |
| Reliability | Fragile (browser timeouts, screenshots) | Stable (clean tool calls) |

See [[cowork-pipeline]] for the predecessor system.

## Adding a New Employee

1. Write the SKILL prompt following [[employee-framework]] conventions
2. Include the dual-mode prompt pattern (check `text` field at top)
3. Create or connect the employee's persistent state repo/tracker
4. Create the routine on Anthropic with schedule + API triggers
5. Add the employee's API endpoint and token to [[ttai-slack-bridge]] env vars
6. Test: scheduled run posts to Slack; API trigger responds to Slack reply

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Routes Slack replies to routine API endpoints
- [[wiki-agent-SKILL]] -- First employee on Routines
- [[cowork-pipeline]] -- Predecessor platform (being phased out for scheduled employees)
- [[connectors-beat-computer-use]] -- Principle: connectors > browser automation
- [[repos-are-employee-memory]] -- Principle: ephemeral sessions need external state

## Sources

- Wiki Agent migration session (2026-04-15)
- inbox/2026-04-15-wiki-agent-migrated-slack-bridge-deployed.md
