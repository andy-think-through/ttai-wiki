# Tonic Health

> Tonic Health: UK vitamin/supplement brand. Custom AI ad creative agent build in progress -- spec evolved after 21 April client call. Days 1-2 complete, Days 3-5 remaining. No rush (Sunna).
> Last updated: 2026-04-21

## Overview
- **Company:** Tonic Nutrition Ltd (Tonic Health)
- **Shortname:** Tonic Health
- **Product(s):** Custom build (ad creative agent), potential [[knowledge-assistant]]
- **Status:** Build in progress -- Days 1-2 complete, spec redirected after client call
- **Revenue:** £1,750 invoiced (INV-005, 5 days @ £350/day). Effective day rate now ~£250/day due to scope growth (absorbed as wedge-project investment).
- **Build spend to date:** $6.57 Apify + $10.38 Anthropic = ~£13 total
- **Registered office (from July 2024):** The Courtyard, Shoreham Road, Upper Beeding, Steyning, West Sussex, BN44 3TN
- **Audience:** 1.5M+ followers across platforms, 50M+ monthly organic views; Channel 4 podcast live.

## Key Contacts
- Sunna van Kampen -- Founder/CEO -- (Personal contact; Andy's friend)
- Potential MD hire in progress -- guy who built Tails.com, was chief commercial officer at Graze, exited Tails.com to Nestle. Introduced to Sunna by Piper VC. If hired, Sunna has more bandwidth for projects like this.

## Current Status

### Build Progress
- **Day 1 (scraper + storage):** Complete. 950 reviews seeded (Tonic 500 full, Novomins 150, Vitabiotics 150, MightyKids 150). Sampling strategy: Tonic in full, competitors sampled for trending signals.
- **Day 2 (insight extraction + pillar validation):** Complete. Pillar distribution analysed. Pain taxonomy research spikes completed.
- **Days 3-5 (creative layer + integration):** Remaining. Timeline relaxed by Sunna ("no rush, side hobby").

### Spec Evolution (21 April Call)
The Sunna call on 21 April redirected the build from a pure Trustpilot review scraper toward a multi-source insight engine:
- **Data sources expanded** beyond Trustpilot to include top-of-funnel parenting forum research (Reddit, Mumsnet -- manual spikes, not scrapers)
- **Competitor set expanded:** Added Nature's Aid, Healthspan, BetterYou, Wild Nutrition, Zooki to Trustpilot scraping targets
- **Config split:** `brands.yaml` (scraper targets only, 9 DTC brands) vs `competitors.yaml` (full register with aliases for cross-source mention detection, includes retail-only brands like Bassetts, Haliborange, Sambucol, Chewy Vites with `trustpilot_scrapable: false`). Sunna: "brands are irrelevant" -- agent shouldn't exclude insights because a brand isn't on Trustpilot.
- **Creative layer reversed:** Pain taxonomy is PRIMARY input, reviews are SECONDARY. Forum language is ad-hook language; review language is landing-page language.
- **Extra days absorbed** within existing £1,750 fee as wedge-project investment. Sunna positioned this as a "playbook" for future agent builds.

### Key Findings

**Tonic pillar distribution:**
| Pillar | Share | Notes |
|--------|-------|-------|
| Proof & Conversion | 58.6% | Dominant (Tonic pays £20 Amazon voucher for reviews -> short generic "great product") |
| Clean & Differentiation | 20.2% | |
| Taste | 18.6% | |
| Guilt Reframe | 2.4% | |
| Brain & Focus | 0.2% (1 review) | DATA finding, not prompt failure. Parents don't self-report focus benefits in reviews. |

**"School" in Tonic reviews means germ-transmission context, not learning context.**

**Two standout competitor brain/focus reviews:**
1. "Son was always in trouble for talking in class... Two separate teachers have commented on the huge change in his behaviour" (Mighty Kids, confidence 0.95)
2. "Daughter has ADHD... After 1 week, daughter falls asleep within 30 minutes, stays relaxed and more focused, feels less anxious" (Novomins, confidence 0.95)

Competitors are capturing the exact language Tonic's strategy is built around -- but in competitor reviews, not Tonic's own.

**Top-of-funnel forum research findings:**
- Supplements only mentioned organically in 2 of 7 parenting pain areas (frequent illness and fussy eating)
- For sleep, focus/behaviour, neurodivergence, anxiety, fatigue -- parents don't mention supplements at all
- **"They grow out of it" is the #1 competitor** -- not another supplement brand. Most common advice in 5/7 pain areas is normalisation and patience.
- **The real buyer is the anxious parent, not the health-optimising parent.** Supplements are a "doing something" purchase driven by parental guilt, not a "fixing something" purchase driven by child symptoms.

### Decisions Made
- **Don't build Reddit/Mumsnet scrapers:** Manual research spikes delivered more value in 20 minutes than a scraper would in 6 months. Quarterly manual refresh instead.
- **Andy covers all API costs during build,** Sunna covers ongoing. Credential handover to Sunna's accounts at end of Day 4.
- **Apify upgraded to paid plan ($29/mo)** on Andy's account. Legitimate TTAI business expense.

### Technical Architecture
- **Build:** Apify (SASWAVE Trustpilot scraper, ~$2/1,000 reviews) -> Python orchestration -> Claude API (analysis + creative generation) -> Notion API (output doc) -> Slack webhook (notification). Hosted on Railway.
- **Config layer:** `config/market_psychology.yaml` (pain taxonomy with creative tiers 1-4, verbatim parent language, competitive consideration sets, blue-ocean opportunities, seasonal patterns). This is the PRIMARY creative input.
- **Pain tier system:** Tier 1 (frequent illness, fatigue/pallor), Tier 2 (picky eating/ARFID, transition dysregulation), Tier 3 (brain & focus, sleep), Tier 4 (neurodivergence, anxiety -- do not touch)
- **Creative quality bar:** Every brief must pass a "parent-as-buyer test" -- does it speak to the parent's emotional reality, or only to the child's symptoms? Brief distribution biased toward Tier 1-2. Tier 4 never generated unless Sunna explicitly requests.
- **Ongoing cost model:** No retainer. Sunna pays Apify (~£30-40/mo), Claude API (~£20/mo), hosting (~£5/mo) directly on her accounts. Andy does ad hoc fixes only.

## Interaction Log
| Date | Summary |
|------|---------|
| 2026-04-07 | Apify review scraper testing: SASWAVE pulled all 521 Tonic reviews ($1.04, 59 seconds). Amazon scrapers failed. Trustpilot validated as production-ready. |
| 2026-04-07 | Proposal sent; £1,750 (5 days @ £350) |
| 2026-04-14 | ACCEPTED. Sunna confirmed good to go on costs. |
| 2026-04-16 | INV-005 issued (£1,750). Build approved w/c 20 April. Python chosen over n8n. Two new principles captured: [[test-before-quoting]] and [[phase-it-if-dependency-fragile]]. |
| 2026-04-17 | Apify free usage exceeded ($5 limit). Upgraded to paid plan ($29/mo). |
| 2026-04-18 | Day 2 build complete. 950 reviews extracted. Pillar distribution analysed. brain_focus at 0.2% is genuine data signal. Claude Code worktree gotcha caught. |
| 2026-04-20 | INV-005 sent to Sunna. Andy made a good start on the build over the weekend. |
| 2026-04-21 | **Spec redirected after Sunna call.** Data sources expanded (forums), competitor set expanded (5 new DTC brands), creative layer reversed (pain taxonomy primary, reviews secondary). Config split (brands.yaml vs competitors.yaml). Extra days absorbed in £1,750 fee. Two forum research spikes produced the most valuable deliverable: market_psychology.yaml pain taxonomy. "They grow out of it" identified as #1 competitor. Real buyer = anxious parent, not health-optimising parent. Timeline relaxed ("no rush, side hobby"). |

## Links
- [[knowledge-assistant]] -- Product: RAG-based staff knowledge chatbot
- [[consulting]] -- Service category
- [[known-failure-modes]] -- Claude Code worktree / main-branch visibility gotcha
- [[sunna-van-kampen]] -- Key contact
- [[test-before-quoting]] -- Principle from this engagement
- [[phase-it-if-dependency-fragile]] -- Principle from this engagement
- [[research-spikes-before-scrapers]] -- Principle from this engagement

## Sources
- raw/ttai/claude.md
- raw/ttai/TTAI_Project_Context.md
- inbox/2026-04-21-ttai-tonic-build-day1-2-spec-change.md
- Gmail thread: "Platform usage exceeded" (Apify, 2026-04-17)
- Gmail thread: "Invoice - Ad Creative Agent Build (INV-005)" (2026-04-20)
- Google Calendar: "Catch up" with Sunna (2026-04-21)
