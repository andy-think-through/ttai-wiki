# Wiki Ingest: Wiki Agent Migrated to Routines + Slack Bridge Deployed

> Source: wiki conversation
> Date: 2026-04-15
> Packaged by: wiki-ingest skill
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
- **Routines remove Computer Use overhead**: Replacing browser automation (scanning Claude.ai conversations) with connector-based information gathering (Slack, Google Drive, wiki inbox) is faster, cheaper, and more reliable
  - Discovered in: Wiki Agent migration
  - Likely applies to: Any agent previously dependent on Computer Use for conversation scanning; Agent Browser strategy (Computer Use is a fallback, not the default path)
  - Evidence: Old Cowork version needed Min browser, 15-30 min runtime, frequent failures. Routine version completes in 5-15 min, no browser, clean tool calls.
- **Shared Slack channel enables cross-employee awareness**: Employees can read each other's reports via the Slack connector, feeding cross-domain pattern detection
  - Discovered in: Architecture design for employee routines
  - Likely applies to: All future employees; this is the architectural payoff of the #ttai-employees channel vs per-employee channels
  - Evidence: Wiki's prompt explicitly instructs it to read Fred's and Mark-Lite's Slack reports as information sources
- **Dual-mode prompt pattern is universal**: Same prompt structure (check `text` field; scheduled run if empty, follow-up if present) works for all autonomous employees
  - Discovered in: Wiki Agent restructure for routines
  - Likely applies to: Fred, Mark-Lite, and any future employee. This is the "respond to colleague" enabler.
  - Evidence: Wiki prompt handles both modes with a single branch at the top; proven end-to-end on 2026-04-15
- **GitHub repos are employee memory**: Routine sessions are ephemeral; persistent state must live in the connected repo or trackers, not in conversation memory
  - Discovered in: Routines architecture
  - Likely applies to: All three employees. Wiki -> wiki repo. Fred -> Google Sheets betting tracker + autostrategy repo. Mark-Lite -> Google Sheets prospect tracker + mark-lite repo.
  - Evidence: Each routine run starts fresh; Wiki successfully reconstructed full context from repo + Slack history on both scheduled run and API follow-up
- **Slack connector requires public channel for discovery**: Private channels not reachable by Slack MCP connector (at least on initial setup)
  - Discovered in: Wiki Agent first run (channel not findable error)
  - Likely applies to: Any agent using Slack connector
  - Evidence: Private channel initially; Wiki fell back to file report. Made channel public and invited the connector app, subsequent run succeeded.

## Product / Methodology Changes
- **Employee architecture**: Cowork scheduled tasks -> Claude Code Routines
  - Detail: Routines run on Anthropic cloud infrastructure. Three trigger types: schedule, API, GitHub events. Employees use schedule + API triggers. Daily run cap per account applies.
- **Reporting channel**: Email -> Slack #ttai-employees
  - Detail: All employee reports post to the same channel. Andy monitors one feed. Thread-based replies trigger follow-up runs via the Slack bridge.
- **Bridge infrastructure (new)**: TTAI Slack Bridge
  - Detail: Node.js Slack Bolt app using Socket Mode (no public URL required). Listens for Andy's messages in #ttai-employees, identifies target employee by name prefix or thread context, fires the correct routine's /fire endpoint with message as `text` field. Deployed on Railway free tier. Auto-deploys from GitHub on push.

## Action Items Completed
- Wiki migrated to GitHub (`andy-think-through/ttai-wiki`)
- Slack workspace and #ttai-employees channel created
- Wiki Agent routine deployed with schedule + API triggers
- Slack bridge bot built, configured, and deployed to Railway
- End-to-end loop proven: scheduled run posts to Slack; curl to API endpoint triggers follow-up that responds in Slack

## Raw Context

This session migrated the first autonomous employee (Wiki) from Cowork scheduled tasks to Claude Code Routines, set up the supporting infrastructure (GitHub repo for the wiki, Slack workspace, bridge bot on Railway), and proved the full interaction loop works end-to-end. The architectural pattern is now established: routine posts to Slack on schedule, Andy replies in Slack, bridge bot fires the routine's API endpoint with the reply as input, routine runs in follow-up mode and responds in Slack.

Fred and Mark-Lite have not yet been migrated -- they still exist as Cowork scheduled task SKILL files and need restructuring to the dual-mode routine prompt pattern. Once migrated, their API endpoints and tokens get added to the bridge bot's env vars and they join the same #ttai-employees channel.

The wiki-ingest skill (used across all Claude projects) needs updating. It currently writes to the local filesystem path. Going forward it should commit to the wiki repo's `inbox/` folder so Wiki Agent picks up ingests automatically on its next cloud run. This is a skill-level change, not something the wiki project can do on its own.

---

## Suggested Wiki Pages Affected
- [[operations/wiki-agent-SKILL]] -- Rewrite to reflect Routines architecture. Remove Computer Use scanning. Add dual-mode prompt pattern. Change reporting from email to Slack. Update file paths from local to repo-relative.
- [[operations/fred-autostrategy-employee-SKILL]] -- Flag for migration. Still Cowork-based.
- [[operations/mark-lite-employee-SKILL]] -- Flag for migration. Still Cowork-based.
- [[operations/employee-framework]] -- Update to reflect: Routines as platform, Slack as reporting channel, dual-mode prompt pattern as universal, GitHub repos as employee memory.
- [[operations/cowork-pipeline]] -- Add note that Cowork is being phased out for scheduled employees in favour of Routines. Still valid for on-demand batch work.
- [NEW: operations/ttai-slack-bridge] -- New infrastructure page. Node.js Slack Bolt app on Railway. Routes Slack replies to routine API endpoints. Repo location, env vars, deployment notes.
- [NEW: operations/claude-code-routines] -- New platform page. Three trigger types, API format, daily limits, how employees use them. The infrastructure layer beneath employee SKILL files.
- [[strategy/overview]] -- Update infrastructure notes. Autonomous employees now running on Routines + Slack, not Cowork + email.
- [[clients/mercia-flooring]] -- Note: go-live date slipped past 2026-04-15. Needs fresh date. OAuth blocker still outstanding.
- [[betting-rules/predicted-loser-rule]] -- Current record 18/18 (verified via Wiki scan). Decision still pending: formalise now or wait for 20.
