# Repos Are Employee Memory

> Routine sessions are ephemeral. Persistent state must live in connected repos or trackers, not in conversation memory. If it isn't committed, it didn't happen.
> Last updated: 2026-04-16

## The Principle

AI employees running on ephemeral infrastructure (Claude Code Routines, Cowork) start each session with zero memory of prior runs. All persistent state -- decision logs, tracker updates, wiki pages, reports -- must be written to external stores (GitHub repos, Google Sheets, Slack) during the run. Relying on conversation memory is a single point of failure.

## Where It Was Discovered

Wiki Agent migration to Routines (2026-04-15). Proven dramatically on 2026-04-16 when four Wiki runs posted Slack reports claiming "5 pages created, 7 updated" but failed to commit changes to the repo. Each subsequent run started fresh and found the repo unchanged. The work only persisted when a run actually committed and pushed.

## Where It Applies

- **Wiki:** GitHub repo `andy-think-through/ttai-wiki` is the source of truth. Every update must be committed.
- **Fred:** Google Sheets betting tracker + autostrategy repo. Decisions, bets, results must be written to sheets/files.
- **Mark-Lite:** Google Sheets prospect tracker + mark-lite repo. Campaign state, decision log, daily reports.
- **Any future employee:** Design for ephemeral sessions from day one. Write state early and often.

## Corollary: Write State Early

Don't batch all writes to the end of a run. If the session times out or fails partway through, everything after the last write is lost. Commit incrementally.

## Evidence

2026-04-16: Four Wiki runs on different branches. Runs 1 and 2 posted to Slack but didn't commit. Runs 3 and 4 committed to different branches. Result: 4 Slack reports, 2 branches with changes, 2 branches empty. Branch proliferation compounded the problem.

## Links

- [[employee-framework]] -- Universal employee operating model
- [[claude-code-routines]] -- Ephemeral platform that necessitates this principle
- [[scheduled-tasks-need-zero-intervention]] -- Related operational principle

## Sources

- Wiki Agent migration session (2026-04-15)
- 2026-04-16 Wiki branch proliferation incident
