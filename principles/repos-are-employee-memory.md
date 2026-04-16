# Repos Are Employee Memory

> Routine sessions are ephemeral. Persistent state must live in connected repos or trackers, not in conversation memory.
> Last updated: 2026-04-16

## The Principle

When running autonomous employees on ephemeral infrastructure (like [[claude-code-routines]]), every piece of state the employee needs must be committed to a durable store -- a Git repo, a Google Sheet, or a database. If it isn't written to persistent storage, it didn't happen.

## Where It Was Discovered

Wiki Agent's first day on Routines (2026-04-16). Multiple runs in the same day created pages, posted Slack reports claiming "5 pages created, 7 updated" -- but committed to ephemeral branches that were never merged. Each subsequent run started fresh and couldn't see the prior run's work. The wiki was unchanged despite hours of apparent activity.

## Evidence

- 2026-04-16: 8+ Wiki runs posted comprehensive Slack reports. The repo only had changes from the April 15 scan. All other work was lost to orphaned branches.
- The principle was articulated and then immediately demonstrated as a failure mode within the same day.

## Where Else It Applies

- **Wiki** -- Wiki repo is the source of truth. Slack reports are communication, not persistence.
- **Fred** -- Google Sheets betting tracker + autostrategy repo. Fred's decisions must be logged to durable state, not just reported.
- **Mark-Lite** -- Google Sheets prospect tracker + mark-lite repo. Pipeline status, draft history, and campaign progress must persist.
- **Any agent on ephemeral infrastructure** -- Cloud functions, serverless, container-based agents all share this constraint.

## Implications

1. **Write state early and often** -- Don't batch changes for the end of a run. Commit incrementally.
2. **Branch strategy matters** -- Multiple parallel runs creating parallel branches is a failure mode. Employees should push to a stable branch (main for personal repos).
3. **Slack is communication, not storage** -- Reports posted to Slack are for Andy's awareness. The repo/tracker is the authoritative record.

## Cross-References

- [[connectors-beat-computer-use]] -- Companion principle from the same migration.
- [[scheduled-tasks-need-zero-intervention]] -- Ephemeral memory is a subtle intervention requirement (the human has to notice and recover lost state).
- [[employee-framework]] -- Framework should enforce durable state patterns.

## Sources

- Wiki ingest: "Wiki Agent Migrated to Routines + Slack Bridge Deployed" (2026-04-15)
- Real-time evidence: 2026-04-16 branch proliferation across 8+ Wiki runs
