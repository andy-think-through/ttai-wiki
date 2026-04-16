# Wiki Agent -- Routines Job Spec

> The Wiki Knowledge Curator employee, migrated from Cowork to Claude Code Routines.
> Last updated: 2026-04-16

## Overview

Wiki is TTAI's Knowledge Curator -- an autonomous employee responsible for keeping the cross-domain LLM Wiki current and surfacing insights Andy wouldn't spot on his own. Runs every other day on schedule, plus reactive follow-ups via Slack.

## Platform

- **Runtime:** Claude Code Routine (Anthropic cloud)
- **Triggers:** Schedule (every other day) + API (Slack replies via bridge)
- **Repo:** `andy-think-through/ttai-wiki` (GitHub, private) -- source of truth
- **Reporting:** Slack #ttai-employees
- **Previous platform:** Cowork scheduled task using Computer Use (Min browser) to scan Claude.ai conversations. Migrated 2026-04-15.

## Dual-Mode Operation

The prompt checks for an API `text` field:

- **No text (scheduled run):** Full daily loop -- gather info from inbox + Slack + connected tools, update wiki, explore cross-domain patterns, post report.
- **Text present (follow-up):** Respond to Andy's message -- answer questions, process new information, make corrections, execute instructions. Skip the full scan.

## Information Sources

| Source | Method | Priority |
|--------|--------|----------|
| Wiki inbox (`inbox/`) | Read files committed to repo | 1 |
| Slack #ttai-employees | Slack connector (read channel) | 2 |
| Google Drive / Sheets | Drive/Sheets connectors (if available) | 3 |

## Key Differences from Cowork Version

| Aspect | Cowork (old) | Routines (current) |
|--------|-------------|-------------------|
| Information gathering | Computer Use scanning Claude.ai conversations | Connectors (Slack, inbox files, Drive) |
| Runtime | 15-30 min, frequent failures | 5-15 min, reliable |
| Reporting | Email (one-way) | Slack (two-way, enables follow-ups) |
| State persistence | Local filesystem on Andy's Mac | GitHub repo (cloud-accessible) |
| Machine dependency | Required Andy's laptop to be on | Runs on Anthropic cloud |
| Cross-employee visibility | None | Shared Slack channel |

## Autonomy Boundaries

**Can do autonomously:** Update factual status, process inbox, create/update pages, add cross-references, flag contradictions, post to Slack, run lint checks.

**Needs approval:** Resolving contradictions, strategic judgments, deleting/archiving pages, anything changing business direction.

**Cannot do:** Message anyone outside #ttai-employees, make strategic decisions, add speculative ideas, modify raw source files.

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Bridge infrastructure enabling follow-ups
- [[claude-code-routines]] -- Platform documentation
- [[connectors-beat-computer-use]] -- Principle discovered during migration
- [[repos-are-employee-memory]] -- Principle discovered during migration

## Sources

- Wiki Agent migration session (2026-04-15)
- Employee framework universal traits
