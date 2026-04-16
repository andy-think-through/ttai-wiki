# Wiki Ingest: Wiki Agent Migrated to Routines + Slack Bridge Deployed

> Source: wiki conversation
> Date: 2026-04-15
> Packaged by: wiki-ingest skill
> Processed by: Wiki Agent 2026-04-16
---

## Status Changes
- **Wiki repository**: Now lives on GitHub
  - Previous: Local-only at `/Users/andyallen/Documents/Claude/Projects/Think Through AI/wiki/`
  - Current: `github.com/andy-think-through/ttai-wiki` (private). Local copy still exists but GitHub is source of truth.
- **[[operations/wiki-agent-SKILL]]**: Migrated from Cowork scheduled task to Claude Code Routine
  - Previous: Cowork scheduled task using Computer Use (Min browser) to scan Claude.ai conversations
  - Current: Claude Code Routine running on Anthropic cloud, reads wiki repo + Slack messages + inbox folder
- **Slack workspace**: Created (new)
  - Workspace: "Think Through AI"
  - Channel: #ttai-employees (ID: C0AT4K9KJFQ, public)
- **TTAI Slack Bridge**: Deployed (new infrastructure)
  - Node.js Slack Bolt app running on Railway free tier
  - Repo: separate GitHub repo, auto-deploys on push
  - Purpose: routes Andy's Slack replies to the correct employee routine API endpoint

## Decisions
- **Autonomous employee platform**: Adopted Claude Code Routines
  - Rationale: Supports API triggers (enables two-way interaction), runs on cloud (no laptop dependency), removes Computer Use overhead
  - Affects: [[operations/wiki-agent-SKILL]], [[operations/fred-autostrategy-employee-SKILL]], [[operations/mark-lite-employee-SKILL]], [[operations/employee-framework]]
- **Reporting channel**: Slack #ttai-employees replaces email
  - Rationale: Single monitoring surface, enables replies, enables cross-employee visibility
  - Affects: All three employee SKILL files
- **Dual-mode prompt pattern**: Scheduled run vs follow-up based on API `text` field presence
  - Rationale: Same prompt handles both the scheduled daily work and reactive follow-up queries
  - Affects: [[operations/employee-framework]]
- **Wiki Agent branch permissions**: Allowed unrestricted branch pushes (pushes direct to main)
  - Rationale: Personal wiki repo, not shared codebase. Git history is the audit trail.
  - Affects: [[operations/wiki-agent-SKILL]]
- **Ingest file destination**: Going forward, wiki-ingest skill should commit to the GitHub repo's `inbox/` folder rather than local filesystem
  - Rationale: Wiki Agent runs on cloud and clones the repo; it can only see files committed to the repo
  - Affects: `wiki-ingest` user skill (requires update in Andy's skill config)

## New Data
- **Wiki Agent first run (2026-04-15)**: 1 inbox file moved to inbox/processed/, 4 pages aligned (predicted-loser rule data to NBA 18/18 authoritative figure), log.md entry appended
- **Wiki Agent runtime**: Approximately 5-15 minutes per run (down from 15-30 min for Cowork version)
- **Predicted-loser rule current record**: 18/18 across live domains (NBA 8/8, Tennis 10/10) as of 2026-04-15 scan
- **Open questions flagged by Wiki first run**:
  1. Formalise predicted-loser rule at 18/18 or wait for 20?
  2. Mercia go-live (planned 15 April) has slipped -- overview.md "Must-Hit" needs rewrite
  3. Fred last reported 2026-04-13 -- still operating?
  4. Slack connector now live for Wiki (resolved)

## New Principles / Learnings
- **Connectors beat Computer Use**: Replacing browser automation with connector-based information gathering is faster, cheaper, and more reliable
- **Shared Slack channel enables cross-employee awareness**: Employees can read each other's reports via the Slack connector
- **Dual-mode prompt pattern is universal**: Same prompt structure works for all autonomous employees
- **GitHub repos are employee memory**: Routine sessions are ephemeral; persistent state must live in the connected repo
- **Slack connector requires public channel for discovery**: Private channels not reachable by Slack MCP connector on initial setup

## Action Items Completed
- Wiki migrated to GitHub (`andy-think-through/ttai-wiki`)
- Slack workspace and #ttai-employees channel created
- Wiki Agent routine deployed with schedule + API triggers
- Slack bridge bot built, configured, and deployed to Railway
- End-to-end loop proven: scheduled run posts to Slack; curl to API endpoint triggers follow-up that responds in Slack
