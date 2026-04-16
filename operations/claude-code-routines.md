# Claude Code Routines

> Platform documentation for Claude Code Routines -- the infrastructure layer beneath TTAI's autonomous employees.
> Last updated: 2026-04-16

## What It Is

Claude Code Routines run on Anthropic's cloud infrastructure. They replace Cowork scheduled tasks for TTAI's autonomous employees. Each routine is a Claude Code session that executes a prompt with access to connected tools (MCP servers for Slack, Google Drive, GitHub, etc.).

## Trigger Types

| Type | How It Works | TTAI Use Case |
|------|-------------|---------------|
| **Schedule** | Runs on a cron-like cadence (daily, every other day, etc.) | Employee daily/regular runs |
| **API** | Fired via POST to a `/fire` endpoint with optional `text` payload | Follow-up responses via Slack bridge |
| **GitHub Events** | Triggered by repo events (push, PR, issue) | Not currently used by employees |

TTAI employees use **Schedule + API** triggers. The schedule handles the regular operational loop; the API handles follow-up interactions routed through the [[ttai-slack-bridge]].

## Dual-Mode Prompt Pattern

All TTAI employees use the same prompt structure:

1. Check whether the API trigger passed a `text` field
2. If **no text**: run the full scheduled operational loop (Mode 1)
3. If **text present**: respond to the specific input (Mode 2 -- follow-up)

This means one prompt handles both autonomous operation and reactive interaction. The pattern is documented in [[employee-framework]] and proven end-to-end with Wiki.

## Key Characteristics

- **Ephemeral sessions** -- Each run starts fresh with no memory of prior runs. Persistent state must live in the connected repo, trackers, or external tools. See [[repos-are-employee-memory]].
- **Connector-first data access** -- Information comes via MCP connectors (Slack, Google Drive, GitHub), not browser automation. See [[connectors-beat-computer-use]].
- **Daily run cap** -- Account-level limit on routine runs per day. Not currently a constraint for three employees.
- **Runtime** -- Wiki completes in 5-15 minutes (down from 15-30 min on Cowork with Computer Use).

## Advantages Over Cowork

| Aspect | Cowork | Routines |
|--------|--------|----------|
| Infrastructure | Andy's Mac must be on | Anthropic cloud |
| Data access | Computer Use (browser) | MCP connectors |
| Interaction | One-way (email reports) | Two-way (Slack + API trigger) |
| Runtime | 15-30 min | 5-15 min |
| Reliability | Frequent CU failures | Clean tool calls |
| Cost | CU token overhead | Lower (no vision tokens) |

## Current Employee Status

| Employee | Platform | Migration Status |
|----------|----------|-----------------|
| Wiki | Routines | Complete (2026-04-15) |
| Fred | Cowork | Pending -- needs prompt restructuring for dual-mode pattern |
| Mark-Lite | Cowork | Pending -- needs prompt restructuring for dual-mode pattern |

## Migration Checklist (Cowork to Routines)

For Fred and Mark-Lite, the following changes are needed:
1. Restructure SKILL.md to dual-mode prompt pattern (check `text` field)
2. Replace email reporting with Slack #ttai-employees posting
3. Replace Computer Use / Desktop Commander references with MCP connector equivalents
4. Replace local filesystem paths with repo-relative paths
5. Add Routine API endpoint + token to Slack bridge env vars

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Slack bridge for two-way interaction
- [[wiki-agent-SKILL]] -- First migrated employee
- [[cowork-pipeline]] -- Predecessor system (phasing out)
- [[connectors-beat-computer-use]] -- Key migration principle
- [[repos-are-employee-memory]] -- Key architecture principle

## Sources

- Wiki Agent migration session (2026-04-15)
- Wiki-ingest file: "Wiki Agent Migrated to Routines + Slack Bridge Deployed"
