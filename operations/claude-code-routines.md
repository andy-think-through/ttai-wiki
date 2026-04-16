# Claude Code Routines

> Platform documentation for TTAI's autonomous employee infrastructure.
> Last updated: 2026-04-16

## What It Is

Claude Code Routines is the Anthropic cloud infrastructure that runs TTAI's autonomous employees. Each employee is a routine with a prompt, connected tools (Slack, GitHub, Drive), and trigger configuration.

## Trigger Types

| Type | Use Case | Example |
|------|----------|---------|
| **Schedule** | Regular cadence runs | Wiki every other day, Fred daily |
| **API** | Reactive follow-ups | Andy replies in Slack, bridge fires API |
| **GitHub events** | Repo-triggered actions | (Not currently used by TTAI employees) |

TTAI employees use **schedule + API** triggers. The dual-mode prompt pattern (check for `text` field) handles both modes in a single prompt.

## Daily Limits

There is a daily run cap per account. With three employees (Wiki every other day, Fred daily, Mark-Lite daily), this should be well within limits. Follow-up triggers from Slack replies count toward the cap.

## How Employees Use It

1. **Routine prompt** defines the employee's full job spec (dual-mode)
2. **Connected tools** provide access to Slack, GitHub, Google Drive/Sheets/Gmail
3. **Schedule trigger** fires the routine at the configured cadence
4. **API trigger** fires when the Slack bridge forwards a message
5. **Each run is ephemeral** -- no conversation memory between runs. All persistent state must be in the repo, trackers, or Slack history.

## Comparison to Cowork

| Aspect | Cowork | Routines |
|--------|--------|----------|
| Execution | Andy's Mac (Cowork scheduled task) | Anthropic cloud |
| Browser access | Computer Use (Min browser) | Not needed (connector-first) |
| Information | Scan Claude.ai conversations visually | Read Slack, inbox files, Drive docs |
| Reporting | Email or filesystem | Slack (two-way) |
| Cost | Computer Use tokens (expensive) | Standard API tokens |
| Reliability | Fragile (browser automation) | Reliable (structured tool calls) |

## Migration Status

| Employee | Platform | Status |
|----------|----------|--------|
| Wiki | Routines | Live since 2026-04-15 |
| Fred | Cowork | Migration pending -- needs prompt restructure for dual-mode, Slack reporting, repo-based state |
| Mark-Lite | Cowork | Migration pending -- same changes needed |

## Links

- [[employee-framework]] -- Universal employee operating model
- [[wiki-agent-SKILL]] -- First migrated employee
- [[ttai-slack-bridge]] -- Slack-to-routine routing
- [[cowork-pipeline]] -- Predecessor platform (phasing out)
- [[connectors-beat-computer-use]] -- Architectural principle

## Sources

- Wiki Agent migration session (2026-04-15)
- Claude Code Routines platform documentation
