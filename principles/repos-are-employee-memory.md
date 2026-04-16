# Principle: Repos Are Employee Memory

> Routine sessions are ephemeral. Persistent state must live in connected repos, trackers, or external stores -- not in conversation memory.
> Last updated: 2026-04-16

## The Principle

**GitHub repos (and other external stores) are the persistent memory layer for autonomous employees.** Each routine run starts fresh with no memory of prior runs. Everything an employee needs to reconstruct context -- wiki pages, decision logs, trackers, configuration -- must be committed to an external store that the next run can read.

## Where It Was Discovered

**Routines architecture design (2026-04-15).** When migrating Wiki from Cowork to Routines, the key architectural insight was that routine sessions are stateless. Wiki successfully reconstructed full context from the repo + Slack history on both its first scheduled run and its first API follow-up -- proving the pattern works.

## Evidence

- Wiki's first run (2026-04-15): started fresh, read `index.md` and `log.md` from the repo, fully oriented itself, processed an inbox file, updated 4 pages, appended to log -- all without any prior session memory.
- Wiki's first follow-up (API trigger): started fresh again, read the repo, answered Andy's question accurately using wiki state.
- Contrast with Cowork: Cowork sessions could accumulate context across a conversation, but this was fragile (sessions timeout, conversations get lost).

## Where Else It Applies

- **Wiki** -- `andy-think-through/ttai-wiki` repo is the memory store
- **Fred** -- Google Sheets betting tracker + autostrategy repo (once migrated)
- **Mark-Lite** -- Google Sheets prospect tracker + mark-lite repo (once migrated)
- **Any future employee** -- must have a defined persistent state store before the routine is created
- **General agent design** -- any agent that runs in ephemeral sessions needs this pattern. Applies beyond TTAI to anyone building agents on stateless infrastructure.

## Design Implications

1. **State must be committed, not just written.** If an employee writes to a file but doesn't commit/push, the next run won't see it.
2. **Read-before-write is mandatory.** Every run must read current state before making changes -- it can't assume anything from a prior run.
3. **Logs and decision trails must be append-only.** The log is the employee's continuity across runs.
4. **Trackers and indexes are the orientation mechanism.** `index.md` and `log.md` for Wiki. The tracker spreadsheet for Fred. The prospect pipeline sheet for Mark-Lite.

## Links

- [[employee-framework]] -- Universal employee operating model (references this principle)
- [[claude-code-routines]] -- The ephemeral-session platform
- [[wiki-agent-SKILL]] -- First employee to prove this pattern

## Sources

- Wiki Agent migration session (2026-04-15)
