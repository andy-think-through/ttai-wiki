# Repos Are Employee Memory

> Routine sessions are ephemeral. Persistent state must live in connected repos or trackers, not in conversation memory.
> Last updated: 2026-04-16

## The Principle

AI employees running on ephemeral infrastructure (Claude Code Routines, Cowork sessions) start each run with zero memory of previous runs. Any state that needs to persist -- wiki pages, tracker data, decision logs, reports -- must be written to durable storage (GitHub repos, Google Sheets, Slack messages) before the session ends.

## Where It Was Discovered

Wiki Agent's first day on Routines (2026-04-16). Eight Wiki runs posted Slack reports claiming "5 pages created, 7 updated" -- but committed to ephemeral branches that no longer existed on subsequent runs. The repo on `main` was unchanged. If it isn't committed to the right branch, it didn't happen.

## Where It Applies

- **Wiki:** GitHub repo `andy-think-through/ttai-wiki` is the source of truth
- **Fred:** Google Sheets betting tracker + autostrategy repo
- **Mark-Lite:** Google Sheets prospect trackers + mark-lite repo
- **Any future employee:** Design for amnesia. Write state early and often.

## The Failure Mode

```
Run 1: Does work, commits to branch-A, posts "done!" to Slack
Run 2: Starts fresh, clones repo, branch-A doesn't exist locally -> work is invisible
Run 3: Repeats Run 1's work on branch-C
...
N runs later: N branches exist, none merged, main is stale
```

This happened to Wiki on 2026-04-16 -- 8+ runs on ephemeral branches, all lost.

## Mitigation

- Push to `main` directly for personal repos (git history is the audit trail)
- For shared repos, merge branches promptly
- Design employees to check what state already exists before redoing work
- Write state early in the run, not just at the end

## Links

- [[connectors-beat-computer-use]] -- Companion principle
- [[employee-framework]] -- Universal employee operating model
- [[claude-code-routines]] -- Platform documentation
- [[scheduled-tasks-need-zero-intervention]] -- Related operational principle

## Sources

- Wiki Agent's first day on Routines (2026-04-16)
- 8 ephemeral branch runs proving the failure mode in real time
