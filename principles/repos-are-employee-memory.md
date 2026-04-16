# Repos Are Employee Memory

> Routine sessions are ephemeral. Persistent state must live in connected repos, trackers, or external tools -- not in conversation memory. If it isn't committed, it didn't happen.
> Last updated: 2026-04-16

## The Principle

AI employees running on ephemeral infrastructure (Claude Code Routines, cloud functions, etc.) start every session fresh. They have no memory of prior runs. All persistent state -- wiki pages, tracker updates, decision logs, reports -- must be written to durable storage (GitHub repos, Google Sheets, databases) during the run, not assumed to carry forward.

## Where It Was Discovered

**Routines architecture design (2026-04-15).** When migrating Wiki Agent from Cowork (which had implicit session continuity) to Routines (ephemeral), the architectural requirement became explicit: every run must reconstruct its context from the repo and external tools, then write its changes back before the session ends.

## Evidence

**2026-04-16 branch proliferation incident.** 8+ Wiki runs posted Slack reports claiming "5 pages created, 7 updated" -- but each run committed to a different ephemeral branch. When the next run started, it found the repo unchanged because it was on a fresh branch starting from main. The work existed briefly in each session's working copy but was never merged to a durable location. The Slack messages were accurate descriptions of intent but the repo was the source of truth, and the repo showed nothing changed.

This is the strongest possible real-time validation of the principle: it failed, visibly, within hours of being articulated.

## Where Else It Applies

- **Wiki:** GitHub repo `andy-think-through/ttai-wiki` is the source of truth. Pages, index, log -- all committed.
- **Fred:** Google Sheets betting tracker + autostrategy repo. P&L, rules, decision log must be written to Sheets or repo each run.
- **Mark-Lite:** Google Sheets prospect tracker + mark-lite repo. Prospect status, outreach log, draft approvals.
- **Any future employee:** Design the state persistence layer before writing the prompt. Ask: "If this session crashes after posting to Slack but before committing, what's lost?"

## Corollary: Write State Early and Often

Don't batch all writes to the end of a run. If the session times out or errors partway through, partial state is better than no state. Commit after each logical unit of work, not once at the end.

## Links

- [[employee-framework]] -- Universal employee operating model
- [[claude-code-routines]] -- Platform where this principle is critical
- [[wiki-agent-SKILL]] -- First employee designed with this principle
- [[scheduled-tasks-need-zero-intervention]] -- Related: both are about autonomous operation resilience

## Sources

- Routines architecture design session (2026-04-15)
- 2026-04-16 branch proliferation incident (real-time evidence)
- Andy's Slack ingest message (2026-04-16)
