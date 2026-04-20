# Wiki Operations Log

> Append-only chronological record of all wiki operations.

---

## 2026-04-08 setup | Initial scaffolding
- Source: wiki-schema-CLAUDE.md (uploaded by Andy)
- Pages created: index.md, log.md, SCHEMA.md
- Pages updated: none
- Key new information: Wiki folder structure created. Schema defines architecture, page types, cross-referencing rules, and 6-phase ingest plan. Awaiting raw source documents from Claude.ai project folders.

## 2026-04-08 ingest | Phase 1 — TTAI Business Foundation
- Sources: raw/ttai/claude.md, raw/ttai/TTAI_Project_Context.md, raw/ttai/TTAI_Project_Instructions.md
- Pages created:
  - products/consulting.md, products/mark.md, products/hike-ses.md, products/knowledge-assistant.md
  - clients/kw-bell.md, clients/accxel.md, clients/mercia-flooring.md, clients/holmes-workholding.md, clients/mjm-consulting.md, clients/ih-group.md, clients/tonic-health.md, clients/carmen-macdougall.md
  - people/malcolm-freeman.md, people/gareth-hunt.md, people/sunna-van-kampen.md, people/bryn.md
  - principles/dont-reveal-methodology-before-paid.md, principles/position-next-stage-not-bigger-commitment.md, principles/let-clients-surface-pain-points.md, principles/email-quality-over-volume.md, principles/_index.md
- Pages updated: index.md
- Key new information: Full business context ingested — 4 products, 8 clients/prospects, 4 key people, 4 cross-cutting principles. Revenue tracked: £688.20 (KW Bell) + £250 (Mercia) invoiced, ~£3,150 in active proposals (AccXel £700, Tonic £1,750, Holmes ~£450 setup). Referral network mapped: Malcolm Freeman is the key connector (IH Group, Carmen). Gareth Hunt is the first client and AccXel referrer.

## 2026-04-08 ingest | Phase 2 — AutoStrategy Methodology & Domains
- Sources: raw/autostrategy/AutoStrategy_Paper_v6.md, raw/autostrategy/AutoStrategy_SKILL_v3.md, raw/autostrategy/autostrategy_STATUS.md, raw/autostrategy/daily-skill-lessons-learned.md
- Pages created:
  - methodologies/autostrategy.md, methodologies/autoresearch.md, methodologies/compound-evaluation.md, methodologies/results-diagnostic.md, methodologies/walk-forward-validation.md, methodologies/probability-calibration.md
  - domains/nba.md, domains/tennis-atp.md, domains/snooker.md, domains/darts.md, domains/efl-championship.md, domains/crypto.md, domains/football-corners.md, domains/horse-racing.md
  - betting-rules/active-rules.md, betting-rules/injury-veto-80pct.md, betting-rules/away-team-threshold.md, betting-rules/never-back-predicted-loser.md, betting-rules/grass-veto.md, betting-rules/predicted-loser-rule.md
  - principles/raw-probabilities-lie.md, principles/removal-as-valuable-as-addition.md, principles/trust-the-model-over-punditry.md, principles/phantom-value.md, principles/data-leakage-silent-killer.md, principles/selectivity-is-everything.md, principles/majority-class-trap.md, principles/market-efficiency-varies-within-domain.md, principles/derivative-markets-harder-than-primary.md
  - operations/cowork-pipeline.md, operations/tool-routing.md, operations/known-failure-modes.md
- Pages updated: index.md
- Key new information: 28 pages covering the full AutoStrategy methodology (6 methodologies), all 8 betting domains with P&L tracking, 6 betting rules, 9 empirical principles, and 3 operations pages. Compound evaluation (L1-L5 framework) and probability calibration documented as core methodologies. Live betting P&L: NBA +£38.90, Tennis +£5.53, Snooker +£3.00.

## 2026-04-08 ingest | Phase 3 — Mark Agent & Mark-Lite
- Sources: raw/mark/FULL_PROJECT_CONTEXT.md, raw/mark/PROJECT_INSTRUCTIONS.md, Hawks/Mercia/BatSurveys/Warwickshire/Northants skill files
- Pages created:
  - products/mark-lite.md
  - clients/hawks-scaffolding.md, clients/midlands-bat-surveys.md, clients/jdw-brickwork.md
  - operations/email-infrastructure.md, operations/planit-api.md
  - principles/scheduled-tasks-need-zero-intervention.md, principles/strict-trade-matching.md
- Pages updated: products/mark.md (added all 5 variants — Hawks, Mercia Schools, Bat Surveys, Mark-Lite Warwickshire, Mark-Lite Northants)
- Key new information: Mark product variants fully documented — from original Hawks prototype through to current Mark-Lite Northants v2. Mark-Lite separated as its own product (Andy selling directly vs licensing the agent). 3 new clients added. Email infrastructure and PlanIt API documented as shared operations. Two new operational principles captured from Mark-Lite learnings.

## 2026-04-08 ingest | Phase 4 — Agent Browser & Hike SES
- Sources: raw/agent-browser/README.md, raw/agent-browser/browser-agent-paper.md, raw/agent-browser/project-instructions.txt
- Pages created:
  - products/betting-portfolio.md
  - operations/browser-agent-arch.md
- Pages updated: products/agent-browser.md, products/hike-ses.md
- Key new information: Browser agent architecture documented (Claude Code → Computer Use → Min browser pattern). Betting portfolio formalised as a product/income stream. Agent browser dual-track strategy documented: internal Hike tool + external commercial product.

## 2026-04-08 audit | Phase 5 — Cross-Reference Audit
- Sources: All existing wiki pages
- Pages created: none
- Pages updated: Multiple pages — verified and fixed bidirectional links across all 9 mandatory connection types (clients↔products, products↔methodologies, principles↔origins, domains↔betting-rules, people↔clients, operations↔products, strategy↔everything)
- Key new information: All 64 pages verified reachable within 2 clicks. No orphan pages. Cross-reference density confirmed adequate.

## 2026-04-08 synthesis | Phase 6 — Strategy Synthesis
- Sources: All wiki pages (cross-domain synthesis)
- Pages created: strategy/overview.md
- Pages updated: index.md
- Key new information: Strategy overview synthesised the "100×100 model" — revenue tracking (~£938.20 invoiced, ~£2,450 in proposals), the TTAI flywheel (consulting → product discovery → recurring revenue → network growth), product pipeline maturity, time allocation analysis, and Q2 2026 priorities. First page that genuinely could not have been written from any single project folder — validates the wiki's cross-domain purpose.

## 2026-04-08 analysis | Cross-Domain Pattern Analysis
- Sources: All 64 wiki pages across 9 categories
- Pages created: strategy/opportunities.md
- Pages updated: index.md
- External output: "TTAI Cross-Domain Pattern Analysis - April 2026.docx"
- Key new information: 10 cross-domain patterns identified, 12 concrete opportunities prioritised. Headline findings: (1) Compound evaluation framework underdeployed outside betting, (2) Revenue concentration mirrors majority-class trap (73% from KW Bell), (3) Planning portal data is a hidden platform opportunity, (4) Autoresearch loop only used in 2 of 6+ applicable domains, (5) Phantom value detectable in consulting pipeline using betting diagnostic, (6) Mike McSweeney proves multi-product expansion model, (7) Agent Browser is infrastructure not product, (8) Seasonal diversification unmanaged, (9) Removal principle has unacted business implications (darts, crypto, knowledge assistant), (10) Wiki methodology itself is proprietary IP.

## 2026-04-12 ingest | Mark-Lite Campaign Analysis (Autoresearch + Compound Eval)
- Sources: Mark-Lite Warwickshire Outreach Tracker (xlsx), Mark-Lite Northants Outreach Tracker (xlsx)
- Pages created: principles/planning-data-serves-site-trades.md
- Pages updated: products/mark-lite.md, strategy/opportunities.md, principles/_index.md, index.md
- External output: "Mark-Lite Campaign Analysis April 2026.docx"
- Key new information: First application of compound evaluation outside betting. L3 trade segmentation revealed 21.1% warm reply rate for site-based trades (Groundworks, Brickwork, Scaffolding) vs 0% for office-managed trades (Electrical, HVAC, Roofing, Drainage) across 65 firms. All 4 warm replies share profile: small firms, site trades, named contacts, replied at Email 3. New principle discovered: planning data serves site trades, not supply-chain trades. JDW Brickwork meeting prep included.

## 2026-04-12 ingest | Agent Browser — Prompt Caching & Cost Optimisation Research
- Sources: 2026-04-12-agent-browser-prompt-caching-and-optimisation-research.md (wiki inbox)
- Pages created: principles/trust-the-agent-not-dom.md
- Pages updated: products/agent-browser.md, principles/_index.md, index.md
- Key new information: Prompt caching implemented (~15-20% input token cost reduction). Schema workflow tested ($0.34, 14 iterations). Three-layer optimisation roadmap established: prompt caching (done) → deterministic routing (next, projected $0.72→$0.10-0.15/page) → action caching (later, ~80% cost reduction on repeats). Industry research validated independently-discovered patterns. Browser agent paper updated to 8 parts. New principle: trust the agent, not the DOM — visual agent bypasses Shadow DOM/React state that scripted approaches fight.

## 2026-04-12 operations | Wiki inbox folder established + direct filesystem write enabled
- Source: Screenshot showing Think Through AI/wiki/inbox/ folder structure; filesystem MCP config update
- Pages created: none
- Pages updated: none
- Key new information: Wiki ingest files from other Claude projects now drop into wiki/inbox/ folder. Filesystem MCP server now has write access to the wiki folder — wiki updates can be written directly without manual file uploads.

## 2026-04-13 ingest | Fred Betfair Exploration Report
- Sources: wiki/operations/fred-reports/2026-04-13-betfair-exploration.md
- Pages created:
  - principles/execution-cost-varies-by-selection.md — New principle: underdog spreads 2-8x wider than favourites across all sports
  - domains/t20-cricket-ipl.md — New domain page with market structure data and toss-window feasibility test design
- Pages updated:
  - domains/nba.md — Added Market Structure section with Betfair spread data, in-play observations
  - domains/darts.md — MODUS floor liquidity confirmed at £13-54; practically untradeable; fill-rate test recommended
  - domains/snooker.md — WC qualifier liquidity £385-4,281 with 8-30% spreads; restrict to main draw only
  - principles/_index.md — Added execution-cost-varies-by-selection
  - index.md — Added t20-cricket-ipl, execution-cost-varies-by-selection, fred operations entries, updated darts summary
  - operations/employee-framework.md — Fred added to Current Employees table
- Key new information:
  1. NBA underdog execution cost (2-8% spread) is a hidden drag not captured in paper trading. Paper ROI of +92.5% would compress in practice.
  2. Darts floor events are practically untradeable (£13-54 matched, 8-10% spreads). Removal principle likely applies.
  3. IPL cricket has best market structure examined (£68K, 0.5% spreads). Toss-window edge thesis is testable now -- IPL season is live.
  4. In-play betting structurally uneconomic across all sports at £5 stakes (spreads widen 3-4x).
  5. Snooker qualifiers untradeable; main draw viability check due April 18.

## 2026-04-13 operations | Fred AutoStrategy Employee created
- Pages created:
  - operations/fred-autostrategy-employee-SKILL.md (665 lines)
  - operations/fred-decision-log.md (initial template)
  - operations/fred-reports/ directory
- Pages updated:
  - operations/employee-framework.md — Fred added to Current Employees table, links, sources
  - index.md — Fred operations entries added
- Key new information: Third TTAI autonomous employee created. Fred manages the AutoStrategy betting portfolio daily. Five refinements applied: first-run safety valve, domain graduation criteria, Cowork pipeline predecessor reference, crypto VPS SSH access method, wiki file infrastructure.

## 2026-04-14 wiki-agent | Scheduled scan
- Sources scanned: Cowork sessions (autostrategy, Mark-lite, agent-browser, Master) + Claude.ai Chat via Min browser (JDW Brickworks, Mercia Flooring, Tonic Health, SEO audit)
- Pages updated:
  - clients/jdw-brickwork.md — CONVERTED, £500 setup invoiced, Mark build 21–25 April; Build Notes section added describing brickwork Mark variant (targets buyers/QSs at main contractors, planning portals + NHBC sources)
  - clients/tonic-health.md — ACCEPTED £1,750, INV-003 pending; Apify/Claude API/Notion access needed from Sunna
  - clients/mercia-flooring.md — 15 April go-live slipped; Outlook/Entra OAuth still outstanding with Solaas IT; Gmail send-as workaround under consideration
  - clients/steve-tipson.md — scoping email sent, parked awaiting response
  - domains/nba.md — P&L +£28.90 regular season close, predicted-loser experiment 8/8 NBA / 18/18 combined
  - products/agent-browser.md — atomic-actions vs workflows architectural direction captured
  - strategy/overview.md — revenue tables updated to reflect Tonic/JDW/Steve Tipson
  - index.md — bumped, added steve-tipson, tippercrete
- Pages created: clients/steve-tipson.md, clients/tippercrete.md
- Contradictions found: overview.md Q2 must-hit section still lists 15 April Mercia go-live (now slipped) — flagged for Andy, not retroactively rewritten
- Key changes: Two conversions in one day (JDW £500 setup + £200/mo; Tonic £1,750 first paid build). Mercia remains blocked on Outlook/Entra. New SEO prospect via Assisted (Steve Tipson) and new Mark-Lite groundworks prospect (Tippercrete, Warwickshire). Agent Browser pivoting toward atomic-actions model — candidate principle "capabilities before workflows".

## 2026-04-20 wiki-agent | Scheduled scan (resumed from compacted conversation)
- **Sources scanned**: 4 unprocessed ingest files in inbox/ (2026-04-16 Holmes signed, Holmes INV-006, Tonic approved, Slack bridge self-fire fix); Slack channel C0AT4K9KJFQ (50 messages); previously existing wiki pages.
- **Browser-based Claude.ai scan skipped**: User absent (autonomous run, no approval flow for computer-use), and ingest 2026-04-16 confirmed wiki input model officially moved to inbox/ + #ttai-employees Slack only.
- **Pages updated**:
  - clients/holmes-workholding.md — FULL REWRITE. Status: Signed — Mark build scheduled. £250 setup invoiced (INV-006). Full Companies House address added. Build 5-7 May, kickoff 5 May 10:00. "Other Tim" referral path and future consulting AI audit prospect captured.
  - clients/tonic-health.md — Build in progress; £1,750 invoiced (INV-005). Added Build Architecture (Apify → Python → Claude API → Notion → Slack), Phasing (Trustpilot-only Phase 1), ongoing cost model, creative quality bar.
  - clients/mercia-flooring.md — 2026-04-16 log entry added: Solaas IT reported Outlook/Entra fix applied; Andy to verify 17 April.
  - products/mark.md — Active Clients table now includes JDW (Signed, £500 INV-004, build 21-25 Apr) and Holmes (Signed, £250 INV-006, build 5-7 May). Mercia row updated.
  - betting-rules/predicted-loser-rule.md — FULL REWRITE. Status: FORMALISED 2026-04-16 at 18/18 (NBA 8/8 + Tennis 10/10). First rule to complete full AutoStrategy evidence cycle. Decision log updated.
  - betting-rules/never-back-predicted-loser.md — Synced to FORMALISED status, note added pointing to predicted-loser-rule as canonical narrative.
  - betting-rules/active-rules.md — Predicted-loser moved to FORMALISED row; methodological significance section added.
  - strategy/overview.md — CRITICAL REVENUE CORRECTION. Q1 invoiced updated from £938.20 to £3,438.20. Pipeline restructured — JDW/Tonic/Holmes moved out of "proposals" and into invoiced. KW Bell concentration dropped from ~73% to ~20%. Must-Hit section rewritten for 17-28 April convergence window. Added custom AI builds as new third revenue stream.
  - index.md — Bumped to 2026-04-20. Holmes/JDW/Tonic summary lines updated to reflect signed/invoiced status. Added test-before-quoting and phase-it-if-dependency-fragile principles (from Tonic ingest). Added ttai-slack-bridge operations entry.
- **Inbox files processed** (moved to inbox/processed/):
  - 2026-04-16-ttai-holmes-workholding-signed.md
  - 2026-04-16-ttai-holmes-inv006-raised.md
  - 2026-04-16-ttai-tonic-health-approved.md
  - 2026-04-16-ttai-slack-bridge-self-fire-fix.md
- **Notable findings flagged for Andy**:
  1. **Orphaned branches issue** — all 2026-04-16 Wiki runs committed to feature branches (e.g. claude/magical-goldberg-IMV8Z) that never merged to main. This run captured decisions from ingest files but the pages those orphaned runs created (if any) may still be missing from main. Investigation needed.
  2. **Revenue de-concentration** — client revenue risk profile has materially improved (KW Bell went from 73% to 20% of invoiced revenue). Worth noting when planning Q2.
  3. **April 17-28 convergence window** — Mercia verification + JDW build + Tonic Phase 1 + AccXel discovery all land within ~11 days. Tight but workable; flagged as main operational risk.
  4. **Predicted-loser rule formalisation** — first AutoStrategy rule to complete full evidence cycle. Validates the paper-trade-to-formalisation pipeline before it's stretched to Snooker/Darts/IPL/Crypto.
  5. **New principles candidate surfaced** (from Tonic): "test before quoting" and "phase it if a dependency is fragile". Added to index but principles/ pages not yet written — will need a dedicated ingest session.

## 2026-04-20 wiki-agent | Chrome-MCP continuation (post-compact)
- **Method**: User requested a second pass using the Claude-in-Chrome MCP to scan claude.ai project chats directly (DOM-aware, no computer-use approval flow). Scanned Think Through AI (Tim Holmes + Tonic ad-creative chats), Agent Browser (Hike proposal chat), and AutoStrategy (IPL chat) projects. Applied findings via filesystem MCP to the wiki on Andy's real disk (/Users/andyallen/Documents/Claude/Projects/Think Through AI/wiki/).
- **Pages updated**:
  - clients/jdw-brickwork.md — Registered address added (Brooks Road, Raunds, NN9 6NS). Customer tier examples (Parrot Construction → United Living → Mulberry Homes). Commercial scope (school extensions, sports halls, community centres). Post-planning pre-construction timing window. Email infrastructure plan mirroring Mercia pattern. Calibration step formalised in Next Actions. Date bumped to 2026-04-20.
  - clients/mercia-flooring.md — Outlook/Entra app-password gotcha added: mysignins.microsoft.com/security-info only shows sign-in methods for the currently authenticated user, so Jack at Solaas IT saw his own account; Pete must generate the app password himself.
  - clients/tonic-health.md — Day 2 build status (950 reviews extracted; pillar distribution analysed; brain_focus at 0.2% is genuine data signal, not prompt failure — don't re-extract). Claude Code worktrees ops lesson added (feature-branch files invisible in main tree). [[known-failure-modes]] link added.
  - products/agent-browser.md — Model A vs Model B commercial shapes section with "Kit insight" (AI as user of existing software, not replacement). Hike proposal status (20 features catalogued in 1-2 hours, drafted/finalised 17 Apr). Hike SEO Internal+External and Mark Product Line Model B destination subsections. Links to [[platform-mapping-compounds]] and [[bryn]].
  - products/mark.md — Calibration step bullet added to Setup. New "Onboarding: The Calibration Step (formalised 2026-04-20)" section with 3-step process (Trade fit / Size fit / Contact fit). Links to [[jdw-brickwork]] and [[agent-browser]] added.
  - domains/t20-cricket-ipl.md — "Findings from First AutoStrategy Pass (2026-04-14)" section: Bayesian Beta(α,β) beats raw win rates; H2H hurts; three-way ensemble; toss×venue 3-6% edge shift. Methodological caveat added about pre-scripted vs genuine autoresearch. Decision log entry 2026-04-14.
  - methodologies/autostrategy.md — "Audit: Pre-scripted Search vs Genuine Autoresearch (2026-04-14)" section distinguishing NBA/Tennis/EFL (genuine) from IPL/horse-racing (pre-scripted). Rule adopted: TASK.md must explicitly require Claude API / tool use per iteration. Link to [[t20-cricket-ipl]] added.
  - people/bryn.md — "Active Decision — Hike Agent Browser Proposal (17 Apr 2026)" section with open questions for Bryn (cost-reduction vs capacity vs differentiator angle).
  - principles/_index.md — Registered [[platform-mapping-compounds]] under Agent Browser Principles. Front-matter date bumped.
  - index.md — agent-browser, bryn, jdw-brickwork summary lines updated. [[platform-mapping-compounds]] principle entry added.
- **Pages created**:
  - principles/platform-mapping-compounds.md — NEW principle. Discovered via Hike audit: ~100x speedup on platform-resident feature mapping (24-day estimate → 1-2 hours for 20 features) because once a platform's patterns are mapped, subsequent features are mechanical. Applies to Evolution MX (KW Bell), future Model A work, Mark onboarding variants. Counterexamples: cross-platform doesn't compound; dynamic UIs can re-inject cost.
- **Key insights captured from Chrome scans**:
  1. **Model A vs Model B commercial shapes** (Agent Browser): A = infrastructure installed inside client systems (sold per-client); B = hidden infrastructure powering Andy's own services (Mark, Hike, future verticals). The Kit insight: both models rely on AI *using* existing software rather than replacing it — that's what keeps deals small and fast-to-close.
  2. **Calibration step formalised** (Mark): before any Mark go-live, run a test batch of 5-10 leads and confirm trade/size/contact fit with the client. Applied immediately to JDW onboarding. Stops the Mercia/Warwickshire-style post-launch opt-outs.
  3. **Platform-mapping compounds** (Agent Browser): first feature on a platform is expensive (discovery + DOM mapping + error modes); subsequent features are mechanical. Counterexample: cross-platform work doesn't compound, so cost per client resets unless same SaaS.
  4. **IPL AutoStrategy was pre-scripted** (AutoStrategy audit): the 2026-04-14 IPL pass looked like autoresearch but didn't call Claude in the loop. Rule adopted: TASK.md must explicitly require Claude API / tool use per iteration. Findings themselves (Bayesian Beta, H2H hurts, ensemble, toss×venue) are still transferable.
  5. **Tonic Day 2 genuine-signal finding**: brain_focus pillar at 0.2% is a real data signal (nobody writes reviews about focus), not a broken prompt — don't re-extract.
  6. **Outlook/Entra app-password gotcha** (Mercia operational): mysignins.microsoft.com/security-info only shows sign-in methods for the currently authenticated user; account holder must generate themselves. Explains the Jack-at-Solaas confusion.
- **Relationship to earlier 2026-04-20 run**: The first run of the day processed ingest/ + Slack bridge and reflected signed contracts (Holmes, Tonic, JDW) + revenue correction. This second run is purely qualitative — insight/principle level, no revenue or status changes. Both runs stack cleanly.
