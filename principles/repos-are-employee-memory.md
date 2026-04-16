# Principle: Repos Are Employee Memory

> On ephemeral infrastructure, persistent state must live in connected repositories or external stores -- not in conversation memory. Each routine run starts fresh; the repo is the memory.
> Last updated: 2026-04-16

## The Principle

When autonomous agents run on ephemeral infrastructure (Claude Code Routines, serverless functions, container-based sessions), they have no built-in memory between runs. All persistent state -- knowledge, status, decision history, operational data -- must be externalised to durable stores that the agent reads at the start of each run.

For TTAI employees, the primary memory stores are:
- **GitHub repos** -- Wiki pages, code, config files, logs
- **Google Sheets** -- Trackers, campaign data, P&L records
- **Slack message history** -- Recent reports, conversations, colleague updates

## Where It Was Discovered

**Routines architecture design (2026-04-15):** When migrating Wiki from Cowork (which ran on Andy's Mac with filesystem persistence) to Claude Code Routines (ephemeral cloud sessions), the key architectural question was: "Where does Wiki's memory live?" The answer: the GitHub repo. Wiki clones the repo, reads index.md and log.md to understand current state, does its work, commits changes, and pushes. The next run clones again and sees the updated state.

## Evidence

- Wiki Agent successfully reconstructed full operational context from repo + Slack on its first Routines run (2026-04-15) -- no prior conversation memory needed
- Follow-up API triggers (Andy's Slack replies) also worked: Wiki read the repo state, answered the question, and posted to Slack -- all without any memory of the scheduled run that happened earlier

## Where Else It Applies

| Employee | Memory Store | What's Stored |
|----------|-------------|---------------|
| **Wiki** | `ttai-wiki` GitHub repo | Wiki pages, index, log, inbox |
| **Fred** | Google Sheets tracker + autostrategy repo | P&L data, model params, decision log |
| **Mark-Lite** | Google Sheets tracker + mark-lite repo | Prospect data, campaign status, outreach history |

- **Any future employee:** The pattern is universal. Define the memory store before writing the SKILL.md.
- **Client agent architectures:** When advising clients on building autonomous agents, this is a key design constraint. "Where does your agent's memory live?" is a first-order question.

## Relationship to Other Principles

- Complements [[connectors-beat-computer-use]] -- connectors are how agents read/write their memory stores
- Supports [[scheduled-tasks-need-zero-intervention]] -- if the agent's memory is external and durable, there's no risk of losing state due to session failures

## Exceptions

- Agents with built-in persistent memory (e.g., conversation-based assistants with context windows that span sessions) -- but even these benefit from externalised state for durability
- Very short-lived agents where a single session handles the full lifecycle

## Sources

- Wiki Agent migration conversation (2026-04-15)
- Ingest file: 2026-04-16-wiki-agent-migration-routines-slack-bridge.md
