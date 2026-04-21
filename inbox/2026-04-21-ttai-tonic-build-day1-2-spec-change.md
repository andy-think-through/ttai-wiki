# Wiki Ingest: Tonic Health Ad Agent — Days 1-2 Complete, Spec Evolved After Client Call

> Source: ttai conversation
> Date: 2026-04-21
> Packaged by: wiki-ingest skill

---

## Status Changes

- **[[tonic-health]]**: Build in progress, Days 1-2 complete, spec evolved after client call
  - Previous: Proposal sent 7 April, £1,750 quoted, awaiting response
  - Current: INV-005 issued (£1,750). Build active. Day 1 (scraper + storage) ✅. Day 2 (insight extraction + pillar validation) ✅. Spec redirected on 21 April call — data sources expanded beyond Trustpilot to include top-of-funnel parenting forum research. Days 3-5 remaining. Timeline relaxed by Sunna ("no rush, side hobby").

## Decisions

- **Absorb additional build days within existing £1,750 fee**: Scope grew after Sunna's call (Reddit/Mumsnet research, expanded competitor set, pain taxonomy). Extra days absorbed as wedge-project investment — Sunna has positioned this as a "playbook" for future agent builds.
  - Rationale: Effective day rate drops to ~£250/day but relationship value justifies it
  - Affects: [[tonic-health]], [[ttai-pricing]]

- **Don't build Reddit or Mumsnet scrapers**: Manual research spikes delivered more value in 20 minutes than a scraper would in 6 months. Quarterly manual refresh instead.
  - Rationale: Signal-to-effort ratio poor for automated scraping; forums gate access; platform changes cause scraper rot
  - Affects: [[tonic-health]]

- **Config split — brands.yaml vs competitors.yaml**: `brands.yaml` drives Trustpilot scraper targets only. `competitors.yaml` is the full competitor register with aliases for cross-source mention detection. Retail brands (Bassetts, Haliborange, Sambucol, Chewy Vites) stay in competitors.yaml with `trustpilot_scrapable: false`.
  - Rationale: Sunna said "brands are irrelevant" — agent shouldn't exclude insights because a brand isn't on Trustpilot
  - Affects: [[tonic-health]]

- **Expanded DTC competitor set**: Added Nature's Aid, Healthspan, BetterYou, Wild Nutrition, Zooki to Trustpilot scraping targets
  - Rationale: Confirmed by Sunna on call. Zooki doesn't do kids but included for general supplement psychology.
  - Affects: [[tonic-health]]

- **Creative layer uses pain taxonomy as PRIMARY input, reviews as SECONDARY**: Original spec had reviews driving creative briefs. Reversed after forum research showed top-of-funnel pain language is the ad-hook language; review language is landing-page language.
  - Rationale: Two independent research spikes (Cowork + ChatGPT) confirmed this direction
  - Affects: [[tonic-health]]

- **Andy covers all API costs during build, Sunna covers ongoing**: Apify + Anthropic on Andy's accounts during build (absorbed into £1,750). Credential handover to Sunna's accounts at end of Day 4.
  - Rationale: Simpler than getting Sunna to set up accounts mid-build
  - Affects: [[tonic-health]], [[ttai-expenses]]

- **Apify upgraded to paid plan ($29/mo)**: On Andy's account. Needed after hitting free-tier spend limit during Day 1 seeding. Legitimate TTAI business expense.
  - Affects: [[ttai-expenses]]

## New Data

- **Build spend to date**: $6.57 Apify + $10.38 Anthropic = ~£13 total
  - Context: Well within the £1,750 fee. Expected remaining: ~$5-10 for Days 3-5.
  - Affects: [[tonic-health]]

- **950 reviews seeded**: Tonic 500 (full), Novomins 150, Vitabiotics 150, MightyKids 150
  - Context: Sampling strategy — Tonic in full, competitors sampled. Competitors are for trending signals, not exhaustive mapping.
  - Affects: [[tonic-health]]

- **Tonic pillar distribution**: Brain & Focus 0.2% (1 review), Guilt Reframe 2.4%, Taste 18.6%, Clean & Differentiation 20.2%, Proof & Conversion 58.6%
  - Context: This is a DATA finding, not a prompt failure. Tonic pays for Trustpilot reviews (£20 Amazon voucher), resulting in short generic "great product" responses. Brain/focus benefits either take too long to notice or aren't articulated in review language. "School" in Tonic reviews means germ-transmission context, not learning context.
  - Affects: [[tonic-health]]

- **Two standout competitor brain/focus reviews**: (1) "Son was always in trouble for talking in class... Two separate teachers have commented on the huge change in his behaviour" (Mighty Kids, confidence 0.95). (2) "Daughter has ADHD... After 1 week, daughter falls asleep within 30 minutes, stays relaxed and more focused, feels less anxious" (Novomins, confidence 0.95).
  - Context: Competitors capturing the exact language Tonic's strategy is built around — but in competitor reviews, not Tonic's own.
  - Affects: [[tonic-health]]

- **Supplements only mentioned organically in 2 of 7 parenting pain areas**: Frequent illness and fussy eating. For sleep, focus/behaviour, neurodivergence, anxiety, fatigue — parents don't mention supplements at all in forum discussions.
  - Context: Cross-validated by two independent research spikes (Cowork + ChatGPT)
  - Affects: [[tonic-health]]

- **"They grow out of it" is the #1 competitor**: Not another supplement brand. The most common advice in 5 of 7 pain areas is normalisation and patience.
  - Context: Reframes Tonic's creative challenge — competing for action, not preference
  - Affects: [[tonic-health]]

- **The real buyer is the anxious parent, not the health-optimising parent**: Supplements are a "doing something" purchase driven by parental guilt, not a "fixing something" purchase driven by child symptoms.
  - Context: Cross-validated finding. Every high-engagement forum thread is about the PARENT breaking, not the child being ill.
  - Affects: [[tonic-health]]

## New Principles / Learnings

- **Run research spikes before building scrapers**: A 20-minute browser spike killed the Reddit scraper idea and saved 2 days of build. The pain research spike reshaped the entire creative layer. Cheap validation before expensive engineering.
  - Discovered in: Tonic ad agent build
  - Likely applies to: Any TTAI project involving external data sources
  - Evidence: Reddit spike ($0 cost, 20 mins) produced more actionable insight than a scraper would have in months. Pain research spike (2x20 mins) became the most valuable deliverable in the entire engagement.

- **Top-of-funnel pain research > review-based research for creative**: Forum language is ad-hook language; review language is landing-page language. You need both, but forums give you the emotional entry point.
  - Discovered in: Tonic ad agent build
  - Likely applies to: Any future ad creative agent builds for other clients
  - Evidence: Tonic's own 500 Trustpilot reviews had near-zero brain/focus content. Parenting forums had the exact emotional language Tonic's ads need.

- **Belt-and-braces on independent safety mechanisms**: When you have two independent safety mechanisms that don't conflict, keep both. Server-side cap + client-side cap. Belt + braces.
  - Discovered in: Vitabiotics near-miss ($70 runaway risk averted by Claude Code catching missing server-side maxReviews cap)
  - Likely applies to: All automation/agent builds with external API costs
  - Evidence: Without the client-side fallback, a future SASWAVE actor update that silently drops the maxReviews parameter would cause runaway spend.

- **Claude Code uses git worktrees**: Files exist on disk but not at the expected repo root — they're in `.claude/worktrees/{session-name}/`. Always check main branch vs worktree before declaring work "done". Merge worktree to main before closing session.
  - Discovered in: Day 2 file audit
  - Likely applies to: All Claude Code projects
  - Evidence: Day 2 analysis code appeared missing from filesystem because it was committed to a worktree branch, not main.

## Product / Methodology Changes

- **Tonic ad agent — new config layer**: `config/market_psychology.yaml` — pain taxonomy with creative tiers (tier_1 through tier_4), verbatim parent language, competitive consideration sets, blue-ocean opportunities, seasonal patterns. This is the PRIMARY input to the creative layer.
  - Detail: Pain areas tiered by creative viability: Tier 1 (frequent illness, fatigue/pallor), Tier 2 (picky eating/ARFID, transition dysregulation), Tier 3 (brain & focus, sleep), Tier 4 (neurodivergence, anxiety — do not touch)

- **Tonic ad agent — competitor config split**: `config/brands.yaml` (Trustpilot scraper targets, 9 DTC brands) vs `config/competitors.yaml` (full register with aliases for mention detection across all sources, includes retail-only brands)

- **Tonic ad agent — creative layer reframed**: Every brief must pass a "parent-as-buyer test" — does it speak to the parent's emotional reality, or only to the child's symptoms? Brief distribution biased toward Tier 1-2 pain areas. Tier 4 briefs never generated unless Sunna explicitly requests.

## New Contacts / Relationships

- **Potential Tonic MD hire**: Guy who built Tails.com and was at Graze (chief commercial officer), exited Tails.com to Nestle. Introduced to Sunna by Piper VC. Meeting Thursday. Not directly TTAI-relevant but context for Sunna's capacity — if he hires an MD, Sunna has more bandwidth for projects like this agent.
  - Linked to: [[sunna-van-kampen]], [[tonic-health]]

## Raw Context

This was a dense day. The Sunna call on the morning of 21 April redirected the build from a pure Trustpilot review scraper toward a multi-source insight engine. Two subsequent research spikes (Reddit brand-discussion, then top-of-funnel parenting pain) produced findings that are genuinely more valuable than the agent infrastructure itself. The pain taxonomy (market_psychology.yaml) is a standalone strategic deliverable that Sunna's creative team could use immediately, regardless of whether the automated agent ships. Andy's effective day rate has dropped below £350 on this engagement but the relationship value and "playbook" positioning for future Tonic agents justifies the investment. Sunna's explicit "no rush" gives headroom to get Day 3 creative layer right rather than shipping fast.

---

## Suggested Wiki Pages Affected
- [[tonic-health]] — status update (build in progress), findings, spec change, competitor set, config architecture
- [[ttai-expenses]] — Apify $29/mo upgrade, Anthropic API spend during build
- [[ttai-principles]] — new learnings (research spikes before scrapers, top-of-funnel > reviews, belt-and-braces, Claude Code worktrees)
- [[ttai-tools]] — market_psychology.yaml as a reusable pattern for future client engagements
- [NEW: claude-code-worktrees] — operational note on how Claude Code manages files via git worktrees
