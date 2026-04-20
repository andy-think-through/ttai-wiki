# Wiki Ingest: Slack Bridge self-fire fix + Routines UI / Wiki ingestion learnings

> Source: ttai conversation (Cowork debugging session)
> Date: 2026-04-16
> Packaged by: wiki-ingest skill

---

## Status Changes
- **[[ttai-slack-bridge]]**: Self-fire loop fixed in production.
  - Previous: Wiki running hourly on 2026-04-16 (runs list showed 20:30, 20:51, 20:58, 21:10, 22:10 — all API-triggered by the bridge firing on Wiki's own "WIKI --" reports).
  - Current: Patched `index.js` deployed via GitHub → Railway auto-deploy. Confirmed working: manual test message posted in #ttai-employees produced one `WIKI --` reply, no cascade.

## Decisions
- **Push-to-main branch behaviour**: Not modifying Wiki / Mark-Lite prompts yet to force push-to-main.
  - Rationale: Wiki told Andy in its last session it would push to main going forward — likely written into an in-repo config (CLAUDE.md or similar). Observing whether that holds before editing system prompts.
  - Affects: [[ttai-slack-bridge]], [[agent-wiki]], [[agent-mark-lite]]
- **Deploy route for bridge fixes**: GitHub web-edit → Railway auto-deploy (rather than local dev + push).
  - Rationale: Fastest path for a two-hunk patch; avoids cloning / local toolchain.
  - Affects: [[ttai-slack-bridge]]

## New Data
- **Trigger IDs (for reference)**:
  - Wiki: `trig_014KqtfjDFehYrvoweuXf7jp`
  - Mark-Lite: `trig_01JYyxdQy3GUKNCHCFPeCQZ7`
- **Bridge hosting**: Runs on **Railway**, not Vercel. Correcting any prior notes that said Vercel.
- **Slack IDs**:
  - Channel #ttai-employees: `C0AT4K9KJFQ`
  - Andy's user ID: `U0AT38SDPKP`

## New Principles / Learnings
- **Agents post as the human via user OAuth token**: When an agent posts to Slack using the user's own OAuth token, a `message.user !== ANDY_USER_ID` filter in a bridge is insufficient — the agent's posts pass the filter. A content-pattern filter (e.g. `^NAME --` matching the agent's own report prefix) is required to exclude self-posts and prevent self-fire loops.
  - Discovered in: ttai-slack-bridge debugging
  - Likely applies to: any future agent-to-Slack bridge, any automation where an agent authenticates as the human
  - Evidence: Wiki looped ~14 times on 2026-04-16 because the bridge re-fired Wiki on every "WIKI --" report Wiki itself posted.
- **Routines UI has no branch config toggle**: The Edit-routine dialog on claude.ai/code/routines exposes only: prompt, model, repo list, triggers, connectors, and cloud environments (Default / custom). Per-run `claude/<name>` branches are Claude Code's default feature-branch-per-session behaviour, not a routine-level setting. The only lever to force push-to-main is instructions inside the prompt.
  - Discovered in: investigating Wiki / Mark-Lite branch proliferation
  - Likely applies to: all future Routines-based agents that touch a GitHub repo
  - Evidence: Verified by reading the full Edit-routine dialog structure and grepping the Wiki prompt — zero mentions of `branch`, `main`, `push`, or `PR`.
- **Cowork → Routines migration changed Wiki's input model**: Wiki no longer scrapes claude.ai (the old computer-use loop is gone). It reads from two sources only: (1) the `inbox/` folder in the ttai-wiki repo (populated by the `wiki-ingest` skill in other Claude projects), (2) recent #ttai-employees Slack messages from Fred and Mark-Lite. Conversations where Andy doesn't explicitly say "wiki ingest" don't reach the wiki.
  - Discovered in: follow-up question about Wiki's info sources
  - Likely applies to: Andy's decisions about which conversations need active ingestion; any future attempt to expand Wiki's input sources
  - Evidence: Wiki's own system prompt under "Differences From the Old Cowork Version" states "Gets information from wiki inbox + Slack messages -- no browser automation needed."

## Product / Methodology Changes
- **TTAI Slack Bridge v2 (`index.js`)**: Two changes committed to `main` on `andy-think-through/ttai-slack-bridge`:
  - Detail (guard): Added `AGENT_REPORT_PATTERN = /^(wiki|fred|mark-?lite)\s*--/i` test in the message listener. Any message from Andy's user whose text matches the pattern is skipped with a log line — prevents agents triggering themselves on their own Slack reports.
  - Detail (logging): `fireRoutine()` now logs non-2xx responses loudly with status, body excerpt, and a redacted fire URL (`trig_01AB…/fire`). Added `redactFireUrl()` helper. Previously, silent 404s from a wrong FIRE_URL could bite us unnoticed.
- **Wiki input methodology (informational)**: Any chat containing wiki-worthy material requires an explicit "wiki ingest" invocation. No passive ingestion exists. Worth being conscious of in longer sessions.

## Action Items Completed
- Bridge patch committed + deployed
- Self-fire guard verified in production via manual test message
- Root cause of Wiki's hourly loop on 2026-04-16 diagnosed and resolved

## Raw Context

This was a two-session debugging effort (the first hit a context limit before the fix landed). Core misdiagnosis in the handoff: the earlier Claude suggested the bridge "double-fires on every message". Actual bug: bridge correctly filters by user, but agents post via Andy's user OAuth token so they pass the filter, then match the employee-name prefix pattern and re-fire. Guard is now pattern-based exclusion of agent-report prefixes, which is the right layer.

Two open items flagged but not resolved here: (1) Wiki's prompt says every-other-day cadence but the runs list showed hourly runs today — probably all self-fire loop runs rather than a mis-set schedule, but worth confirming. (2) Wiki itself flagged that `overview.md` still references a 15 April Mercia go-live that's now past — awaiting Andy's call on how to update.

---

## Suggested Wiki Pages Affected
- [[ttai-slack-bridge]] — add self-fire guard + non-2xx logging as current architecture; note Railway (not Vercel) hosting; record trigger IDs
- [[agent-wiki]] — note branch behaviour status (pushing to main via in-repo note, not via prompt instructions); confirm every-other-day cadence is actually set
- [[agent-mark-lite]] — same branch-behaviour caveat applies
- [[routines-platform]] or [NEW: routines-platform] — record UI limitations: no branch config, only prompt / model / repo / triggers / connectors / cloud envs
- [[principles]] — add "agents post as the human via user OAuth token" as a reusable principle
- [[wiki-ingestion-model]] or [NEW: wiki-ingestion-model] — document the inbox + Slack input model and its "explicit-ingest-required" trade-off
