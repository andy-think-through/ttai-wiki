# Wiki Ingest: Mark-Lite v2 Prompt, Org Chart Planning, Context-Gathering Fix

> Source: wiki project conversation
> Date: 2026-04-21
> Packaged by: wiki-ingest skill

---

## Status Changes
- **[[products/mark-lite]]**: Routine prompt v2 completed with safety feedback applied. Drafts-only launch mode. Not yet deployed -- awaiting context-gathering fix first.
  - Previous: v1 prompt drafted (2026-04-15), missing safety controls
  - Current: v2 prompt with trust ladder, kill switch, experiment gating, Mode 2 classification, tracker schema lockdown, removal floor rule
- **ttai-mark-lite GitHub repo**: Created with full file structure
  - Files: prompt.md, context.md, principles.md, tracker-schema.md, decision-log.md, .gitignore, README.md, plus reports/, campaigns/, templates/ folders
- **Fred migration**: Deferred
  - Previous: Planned as next after Wiki
  - Current: Deferred due to heavy local dependencies (Python model scripts on Mac, Betfair browser automation, crypto VPS SSH access). Mark-Lite prioritised instead.
- **Google Calendar connector**: Added to both Wiki and Mark-Lite routines
  - Previous: Not connected
  - Current: Connected, awaiting prompt updates to use it

## Decisions
- **Mark-Lite trust ladder**: Drafts-only for minimum 14 days, 20 reviewed drafts, 90% approval rate, explicit GRADUATE MARK-LITE TO SEND MODE command required. Certain categories (re-engagement, prospects Andy has spoken to, adapted copy, warm-reply prospects) stay drafts-only permanently.
  - Rationale: Cost of an ill-timed email to a live prospect (e.g. Danny Fordham) is higher than friction of approving drafts for two weeks
  - Affects: [[products/mark-lite]], [[operations/mark-lite-employee-SKILL]], [[operations/employee-framework]]
- **Experiments permanently approval-gated**: Mark-Lite proposes experiments in Slack, Andy approves before any run on live outreach. This never relaxes, even after graduation.
  - Rationale: A bad A/B test on live prospects tanks reply rates and burns relationships
  - Affects: [[operations/mark-lite-employee-SKILL]], [[operations/employee-framework]]
- **Kill switch added**: PAUSE MARK-LITE / RESUME MARK-LITE as exact Slack commands. Halts all activity immediately.
  - Affects: [[operations/mark-lite-employee-SKILL]]
- **Removal floor rule**: Min 10 prospects contacted AND 21 days of data AND clear zero-response pattern before parking a segment. Prevents pruning on noise.
  - Affects: [[principles/removal-as-valuable-as-addition]]
- **Tracker schema immutable**: tracker-schema.md documents canonical Google Sheets structure. Mark-Lite cannot add/rename columns or tabs. Mismatch = stop and escalate.
  - Affects: [[operations/mark-lite-employee-SKILL]]
- **Context-gathering fix before split-brain**: Remote routines will be made smarter at pulling context from connectors (Calendar, Gmail, Slack history, wiki) before considering a split-brain (local task + remote routine) architecture.
  - Rationale: Simpler fix first. Split-brain doubles the task count and adds complexity. Try the easy path before the hard path.
  - Affects: All employee SKILL files
- **Future employees planned**: Karen (PA/finance) and Cord (manager/coordinator) added to org chart. Not being built yet.
  - Affects: [[operations/employee-framework]], [[strategy/overview]]

## New Data
- **Local Desktop scheduled tasks**: Confirmed schedule-only triggers. No API or GitHub event triggers available.
- **Remote routines**: Confirmed schedule + API + GitHub event triggers, but no local file access (fresh clone only).
- **Mark-Lite prompt v2**: ~19KB covering trust ladder, Mode 2 classification, draft review format, warm reply 48-hour nudge, tracker schema lockdown.
- **Org chart**: 5 planned employees total -- Wiki, Fred, Mark-Lite, Karen (PA/finance), Cord (manager).

## New Principles / Learnings
- **Trust ladder over binary trust**: Don't give full autonomy after one good run. Graduate through stages: drafts-only -> standard sends -> novel situations still drafts-only. Applies to any employee that communicates with external humans.
  - Discovered in: Mark-Lite v2 safety review
  - Likely applies to: Any future employee with external-facing communication (Karen's invoicing emails, Cord's client updates if ever applicable)
  - Evidence: External safety review flagged that v1's "first run drafts, second run sends" model was too aggressive for an agent talking to real prospects with money on the line
- **Mode 2 classification prevents over-action**: Classify every inbound Slack message before acting -- acknowledgement, command, question, instruction, draft feedback, ambiguous. Acknowledgements get "Noted." and stop. Ambiguous triggers a clarifying question, not a guess.
  - Discovered in: Mark-Lite v2 safety review
  - Likely applies to: All employees with Slack interaction. Universal pattern for the dual-mode prompt.
  - Evidence: Original prompt treated every Slack message as an instruction. "Nice work" would have triggered Mark-Lite to try to DO something.
- **Experiments permanently approval-gated**: The cost of a bad experiment on live prospects outweighs the friction of asking first. This is not a trust-ladder item that graduates -- it stays manual forever.
  - Discovered in: Mark-Lite v2 safety review
  - Likely applies to: Any employee running experiments that affect real humans or real money
  - Evidence: "Run experiments on live outreach" autonomy on day one means Mark-Lite could A/B test subject lines on Danny Fordham before we know it classifies replies correctly
- **"Communications officer" framing for remote routines**: Remote routine's job is not to execute campaigns but to report, answer questions, receive strategic input, and bridge context. Execution stays with the local task (if split-brain is needed) or is gated through approval (if single-brain with better context).
  - Discovered in: Architecture discussion about local vs remote trade-offs
  - Likely applies to: All employees. Reframes what "autonomous employee" means in a remote-only setup.
  - Evidence: Mark-Lite routine didn't know about Josh Warren meeting because it lacked calendar access. The fix is better context gathering, not local execution.
- **Context gathering before architecture change**: Make routines smarter at pulling from available connectors before adding the complexity of split-brain architecture. Simple fix first, complex fix only if simple fails.
  - Discovered in: Discussion of local vs remote limitations
  - Likely applies to: Any architectural decision where there's a simple and complex option. Try simple first.

## Product / Methodology Changes
- **Employee org chart expanded to 5**: Wiki, Fred, Mark-Lite, Karen (PA/finance), Cord (manager)
  - Karen: manages email, calendar, Drive. No local file access. Scheduling, invoicing follow-ups, admin tasks. Can operate exclusively through cloud connectors.
  - Cord: manager layer. Reads all employee reports in Slack, coordinates between employees, can fire other employees' routines via API, bridges context between Slack and Claude.ai project conversations. New architectural pattern -- manager above peer employees.
- **Mark-Lite safety framework**: Trust ladder, kill switch, experiment gating, Mode 2 classification, tracker schema lockdown, removal floor, draft review format, warm reply 48-hour nudge. This framework is reusable for any employee with external-facing communication.

## Raw Context

This session (April 16-21) completed the Mark-Lite v2 prompt with comprehensive safety controls following an external review, created the ttai-mark-lite GitHub repo, confirmed local-vs-remote trigger limitations, decided on a "better context gathering" fix over split-brain architecture, and began early org chart planning for two future employees (Karen, Cord). A handoff prompt was created for the next session to implement context-gathering updates to Wiki and Mark-Lite routine prompts (adding Google Calendar reading, deeper Gmail scanning, Slack history reading at start of each run). The org chart expansion is early-stage and not yet being actioned.

---

## Suggested Wiki Pages Affected
- [[operations/mark-lite-employee-SKILL]] -- Major rewrite needed to reflect v2 prompt (trust ladder, kill switch, experiment gating, Mode 2 classification, tracker schema). Current page reflects Cowork version.
- [[operations/employee-framework]] -- Add: trust ladder pattern, Mode 2 classification as universal, experiment gating principle, kill switch as standard, removal floor rule. Add Platform section update for context-gathering approach.
- [[principles/removal-as-valuable-as-addition]] -- Add removal floor rule (min 10 prospects, 21 days) as a boundary condition.
- [[strategy/overview]] -- Update org chart section: 5 planned employees. Note Karen and Cord as planned-not-built.
- [NEW: operations/mark-lite-tracker-schema] -- Canonical tracker structure for Mark-Lite's Google Sheets. Schema immutability rule.
- [NEW: principles/trust-ladder-over-binary-trust] -- Graduated autonomy for external-facing employees. Origin: Mark-Lite v2 safety review.
- [NEW: principles/classify-before-acting] -- Mode 2 classification pattern. Prevents over-action on ambiguous input.
- [[products/mark-lite]] -- Update status: v2 prompt complete, repo created, awaiting context-gathering fix before deployment.
