# Principle: Repos Are Employee Memory

> Routine sessions are ephemeral. Persistent state must live in connected repos or trackers, not conversation memory. If it isn't committed, it didn't happen.
> Last updated: 2026-04-16

## The Principle

AI employees running on ephemeral infrastructure (Claude Code Routines, Cowork) lose all conversation state between runs. The only persistent memory is what gets written to external stores: GitHub repos, Google Sheets, Slack messages. Design all employee workflows around writing state early and often.

## Where It Was Discovered

**Wiki Agent first day on Routines (2026-04-16).** Eight Wiki runs posted Slack reports claiming "5 pages created, 7 updated" -- but committed to ephemeral branches that no longer existed on the next run's cold start. The repo on main was unchanged. Real-time proof that work not committed to the right branch is work that didn't happen.

## Where It Applies

| Employee | Memory Store | Risk If Not Committed |
|----------|-------------|----------------------|
| Wiki | GitHub wiki repo | Pages "created" but not persisted; next run redoes work |
| Fred | Google Sheets tracker + autostrategy repo | Bet history lost; P&L tracking gaps |
| Mark-Lite | Google Sheets tracker + mark-lite repo | Outreach state lost; duplicate sends possible |

## Implications

1. **Commit early, commit often.** Don't batch all changes to end of run.
2. **Push to a stable branch.** Ephemeral branches create orphaned work. For personal repos, push to main.
3. **Slack messages are also memory.** Reports posted to Slack persist even if repo commits fail -- Slack is a secondary audit trail.
4. **Decision logs belong in repos, not conversation.** If you reason about something important, write it down in a file and commit it.

## Exceptions

None. This is an absolute constraint of ephemeral infrastructure.

## Links

- [[employee-framework]] -- Universal operating model
- [[claude-code-routines]] -- Platform with ephemeral sessions
- [[wiki-agent-SKILL]] -- First employee to encounter this failure mode
- [[connectors-beat-computer-use]] -- Related infrastructure principle

## Sources

- Wiki Agent migration session (2026-04-15)
- 2026-04-16 branch proliferation incident (8+ orphaned branches)
