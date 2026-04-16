# Wiki Agent -- Routines Job Spec

> Autonomous knowledge curator for Think Through AI. Runs every other day on Claude Code Routines. Maintains the LLM Wiki, processes ingest files, reads Slack reports from colleagues, spots cross-domain patterns.
> Last updated: 2026-04-16

## Platform

- **Runtime:** Claude Code Routines (Anthropic cloud)
- **Triggers:** Schedule (every other day) + API (follow-up from Slack via [[ttai-slack-bridge]])
- **Repo:** github.com/andy-think-through/ttai-wiki (private). Source of truth for all wiki content.
- **Reporting:** Slack #ttai-employees
- **Previous platform:** Cowork scheduled task with Computer Use (migrated 2026-04-15)

## Dual-Mode Pattern

Wiki runs in two modes, determined by the presence of a `text` field in the API trigger:

1. **Scheduled Run (no input text):** Full daily loop -- gather information, update wiki, explore patterns, report to Slack.
2. **Follow-Up (input text present):** Andy or a colleague has sent a message. Read it, respond to it, do any wiki work it requires, post response to Slack.

This pattern is universal across all TTAI employees. See [[employee-framework]] for the template.

## Information Sources (Priority Order)

1. **Wiki inbox** -- `inbox/` folder in the repo. Structured ingest files dropped by the wiki-ingest skill from other Claude projects. Pre-formatted, easy to process.
2. **Slack #ttai-employees** -- Reports from Fred and Mark-Lite. Andy's messages and replies. Live status updates.
3. **Connected tools** -- Google Drive docs, Google Sheets trackers, Gmail threads (if connectors available).

## Daily Loop (80% -- Keep the Wiki Fresh)

1. Read `index.md` for current page catalog
2. Read `log.md` for last scan date and coverage
3. Check `inbox/` for new ingest files
4. Read Slack #ttai-employees for recent messages from Fred, Mark-Lite, Andy
5. For each piece of new information, check whether wiki already reflects it
6. Build change list before writing
7. Update pages following SCHEMA.md conventions
8. Propagate changes to all linked pages
9. Update `index.md` if pages created or renamed
10. Append to `log.md`

## Exploration (20% -- Spot Patterns)

After updates, switch to exploration mode:

- Read across all pages just updated
- Read `strategy/opportunities.md` for known patterns
- Read `principles/_index.md` for current principle set
- Read recent Slack from Fred and Mark-Lite
- Write 2-4 bullet points of genuine cross-domain insight

## Autonomy Boundaries

**Can do (no approval):** Update factual status, process inbox, create pages, add cross-references, flag contradictions, post to Slack, run lint checks.

**Needs Andy's approval:** Resolving contradictions, strategic judgments, deleting/archiving pages, anything that changes business direction.

**Cannot do:** Send messages outside #ttai-employees, make strategic decisions for Andy, add speculative ideas Andy hasn't discussed, modify raw source files.

## Migration Notes (from Cowork)

| Aspect | Cowork (old) | Routines (current) |
|--------|-------------|-------------------|
| Information gathering | Computer Use scanning Claude.ai conversations | Slack connector + inbox folder + Google Drive |
| State persistence | Local filesystem | GitHub repo (cloned fresh each run) |
| Reporting | Email to Andy | Slack #ttai-employees |
| Runtime | 15-30 min, frequent failures | 5-15 min, clean tool calls |
| Two-way interaction | None (one-way email) | API trigger via [[ttai-slack-bridge]] |

## Links

- [[employee-framework]] -- Universal employee operating model
- [[ttai-slack-bridge]] -- Infrastructure routing Slack replies to routine API endpoints
- [[claude-code-routines]] -- Platform documentation
- [[connectors-beat-computer-use]] -- Principle validated by this migration
- [[repos-are-employee-memory]] -- Principle: repos as persistent state for ephemeral sessions
- [[cowork-pipeline]] -- Previous platform (being phased out)

## Sources

- Wiki Agent migration session (2026-04-15)
- Wiki ingest file: "Wiki Agent Migrated to Routines + Slack Bridge Deployed"
