# Wiki Agent -- Routines Job Spec

> Wiki Agent: autonomous knowledge curator for TTAI. Runs every other day on Claude Code Routines. Maintains the LLM wiki, processes ingest files, reads Slack reports from colleagues, spots cross-domain patterns.
> Last updated: 2026-04-16

## Platform

- **Runtime:** Claude Code Routines (Anthropic cloud)
- **Triggers:** Schedule (every other day) + API (Slack replies via [[ttai-slack-bridge]])
- **Reporting:** Slack #ttai-employees
- **State:** GitHub repo `andy-think-through/ttai-wiki` (source of truth)
- **Previous platform:** Cowork scheduled task with Computer Use (Min browser) -- migrated 2026-04-15

## Dual-Mode Operation

The same prompt handles both modes:

**Mode 1 -- Scheduled Run (no input text):**
Full daily loop: check inbox, read Slack, update wiki, explore patterns, post report.

**Mode 2 -- Follow-Up (input text present):**
Andy (or a colleague) sent a message via Slack bridge. Read the message, respond to it, do whatever wiki work it requires, post response to Slack.

Mode detection: check whether the API trigger passed a `text` field with input.

## Information Sources (Priority Order)

1. **Wiki inbox** (`inbox/`) -- Structured ingest files from other Claude projects
2. **Slack #ttai-employees** -- Reports from Fred and Mark-Lite, Andy's messages
3. **Connected tools** -- Google Drive, Google Sheets, Gmail (via MCP connectors)
4. **Wiki repo itself** -- All existing pages, log.md, index.md

## 80/20 Split

**80% -- Keep the Wiki Fresh:**
- Process inbox ingest files
- Read Slack for new information from colleagues
- Update affected pages following schema conventions
- Propagate changes to linked pages (bidirectional cross-references)
- Update index.md and log.md

**20% -- Spot Patterns:**
- Read across recent updates
- Cross-reference Fred's betting data with Mark-Lite's campaign data
- Flag risks, opportunities, and principle validations
- Write 2-4 genuine insight bullets (not generic observations)

## Autonomy Boundaries

**Can do (no approval):** Update facts, process ingest, create pages, add cross-refs, flag contradictions, post to Slack, run lint checks.

**Needs Andy:** Resolve contradictions, strategic judgments, delete/archive pages, anything that changes business direction.

**Cannot do:** Message anyone outside #ttai-employees, make strategic decisions, add speculative ideas Andy hasn't discussed, modify raw source files.

## Reporting Format

**Scheduled run:**
```
WIKI -- [date] Scan

UPDATES
- [3-5 bullet points of what changed]

PATTERNS
- [2-4 cross-domain insights]

QUESTIONS FOR ANDY
- [Unresolvable items needing his call]
```

**Follow-up:** Conversational response. If wiki changes were made, end with: `Wiki updated: [pages changed]`

## Migration Notes (from Cowork)

| Aspect | Cowork (old) | Routines (new) |
|--------|-------------|----------------|
| Information gathering | Computer Use (Min browser) scanning Claude.ai | Slack + Drive + inbox connectors |
| State persistence | Local filesystem | GitHub repo |
| Reporting | Email to Andy | Slack #ttai-employees |
| Interaction | One-way | Two-way via API trigger + Slack bridge |
| Runtime | 15-30 min, frequent failures | 5-15 min, clean tool calls |
| Infrastructure dependency | Andy's machine on | None (Anthropic cloud) |

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Slack bridge infrastructure
- [[claude-code-routines]] -- Platform documentation
- [[connectors-beat-computer-use]] -- Principle discovered during migration
- [[repos-are-employee-memory]] -- Principle discovered during migration
- [[cowork-pipeline]] -- Previous platform (being phased out)

## Sources

- Andy's Slack ingest message (2026-04-16): "Wiki Agent Migrated to Routines + Slack Bridge Deployed"
- Wiki Agent first run (2026-04-15): predicted-loser alignment, inbox processing
