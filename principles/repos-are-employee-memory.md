# Repos Are Employee Memory

> Routine sessions are ephemeral. Persistent state must live in the connected repo or trackers, not in conversation memory. Write state early and often.
> Last updated: 2026-04-16

## The Principle

When autonomous employees run on ephemeral infrastructure (Claude Code Routines, cloud functions, serverless), every run starts fresh with no memory of prior runs. All persistent state -- wiki pages, tracker data, decision logs, operational status -- must be written to a durable store (GitHub repo, Google Sheets, database) and committed/saved before the session ends.

If it isn't committed, it didn't happen.

## Where It Was Discovered

**Wiki Agent migration to Routines (2026-04-15).** The Routines architecture means each Wiki run starts from scratch -- no conversation history, no local files from last run. Wiki successfully reconstructed full context from the repo + Slack history on both scheduled and follow-up runs, proving the pattern works.

**Validated in real-time (2026-04-16).** Earlier Wiki runs today posted reports to Slack but failed to commit page changes to the repo. The work appeared to be done (Slack messages existed), but the repo was unchanged. The principle was proven within hours of being articulated.

## Where It Applies

| Employee | Durable State Store | What Gets Written |
|----------|-------------------|-------------------|
| Wiki | GitHub repo (ttai-wiki) | Wiki pages, index, log, inbox processing |
| Fred | Google Sheets (betting tracker) + autostrategy repo | P&L data, decision log, daily reports |
| Mark-Lite | Google Sheets (prospect tracker) + mark-lite repo | Outreach status, reply tracking, campaign data |

## Implications

1. **Write early, write often** -- Don't batch all writes to end-of-session. If the session crashes mid-run, uncommitted work is lost.
2. **Repo is the source of truth** -- Slack messages are ephemeral communication. The repo/tracker is the canonical state.
3. **Design for cold starts** -- Every employee prompt should be self-contained enough to reconstruct context from the durable store without prior conversation history.
4. **Commit before reporting** -- Always commit changes before posting the Slack report. A report claiming "5 pages updated" is misleading if the changes weren't persisted.

## Links

- [[employee-framework]] -- Universal employee operating model
- [[wiki-agent-SKILL]] -- Primary evidence source
- [[claude-code-routines]] -- Ephemeral platform this principle addresses
- [[scheduled-tasks-need-zero-intervention]] -- Related: autonomous operation requires durable state

## Sources

- Wiki Agent migration session (2026-04-15)
- Wiki Agent 2026-04-16 runs (real-time validation of the principle)
