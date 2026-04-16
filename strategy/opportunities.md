# Cross-Domain Opportunities

> First wiki-wide pattern analysis -- April 8, 2026. Updated April 16, 2026.
> Method: Read all 64 pages, identify connections that no single project folder could surface.

---

## Pattern 1: Compound Evaluation Is a General-Purpose Framework

**What the wiki says:** [[compound-evaluation]] was built for betting models — five evaluation levels (L1–L5) that catch overfitting, majority-class traps, and phantom value. It turned EFL Championship from -2.0% ROI to +2.2% ROI (and +63.5% at the highest-confidence tier).

**What hasn't been connected:** The same framework applies to every product and decision Andy makes, but only betting uses it today.

| Business Domain | L1 (Training) | L2 (Holdout) | L3 (Edge Cases) | L4 (Coherence) | L5 (Compound) |
|---|---|---|---|---|---|
| Mark-Lite Outreach | Open rate on tested emails | Reply rate on new prospect batches | Reply rate by trade segment (hard trades vs general) | Email tone/relevance audit | Conversion to meeting, weighted |
| Consulting Pipeline | Audit satisfaction score | Conversion rate to next stage (on new clients) | Performance across industry types | Methodology coherence check | Lifetime client value |
| Agent Browser | Task completion on dev tests | Completion on unseen workflows | Cross-site/cross-app robustness | Cost vs manual comparison | Value-per-dollar to client |

**Opportunity (Quick Win):** Build a lightweight compound score for Mark-Lite campaigns. The data already exists in the 5-tab tracker — open rates (L1), reply rates on new batches (L2), trade-segment splits (L3). This would let Andy know within a week whether a new postcode area is working, rather than waiting for the full 4-week sequence to play out.

**STATUS (2026-04-12):** ✅ Done. L1–L3 compound evaluation applied to both Warwickshire and Northants trackers. Key finding: 21.1% warm reply rate for site-based trades vs 0% for office-managed trades. See [[mark-lite]] campaign performance section for full results. New principle discovered: [[planning-data-serves-site-trades]].

**Opportunity (Bold):** Productise the compound evaluation framework as part of [[consulting]] methodology. When Andy audits a client's process, he could offer a "compound score" that's more rigorous than typical KPIs. This is proprietary IP (see [[dont-reveal-methodology-before-paid]]).

---

## Pattern 2: Revenue Concentration Mirrors the Majority-Class Trap

**What the wiki says:** [[majority-class-trap]] describes how 92% accuracy can hide a model that never predicts underdogs -- it just predicts the common outcome. KW Bell was 73% of invoiced revenue at first analysis (£688.20 of ~£938.20). As of April 2026, KW Bell is 22% of £3,188.20 invoiced -- de-concentration happened organically via JDW (inbound) and Tonic (friend referral) converting, not from deliberate diversification.

**What hasn't been connected:** Optimising for KW Bell's needs (OCR invoice correction, browser automation) might not generalise to other clients, just like optimising for accuracy doesn't generalise to profitable bets.

**Evidence across wiki pages:**
- [[kw-bell]] — Audit complete, solution design proposed. Revenue: confirmed.
- [[mercia-flooring]] — Setup invoiced (£250). Revenue: confirmed but small.
- [[accxel]], [[tonic-health]], [[holmes-workholding]] — All in proposal/pipeline stage. Revenue: £0 actual.

The £2,450 "in proposals" from [[overview]] is analogous to paper P&L — it looks real but hasn't been validated live.

**Opportunity (Quick Win):** Apply [[selectivity-is-everything]] to the consulting pipeline. Score each prospect on conversion probability using features that map to betting signals: referral source strength (Gareth direct referral → high confidence; cold approach → low confidence), time-to-first-response, specificity of pain point, budget signalling. Drop or deprioritise low-score prospects rather than spreading thin.

**Opportunity (Medium):** Track "invoiced revenue" and "pipeline revenue" separately — just like actual P&L vs paper P&L in [[betting-portfolio]]. Forward-only revenue tracking prevents the [[data-leakage-silent-killer]] equivalent in business forecasting.

---

## Pattern 3: Planning Portal Data Is a Hidden Platform

**What the wiki says:** [[planit-api]] documents how planning applications are searched for [[midlands-bat-surveys]] (bat survey likelihood) and [[hawks-scaffolding]] (scaffolding opportunities). Both use the same PlanIt API with different keyword filters and region IDs.

**What hasn't been connected:** Planning application data is valuable to every construction-adjacent business. The monitoring infrastructure already exists — different clients just need different filters.

**Current state:**
- Hawks: 7 council portals + PlanIt, scaffolding keywords, Warwickshire region
- Bat Surveys: PlanIt West/East Midlands, bat survey likelihood scoring
- Mercia: Schools data (DfE GIAS, not PlanIt, but same pattern)

**Opportunity (Medium):** Create a shared "Planning Intelligence" layer that all Mark clients tap into. One weekly PlanIt pull across Warwickshire + Northants + Midlands, filtered per client. This reduces API calls (rate limit is 1 req/min — currently each client burns through this independently), improves data quality (deduplication across clients), and enables Andy to sell the same underlying data to multiple non-competing trades in the same region.

**Opportunity (Bold):** "Construction Intelligence" as a standalone subscription product. Not managed outreach (Mark), just the data feed — planning applications, filtered by trade relevance, delivered weekly. Lower price point (£50–100/month), higher volume, minimal per-client work once the filters are built. [[jdw-brickwork]] discovery meeting (14 April) could be the test case: would Josh Warren pay for a weekly brickwork-relevant planning feed even without managed outreach?

---

## Pattern 4: The Autoresearch Loop Is Underdeployed

**What the wiki says:** [[autoresearch]] documents how Karpathy's "Read → Hypothesize → Modify → Evaluate → Keep/Revert → Repeat" loop was first applied to Mark-Lite v3→v4, improving lead-finding from 6.6→10.0 and outreach from 9.0→10.0.

**What hasn't been connected:** Only Mark-Lite and betting strategies have been through this loop. Consulting proposals, email templates, pricing structures, and even the wiki itself haven't been optimised this way.

**Domains where autoresearch could run today:**
- **Mark-Lite email sequences:** The A-B-C subject line rotation collects data but doesn't feed it back into a structured hypothesis → test cycle. Which subject lines win, by trade segment?
- **Consulting proposal structure:** Each proposal (AccXel, Tonic, Holmes) is written somewhat differently. Could these be structured as experiments with a consistent evaluation metric?
- **Agent Browser cost optimisation:** Per-run costs vary ($0.50–$1.69). Systematic prompt engineering experiments with cost as the evaluation metric.

**Opportunity (Quick Win):** Run one autoresearch cycle on Mark-Lite Northants email copy before the JDW Brickwork meeting. The tracker has outreach data from 39 firms across 8 trades. What patterns separate warm replies from silence?

**STATUS (2026-04-12):** ✅ Done. Full autoresearch cycle completed across both trackers. Key patterns identified: (1) All warm replies from site-based trades, (2) Email 3 (Mark introduction) is the trigger email, (3) Small owner-operator firms respond, office-managed firms don't, (4) 0/34 office-managed trades engaged. Analysis document produced for JDW meeting prep. See [[mark-lite]] campaign performance section.

---

## Pattern 5: Phantom Value in the Consulting Pipeline

**What the wiki says:** [[phantom-value]] describes how tennis grass courts show 20% edge signals but deliver -20% ROI — structural noise masquerading as opportunity. [[market-efficiency-varies-within-domain]] says edge is sub-domain specific.

**What hasn't been connected:** Some consulting prospects look promising but may be structural losers. The wiki already contains the diagnostic signals.

**Potential phantom-value prospects (stress-testing, not prescribing):**
- [[mjm-consulting]] — Engineering firm, competitive pitch against incumbent (Your Engine Room). Ned's feedback ("don't pretend to know my business") suggests misalignment. Outcome pending. This may be a structurally harder sub-domain (entrenched incumbent, sceptical buyer).
- [[holmes-workholding]] — "Proposal under review" with long-term reseller potential deliberately kept out of early comms. If the short-term engagement doesn't convert, the long-term upside is phantom.
- [[knowledge-assistant]] — "Exploring, not yet live." Viability depends on RAG quality on unstructured docs, client adoption of chat interfaces — both uncertain.

**Phantom-value filter (adapted from betting rules):**
1. Is there a specific, articulated pain point? (Equivalent of edge signal)
2. Has the prospect demonstrated willingness to pay? (Equivalent of market actually mispricing)
3. Is there an incumbent or free alternative? (Equivalent of market efficiency)
4. Is the timeline bounded? (Open-ended = leaky evaluation)

**Opportunity (Quick Win):** Run this filter on the current pipeline. Prioritise prospects that pass all four (KW Bell/AccXel referral chain, Tonic's specific agent brief, JDW inbound lead) over those that don't.

---

## Pattern 6: Mike McSweeney Is the First Multi-Product Client

**What the wiki says:** [[hawks-scaffolding]] and [[midlands-bat-surveys]] are both Mike McSweeney. Hawks is £500/month scaffolding leads. Bat Surveys is £500/month planning portal monitoring. That's £1,000/month from one person across two distinct businesses.

**What hasn't been connected:** Mike demonstrates the "land and expand" model that could replicate across the network. He started with one product (Hawks/Mark), was satisfied enough to buy a second (Bat Surveys), in a completely different domain. This is the [[consulting]] → product flywheel in action, but client-side rather than consulting-side.

**Network expansion opportunities using the same pattern:**
- [[gareth-hunt]] already referred AccXel. If AccXel converts, could Gareth's other KW Bell subsidiaries need similar automation?
- [[malcolm-freeman]] connects to multiple Midlands businesses. If IH Group converts, Malcolm's broader BNI network opens.
- [[jdw-brickwork]] is inbound from Mark-Lite — already qualified by action. If Josh converts, his trade network in Northamptonshire is a warm lead pool.

**Opportunity (Medium):** Create a "client expansion score" — after 30 days of service, assess: Does this client operate multiple businesses? Do they have a network of similar firms? Are they satisfied enough to refer? Mike scores 3/3. Systematise what happened organically.

---

## Pattern 7: The Browser Agent Is Infrastructure, Not a Product

**What the wiki says:** [[agent-browser]] is described as a product (keyword strategy, blog writing, onsite optimizer for Hike). [[browser-agent-arch]] documents the technical loop (screenshot → Claude → action → repeat).

**What hasn't been connected:** The browser agent pattern already powers or could power:
- Hike SES workflows (current)
- KW Bell invoice OCR correction (proposed)
- Mark's planning portal monitoring (currently API-based, but fallback)
- Betting odds capture (current, via Computer Use)
- Google Sheets automation (workaround for sandbox limitations)

This is a horizontal infrastructure layer, not a vertical product. Every product in the wiki touches browser automation in some way.

**Opportunity (Bold):** Position Agent Browser as TTAI's core infrastructure offering for consulting clients. Instead of selling "we'll build you a browser bot," sell "AI-powered process automation" — audit the client's repetitive browser-based workflows, automate them with the proven architecture, charge setup + monthly maintenance. This is the [[consulting]] three-stage model (Audit → Design → Implementation) with Agent Browser as the implementation engine.

**Revenue model:** £500–1,000 setup (discovery + first workflow) + £200–400/month per automated workflow. Target clients: small businesses doing repetitive data entry, form filling, monitoring — exactly the firms Mark already reaches.

---

## Pattern 8: Seasonal Arbitrage Across Revenue Streams

**What the wiki says:** Seasonal patterns are documented independently across products:
- NBA: October–June
- Tennis: Year-round (clay spring, grass summer)
- Snooker: September–May
- Schools/Mercia: January–July
- Construction/Mark: Peaks in spring/summer
- Consulting: Unknown — not tracked

**What hasn't been connected:** These seasonal curves don't all peak at the same time. There's a natural diversification benefit, but it's not being managed.

**Revenue gap periods (based on current data):**
- **July–August**: Schools break up (Mercia quiet), NBA off-season, Snooker off-season. Tennis active but grass court (phantom value). Construction slower.
- **September–October**: New seasons start (NBA, Snooker), schools return. But consulting pipeline may be quiet (budget cycles).
- **December**: Holiday period across everything.

**Opportunity (Medium):** Build a seasonal revenue calendar showing expected cash flow by month across all streams. This exposes concentration risk in specific months and identifies where a new product/client would have highest marginal value. For example, if July is the weakest month across all streams, that's when Andy should front-load consulting business development.

---

## Pattern 9: The "Removal" Principle Has Unacted Business Implications

**What the wiki says:** [[removal-as-valuable-as-addition]] — removing NBA streak dampening improved ROI by +0.7%. Exploitation loops "never remove" which is a bug, not a feature.

**What hasn't been connected:** Several wiki pages describe things that should potentially be removed or deprioritised:
- [[football-corners]] — Parked. Good decision.
- [[horse-racing]] — Concluded. Good decision.
- [[crypto]] — Paper trading, -2.36%, 25% win rate. 4-week review due ~April 24. Apply the same rigour that parked corners.
- [[knowledge-assistant]] — "Exploring, not yet live." No clients, uncertain viability. Is this a football-corners equivalent — an idea that looks promising but has irreducible randomness in adoption?
- [[darts]] — "Live but viability limited by market." Floor event coverage near-zero. Train accuracy 70.2% vs holdout 64.6% (overfit flag). Why is this still live?

**Opportunity (Quick Win):** Apply the betting decision framework to business decisions. If a product line would be "parked" under compound evaluation rules (persistent negative or near-zero ROI, insufficient market coverage, overfit to one client), park it. The time freed up has value.

---

## Pattern 10: The Wiki Itself Is Proprietary Methodology

**What the wiki says:** [[dont-reveal-methodology-before-paid]] — protect IP. High-level frameworks fine; detailed methodology stays behind paywall.

**What hasn't been connected:** The cross-domain intelligence pattern demonstrated by this wiki — where betting principles inform consulting, consulting principles inform product design, and operational learnings propagate everywhere — is itself a differentiator. No competitor is running compound evaluation on email campaigns or applying phantom-value analysis to their client pipeline.

**Opportunity (Bold):** The meta-methodology (applying quantitative decision frameworks from one domain to another) could become a core part of the [[consulting]] pitch. Not "we know AI" but "we apply rigorous evaluation frameworks that most consultants don't have." The wiki structure — interconnected, empirical, falsifiable — is the evidence base.

Andy doesn't sell the wiki. He sells decisions made better because the wiki exists.

---

## Summary: Priority Matrix

### This Week (originally set 2026-04-08; staleness flagged 2026-04-16)
1. Score consulting pipeline with selectivity filter (Pattern 5) -- **unacted 8 days**
2. Separate pipeline/invoiced revenue tracking (Pattern 2) -- **partially done**: overview.md now tracks invoiced vs proposals separately. Revenue concentration dropped from 73% to 22% organically.
3. Review darts + crypto with removal lens (Pattern 9) -- **unacted 8 days**; crypto review due 24 April, darts fill-rate test still pending
4. ~~Run Mark-Lite autoresearch on Northants email data before JDW meeting (Pattern 4)~~ ✅ Done 2026-04-12

### This Month
5. ~~Build lightweight compound evaluation for Mark-Lite campaigns (Pattern 1)~~ ✅ Done 2026-04-12 — L1–L3 applied, site-vs-office trade split discovered
6. Create shared Planning Intelligence layer for Mark clients (Pattern 3)
7. Client expansion scoring after 30 days (Pattern 6)
8. Seasonal revenue calendar (Pattern 8)

### Q2–Q3 (Bold Bets)
9. "Construction Intelligence" standalone data subscription (Pattern 3) -- **in motion**: Mark-Lite CI tier (£75/mo) added to product. Tippercrete is first CI sample recipient.
10. Agent Browser as infrastructure offering for consulting clients (Pattern 7)
11. Productise compound evaluation as consulting methodology (Pattern 1)
12. Cross-domain decision framework as TTAI's core IP (Pattern 10)

---

## Navigation
- Up: [[overview]]
- Related: [[compound-evaluation]], [[selectivity-is-everything]], [[phantom-value]], [[removal-as-valuable-as-addition]], [[autoresearch]]
- Products: [[mark]], [[mark-lite]], [[agent-browser]], [[consulting]], [[knowledge-assistant]]
- Clients: [[hawks-scaffolding]], [[midlands-bat-surveys]], [[jdw-brickwork]]
