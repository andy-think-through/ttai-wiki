# Wiki Ingest: Platform Knowledge Approach & Hike Proposal Scoping

> Source: agent-browser conversation
> Date: 2026-04-14
> Packaged by: wiki-ingest skill

---

## Decisions
- **Browser agent development methodology**: Shifting from workflow-first to platform-first approach ("Lego bricks")
  - Rationale: Building monolithic workflows wastes effort -- learnings from one workflow (e.g. JSON-LD textarea gotchas) get locked inside workflow-specific code and aren't reusable. Mapping platform features as building blocks first means every subsequent workflow is cheaper to build.
  - Affects: [[browser-agent]], [[hike-workflows]]

- **Three-layer architecture adopted**: Layer 1 (platform knowledge/Lego bricks) → Layer 2 (lightweight workflow templates with goal + constraints) → Layer 3 (goal-directed execution)
  - Rationale: Spectrum from fully scripted (cheap, reliable, brittle) to fully autonomous (expensive, flexible, occasionally wrong). Middle layer provides structure without rigidity. Empirical testing will determine how much structure each workflow needs.
  - Affects: [[browser-agent]], [[hike-workflows]]

- **Day 1 prioritises cost control over full agent autonomy**
  - Rationale: The v1-to-v4 optimisation journey showed that removing agent decision-making at runtime and replacing with hardcoded sequences dramatically reduces cost. Full autonomy is the end-state vision, not the starting point.
  - Affects: [[browser-agent]]

## Status Changes
- **Onsite Optimizer platform knowledge document**: Created and saved to `docs/platforms/hike/onsite-optimizer.md` in the browser-agent project
  - Previous: Platform knowledge was scattered across phase files (phase2-seo-settings.ts, phase3-schema.ts) and conversation history
  - Current: Consolidated into a single 319-line reference document covering all elements, coordinates, interaction patterns, and gotchas

- **New project directory structure**: `docs/platforms/hike/` created
  - Previous: Only `docs/prompts/` and `docs/workflows/` existed
  - Current: `docs/platforms/hike/` added for platform knowledge docs -- will expand as other Hike features are mapped

- **Bryn (Hike MD) proposal**: Requested full scope proposal for completing browser agent across all Hike features
  - Previous: No formal proposal requested
  - Current: Proposal prompt drafted and ready for a dedicated chat session

## New Principles / Learnings
- **"Map the platform, not the workflow"**: Building reusable platform knowledge first makes every subsequent workflow cheaper to build. The expensive part is Layer 1 (platform mapping). Once done, adding workflows is cheap because you're composing existing building blocks.
  - Discovered in: Browser agent / Hike automation
  - Likely applies to: Any external client platform (Evolution MX, etc.)
  - Evidence: The title/meta workflow and schema workflow both needed the same modal, same buttons, same publish flow -- but the knowledge was duplicated across separate phase files

- **Chrome MCP tools can discover but not interact with cross-origin iframe content**: Hike toolbar and modals are in a cross-origin iframe. Chrome tools can screenshot the full page but clicks don't reach through to iframe elements. Playwright-based browser agent handles this fine.
  - Discovered in: Chrome discovery session on florabhattachary.com in Onsite Optimizer
  - Likely applies to: Any SaaS platform with cross-domain editor architecture
  - Evidence: Multiple attempts to click the SEO Settings modal X button failed -- clicks landed on the overlay but didn't reach the iframe element

- **SEO Settings modal cannot be dismissed via Escape key or clicking outside**: Must click the X button. Confirmed via Chrome discovery.
  - Discovered in: Chrome discovery session
  - Likely applies to: Onsite Optimizer workflows only

## New Data
- **Sub-toolbar icons mapped (at 1470x742 viewport)**: Add Link (~55, 105), Remove Link (~117, 105), Rephrase & Optimize (~204, 105), Expand & Optimize (~268, 105), Add Image Alt Tag (~352, 105)
  - Context: Coordinates are approximate and need 1280x800 calibration via browser agent run
  - Affects: [[onsite-optimizer-platform-knowledge]]

- **AI title/meta generators**: "Choose from three SEO-friendly options" dropdown exists below BOTH the Page Title and Meta Description fields (previously only documented below title). Shows suggested text with Select button and three tone options: Enthusiastic, Standard, Professional. Agent does not use these.
  - Affects: [[onsite-optimizer-platform-knowledge]]

- **Publish modal coordinates still unmapped**: Continue button, Cancel button, and success modal X button have never been hardcoded -- agent finds them visually each run, costing an extra screenshot per publish
  - Affects: [[onsite-optimizer-platform-knowledge]]

## Product / Methodology Changes
- **Platform knowledge document structure established**: Each Hike feature gets a doc in `docs/platforms/hike/` covering: how the feature works, pre-requisite data, every UI element with coordinates, interaction patterns, field behaviours, gotchas, coordinate verification status, and how workflows compose the building blocks
  - Detail: The Onsite Optimizer doc is the reference standard -- 10 sections, 13 gotcha rules, verification status for every coordinate

- **Proposal approach for Bryn**: Two-phase framing -- Phase 1 maps entire Hike platform as building blocks, Phase 2 enables workflows as lightweight goal+constraints templates on top. Not proposing fully autonomous agent on day 1 -- cost control takes priority, with empirical testing determining how much freedom each workflow gets.
  - Detail: Prompt drafted for dedicated proposal chat session, with option for Claude to explore Hike via Chrome tools

## New Contacts / Relationships
- **Bryn**: Managing Director at Hike SEO, has requested full scope proposal for the browser agent project
  - Linked to: [[hike]]

## Raw Context
This conversation spanned two days. Day 1 focused on the conceptual shift from workflow-first to platform-first development, Chrome discovery of the Onsite Optimizer sub-toolbar icons and SEO Settings modal details, and drafting the platform knowledge document. Day 2 incorporated Andy's feedback on the document (actions panel gotcha, session setup, domain allowlist, AI generators below both fields), wrote the final version to the project, and then pivoted to scoping the proposal for Bryn. The three-layer architecture (platform knowledge → lightweight workflows → goal-directed execution) emerged from discussion about how much autonomy the agent should have vs how much structure it needs for cost control.

---

## Suggested Wiki Pages Affected
- [[browser-agent]] -- update methodology to reflect platform-first approach and three-layer architecture
- [[hike-workflows]] -- note the shift from monolithic workflows to composable building blocks
- [[hike]] -- add Bryn as MD, note proposal request
- [NEW: onsite-optimizer-platform-knowledge] -- reference the new platform knowledge document at docs/platforms/hike/onsite-optimizer.md
- [NEW: platform-knowledge-approach] -- document the Lego bricks methodology as a reusable pattern for any platform
