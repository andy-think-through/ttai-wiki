# Repos Are Employee Memory

> Routine sessions are ephemeral. Persistent state must live in the connected repo or external trackers, not in conversation memory.
> Last updated: 2026-04-16

## The Principle

When running AI agents on ephemeral infrastructure (Claude Code Routines, cloud functions, serverless), persistent state must be stored externally -- in GitHub repos, Google Sheets, databases, or other durable stores. The agent cannot rely on "remembering" anything between runs. Each run reconstructs context from its external state.

## Where It Was Discovered

**Wiki Agent architecture (2026-04-15):** When migrating Wiki from Cowork (which ran on Andy's Mac with local filesystem access) to Claude Code Routines (which run on Anthropic cloud), the local filesystem was no longer available. The wiki repo on GitHub became the single source of truth. Each Wiki run clones the repo, reads the current state, makes changes, commits, and pushes. No state persists between runs except what's in the repo.

## Evidence

- Wiki Agent successfully reconstructed full context from repo + Slack history on both its first scheduled run and first API follow-up (2026-04-15)
- The `log.md` file acts as the agent's memory of what it has already done -- without it, each run would re-process old information
- The `index.md` file acts as the table of contents -- without it, the agent wouldn't know what pages exist

## Where Else It Applies

| Employee | Persistent State Store | What It Holds |
|----------|----------------------|---------------|
| Wiki | GitHub repo (`ttai-wiki`) | Wiki pages, log, inbox |
| Fred | Google Sheets tracker + autostrategy repo | Bet history, P&L, model code |
| Mark-Lite | Google Sheets prospect tracker + mark-lite repo | Lead status, email history, campaign data |

- **Any future employee** -- Must have a clearly defined external state store before it can run on Routines
- **Agent Browser** -- If productised as a service, each workflow run would need external state (customer data, workflow definitions, results)

## Implications

1. **Design for cold start** -- Every run must be able to reconstruct its working context from external state alone
2. **Write state early and often** -- Don't accumulate changes in memory and write at the end. Commit incrementally so progress isn't lost if the run fails mid-way.
3. **Log what you've done** -- An append-only operations log (like `log.md`) prevents re-processing and provides an audit trail
4. **External state is the API contract** -- The format of the repo/tracker IS the employee's interface. Changes to state format affect the employee.

## Relationship to Other Principles

- Supports [[scheduled-tasks-need-zero-intervention]] -- external state means no human needs to seed context
- Complements [[connectors-beat-computer-use]] -- connectors provide the access path to external state
- Related to the Fred [[fred-decision-log]] pattern -- append-only reasoning audit trail

## Links

- [[claude-code-routines]] -- Platform where this principle applies
- [[employee-framework]] -- Universal employee model (state management section)
- [[wiki-agent-SKILL]] -- First employee proving the pattern
- [[fred-decision-log]] -- Fred's append-only audit trail

## Sources

- Wiki Agent migration session (2026-04-15)
- Routines architecture design
