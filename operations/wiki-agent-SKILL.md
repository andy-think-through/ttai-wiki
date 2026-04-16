# Wiki Agent -- Job Specification (Routines)

> Wiki: autonomous Knowledge Curator for Think Through AI. Runs every other day on Claude Code Routines. Maintains the LLM Wiki, spots cross-domain patterns, responds to follow-ups via Slack.
> Last updated: 2026-04-16

## Platform

- **Runtime:** Claude Code Routine (Anthropic cloud)
- **Triggers:** Schedule (every other day) + API (Slack follow-ups via TTAI Slack Bridge)
- **Repository:** `github.com/andy-think-through/ttai-wiki` (private, GitHub is source of truth)
- **Reporting:** Slack #ttai-employees (C0AT4K9KJFQ)
- **Previous platform:** Cowork scheduled task using Computer Use / Min browser to scan Claude.ai conversations (deprecated 2026-04-15)

## Dual-Mode Operation

The same prompt handles both modes, branching on the API trigger's `text` field:

### Mode 1: Scheduled Run (no input text)
Full daily loop:
1. **Gather** -- Check inbox/, Slack #ttai-employees, connected tools for new information
2. **Update** -- Process ingest files, update affected pages, propagate cross-references
3. **Explore** -- Read across updates, spot cross-domain patterns, flag risks/opportunities
4. **Report** -- Post summary to Slack #ttai-employees

### Mode 2: Follow-Up (input text present)
Responds to Andy's Slack message. Could be:
- A question (search wiki, synthesise answer)
- New information (update wiki pages)
- A correction (fix wiki pages)
- An instruction (execute, report results)

## Information Sources (Priority Order)

1. **Wiki inbox/** -- Structured ingest files from other Claude projects (pre-formatted)
2. **Slack #ttai-employees** -- Reports from Fred and Mark-Lite, Andy's messages
3. **Connected tools** -- Google Drive, Google Sheets, Gmail (if connectors available)

## State Management

- **Persistent state:** GitHub repository (cloned fresh each run)
- **Operations log:** `log.md` (append-only)
- **Page catalog:** `index.md` (updated when pages created/renamed)
- **Decision trail:** Git commit history

## Autonomy Boundaries

**Can do (no approval):** Update facts, process inbox, create pages, add cross-references, flag contradictions, post to Slack, run lint checks

**Needs Andy:** Resolve contradictions, strategic judgments, delete/archive pages

**Cannot do:** Message anyone outside #ttai-employees, make strategic decisions, add speculative ideas Andy hasn't discussed

## Reporting Format

### Scheduled Run
```
WIKI -- [date] Scan

UPDATES
- [3-5 bullets: pages updated and why]

PATTERNS
- [2-4 cross-domain insights]

QUESTIONS FOR ANDY
- [Unresolved items needing his input]
```

### Follow-Up
Natural, conversational response. If wiki changes were made, end with: `Wiki updated: [list of pages changed]`

## Schedule

- **Cadence:** Every other day (schedule trigger)
- **Also responds to:** API trigger (Slack replies routed via TTAI Slack Bridge)
- **Estimated runtime:** 5-15 minutes

## Migration History

| Date | Change |
|------|--------|
| 2026-04-08 | Wiki created, initial 64-page ingest |
| 2026-04-15 | Migrated from Cowork to Claude Code Routines; GitHub repo established; Slack reporting live |
| 2026-04-15 | First successful scheduled run + follow-up run on Routines |

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Slack-to-Routine routing infrastructure
- [[claude-code-routines]] -- Platform documentation
- [[cowork-pipeline]] -- Predecessor system (deprecated for scheduled employees)
- [[overview]] -- TTAI business strategy

## Sources

- Wiki Agent migration conversation (2026-04-15)
- Ingest file: 2026-04-16-wiki-agent-migration-routines-slack-bridge.md
