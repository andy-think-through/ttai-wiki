# Claude Code Routines

> Platform for running TTAI autonomous employees. Runs on Anthropic cloud infrastructure. Replaced Cowork scheduled tasks.
> Last updated: 2026-04-16

## What It Is

Claude Code Routines is the execution platform for TTAI's autonomous AI employees. Each employee is a Routine with a prompt (SKILL file), connectors, and triggers.

## Trigger Types

| Type | Use Case | Example |
|------|----------|---------|
| **Schedule** | Regular cadence runs | Wiki every other day, Mark-Lite daily |
| **API** | Reactive follow-ups | Andy replies in Slack -> bridge fires API -> employee responds |
| **GitHub events** | Repo-driven triggers | Not currently used by TTAI employees |

## How Employees Use Routines

1. **Prompt:** The SKILL file defines the employee's identity, mission, and workflows
2. **Dual-mode pattern:** Check for `text` field in API trigger. Present = follow-up mode. Absent = scheduled run.
3. **Connectors:** Slack, Google Drive, Gmail, GitHub -- connector-first access replaces Computer Use
4. **Memory:** GitHub repos persist state between ephemeral sessions. Each run clones the repo, reads state, makes changes, commits and pushes.
5. **Reporting:** All output goes to Slack #ttai-employees

## Key Characteristics

- **Ephemeral sessions:** Each run starts fresh with no conversation memory
- **Cloud-hosted:** Runs on Anthropic infrastructure, no dependency on Andy's laptop
- **Daily run cap:** Account-level limit on runs per day
- **Branch config:** Set per-trigger; employees should push to main for personal repos

## Migration from Cowork

Cowork scheduled tasks used Computer Use (Min browser) to scan Claude.ai conversations. Routines replace this with connector-based information gathering -- faster, cheaper, more reliable. See [[connectors-beat-computer-use]].

| Employee | Migration Status |
|----------|-----------------|
| Wiki | Migrated (2026-04-15) |
| Mark-Lite | Migrated (2026-04-16) |
| Fred | Pending -- still Cowork-based, paused |

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Bridge routing Slack to API endpoints
- [[cowork-pipeline]] -- Previous platform (being phased out)
- [[connectors-beat-computer-use]] -- Key migration principle

## Sources

- Wiki Agent migration session (2026-04-15)
