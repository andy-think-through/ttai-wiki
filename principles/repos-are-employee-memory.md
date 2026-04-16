# Repos Are Employee Memory

> Routine sessions are ephemeral. Persistent state must live in connected repos, trackers, or external stores -- not in conversation memory.
> Last updated: 2026-04-16

## The Principle

When running autonomous employees on ephemeral infrastructure (Claude Code Routines, or any session-based agent platform), all state that needs to survive between runs must be externalised. The agent has no memory of previous runs. Its "memory" is the repo it clones, the Slack messages it reads, and the trackers it queries.

## Where It Was Discovered

**Wiki Agent migration (2026-04-15).** Each Routines session starts fresh -- no conversation history, no prior context. Wiki successfully reconstructed full context from the GitHub repo + Slack history on both its first scheduled run and its first API follow-up. The repo serves as the Wiki's long-term memory.

## Where Else It Applies

| Employee | Memory Store | What It Contains |
|----------|-------------|-----------------|
| Wiki | ttai-wiki GitHub repo | All wiki pages, log.md, inbox/ |
| Fred | Google Sheets betting tracker + autostrategy repo | P&L, bet history, model artefacts, decision log |
| Mark-Lite | Google Sheets prospect tracker + mark-lite repo | Prospect status, email history, campaign data |

This also applies to any future employee or agent product Andy builds. If a client asks "can you build us an AI employee?", the architecture answer includes: "its memory lives in your existing systems (spreadsheets, repos, CRMs), not in a proprietary database."

## Design Implications

1. **Read state first:** Every run should start by reading its state stores to reconstruct context.
2. **Write state explicitly:** Every change must be committed/saved to the external store before the session ends.
3. **State stores must be structured:** Unstructured conversation logs are hard to reconstruct from. Structured pages (wiki), structured rows (sheets), and structured commits (git) work.
4. **Idempotent operations:** Since the agent doesn't remember what it did last time, operations should be safe to re-run.

## Relationship to Other Principles

- [[connectors-beat-computer-use]] -- Connectors are how the agent reads its memory stores. If state lives in Google Sheets but the agent can only reach it via Computer Use, the architecture is fragile.
- [[scheduled-tasks-need-zero-intervention]] -- Reliable memory stores enable zero-intervention operation. If the agent can't reconstruct its context, it can't run autonomously.

## Links

- [[employee-framework]] -- All employees inherit this architecture
- [[claude-code-routines]] -- Platform that makes this principle necessary
- [[wiki-agent-SKILL]] -- Primary evidence source
- [[connectors-beat-computer-use]] -- Complementary principle

## Sources

- Wiki Agent migration session (2026-04-15)
- Wiki ingest file: "Wiki Agent Migrated to Routines + Slack Bridge Deployed"
