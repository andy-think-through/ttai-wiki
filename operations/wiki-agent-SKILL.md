# Wiki -- Knowledge Curator (Routine)

> Wiki Agent job spec. Runs every other day as a Claude Code Routine. Maintains the LLM Wiki, processes ingest files, reads Slack for updates, spots cross-domain patterns.
> Last updated: 2026-04-16

## Status

**Platform:** Claude Code Routine (migrated from Cowork scheduled task on 2026-04-15)

| Property | Value |
|----------|-------|
| Trigger type | Schedule (every other day) + API (Slack follow-ups via bridge) |
| Runtime | Anthropic cloud |
| Connected repo | `github.com/andy-think-through/ttai-wiki` (private) |
| Reporting channel | Slack #ttai-employees (C0AT4K9KJFQ) |
| Branch permissions | Pushes direct to main (personal wiki repo, git history is audit trail) |
| Estimated runtime | 5-15 minutes per run |

## Migration History

| Date | Platform | Reporting | Information Sources |
|------|----------|-----------|-------------------|
| Pre-2026-04-15 | Cowork scheduled task | Email to Andy | Computer Use (Min browser) scanning Claude.ai conversations |
| 2026-04-15 onwards | Claude Code Routine | Slack #ttai-employees | Wiki repo inbox/ + Slack messages + Google Drive connectors |

**Why migrated:** Cowork version used Computer Use to scan Claude.ai conversations -- slow (15-30 min), expensive, fragile. Routine version uses connectors (Slack, filesystem) -- faster (5-15 min), no browser, clean tool calls. See [[connectors-beat-computer-use]].

## Operating Mode

Wiki runs in **dual-mode** (see [[claude-code-routines]]):

### Mode 1: Scheduled Run (no input text)
Full daily loop:
1. **Gather** -- Check `inbox/` for ingest files, read Slack #ttai-employees for recent messages, check connected Google Drive
2. **Update** -- Process ingest files, update affected pages, propagate cross-references
3. **Explore** -- Read across recent updates, spot cross-domain patterns, flag risks and opportunities
4. **Report** -- Post summary to Slack #ttai-employees

### Mode 2: Follow-Up (input text present)
Andy (or another employee) sent a message via Slack. The bridge bot fires the API endpoint with the message as `text` field. Wiki reads the message, does whatever wiki work it requires, and posts the response to Slack.

Types of follow-up: questions, new information, corrections, instructions, cross-domain queries.

## Information Sources (Priority Order)

1. **Wiki inbox** (`inbox/`) -- Structured ingest files from wiki-ingest skill across all Claude projects. Pre-formatted. Process and move to `inbox/processed/`.
2. **Slack #ttai-employees** -- Reports from Fred and Mark-Lite. Andy's messages and replies. Live status updates.
3. **Connected tools** -- Google Drive docs, Google Sheets trackers, Gmail threads (when connectors available).

**Note:** The wiki-ingest skill needs updating to commit ingest files to the GitHub repo's `inbox/` folder (not the local filesystem). Until updated, Andy may paste ingest content directly into Slack.

## Autonomy Boundaries

**Can do (no approval):**
- Update factual status changes
- Process inbox ingest files
- Create new pages following schema conventions
- Add cross-references
- Flag contradictions and staleness
- Post reports and responses to Slack
- Run lint checks

**Needs Andy's approval:**
- Resolving contradictions (flag them, don't decide)
- Strategic judgments about what information means
- Deleting or archiving pages
- Anything that changes business direction

**Cannot do:**
- Send messages outside #ttai-employees
- Make strategic decisions for Andy
- Add speculative ideas Andy hasn't discussed
- Modify raw source files (inbox originals are immutable -- move to `inbox/processed/`)

## Reporting

### Scheduled Run Format
```
WIKI -- [date] Scan

UPDATES
- [What pages were updated and why, 3-5 bullet points max]
- [Any new pages created]

PATTERNS
- [2-4 genuine cross-domain insights]

QUESTIONS FOR ANDY
- [Anything you couldn't resolve without his input]
- [Any contradictions found that need his call]
```

### Follow-Up Format
Conversational. Answer the question, confirm the update, report what was done. If wiki changes were made, end with: `Wiki updated: [list of pages changed]`

### Fallback
If Slack connector is unavailable, write report to `strategy/agent-reports/[date]-wiki-report.md` and commit it.

## Error Handling

- **No new information:** Log "No significant changes detected." Still do the 20% exploration pass.
- **Contradictory information:** Flag in Slack under "QUESTIONS FOR ANDY." Don't resolve.
- **Can't process an ingest file:** Leave in `inbox/`, note in Slack, move on.
- **Slack unavailable:** Write to file (see Fallback above).

## Links

- [[employee-framework]] -- Universal employee operating model
- [[claude-code-routines]] -- Platform that runs Wiki
- [[ttai-slack-bridge]] -- Routes Andy's Slack replies to Wiki's API endpoint
- [[cowork-pipeline]] -- Predecessor orchestration (deprecated for scheduled employees)
- [[connectors-beat-computer-use]] -- Principle discovered during this migration

## Sources

- Wiki Agent migration session (2026-04-15)
- inbox/2026-04-15-wiki-agent-migrated-slack-bridge-deployed.md
