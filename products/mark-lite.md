# Mark-Lite

> Direct-sales lead generation service where Andy sells Mark's output (pre-found construction leads) directly to tradespeople. Time-bounded campaigns by region; current focus: Warwickshire (v3) and Northamptonshire (v2). Now includes Construction Intelligence tier (£75/month data feed).
> Last updated: 2026-04-16

## What Mark-Lite Is

**Mark-Lite** is a separate commercial model from the managed [[mark]] service. Instead of Andy running Mark on behalf of a trade client (client owns the service), Mark-Lite is Andy selling the output directly:

- Andy finds construction leads via [[planit-api]] and tender portals
- Andy sends outreach emails on the leads he found (to tradespeople in a given region)
- Tradespeople receive 4-week email + LinkedIn sequence introducing leads, then an offer to become an ongoing client

This is a **tactical, time-bounded engagement** rather than an ongoing retainer. Mark-Lite campaign typically runs 4-12 weeks, then transitions to either an ongoing managed Mark contract or winds down.

## Regional Variants & Evolution

### Warwickshire (v3) — Live

**26 trade prospects across 8 trades:**
- Roofing (6 firms: Sage, F.H. Roofing, Jessop, Moss, JCD, M Carty Brickwork)
- Groundworks (5 firms: Kimben, J&M Groundworks, KAVAN/SRK, Tippercrete, A Valley Plant)
- Electrical (4 firms: JRP, Synergy, Hertz, Multiphase, Coventry Electrical, Switched On, Ac Electrical 4u)
- HVAC/Mechanical (6 firms: Rowland AC, Chilled, Univent, Chillaire, PRT Heating, Temp Air)
- Brickwork, Drainage
- **Excludes:** Scaffolding (exclusive agreement with [[hawks-scaffolding]])

**Batch Structure (updated from Northants learnings):**
- Tuesday: Roofing + Brickwork (6 firms)
- Wednesday: Groundworks + Drainage + Brickwork (5 firms)
- Thursday: Groundworks + Electrical (5 firms)
- Friday: Electrical (4 firms)
- Monday: HVAC/Mechanical (6 firms)

**Key Learnings Incorporated:**
- Email 1 opens with "I'm not involved in these — I just find them and pass them on" (clarifies Andy's role)
- Subject lines rotate A-B-C (not random, strict fixed rotation across batch)
- Email 3 Mark introduction: 45 words, no pricing mention (was 95 words with price, caused lower conversion)
- Package language throughout ("groundworks and drainage packages" not planning-speak)
- Strict explicit-only trade matching for Electrical, HVAC, Roofing — no inferred leads
- Size-fit tags enforced: Small jobs only / Small to medium / Open to larger commercial
- 50%+ named contact rate hard gate
- Warm vs. opted-out replies tracked separately

### Northamptonshire (v2) — Live, Post-Warwickshire

**39 construction trade subcontractors across 8 trades:**
- Groundworks, Civil Engineering, Brickwork, Drainage
- Scaffolding (scope expanded from Warwickshire; applied explicit-only gate)
- Roofing, Electrical, HVAC/Mechanical

**Batch Structure:**
- Monday: Groundworks + Civil + Brickwork + Drainage (8 firms)
- Tuesday: Civil + Scaffolding + Brickwork + Drainage (8 firms)
- Wednesday: Scaffolding + Roofing + Brickwork + Drainage (7 firms)
- Thursday: Roofing + Electrical + Drainage (8 firms)
- Friday: Electrical + HVAC + Drainage (6 firms)

**v2 Improvements Over Warwickshire:**
- Better email clarity in Email 1 (one-line "who I am")
- Subject line rotation in all three A-B-C formats (v1 was less systematic)
- Partial lead allowance: Email 1 and 4 can run with 1/2 leads if no second explicit match exists (logged as "Drafted with 1/2 leads")
- Skip-gap check-in template: if a prospect skipped 2+ weeks, send a warm "keeping an eye out" email (doesn't count in 4-email sequence)
- Stricter trade matching: Electrical, HVAC, Roofing, Scaffolding, Drainage all explicit-only
- Tender portal search mandatory for Electrical, Roofing, HVAC, Scaffolding (don't appear in planning data)

**Converted:**
- **Josh Warren ([[jdw-brickwork]])** — CONVERTED 14 April. £500 setup invoiced (TTAI-004), £200/month ongoing. Mark build 21--25 April. Inbound from campaign Email 1 -- skipped intelligence tier entirely.

**Warm Prospects:**
- **Daniel Fordham ([[tippercrete]])** — Re-engagement email sent 13 April. Replied twice within 19 min. Construction Intelligence sample delivered 14 April. Monitoring.

**Other Warm Reply:**
- **Brian Kelly (Hawk Drainage)** — Warm response to planning application lead

## Campaign Performance Analysis (April 2026)

First application of [[compound-evaluation]] framework outside AutoStrategy betting. Analysed both trackers (Warwickshire 26 firms, Northants 39 firms) on 2026-04-12.

### Combined Results

| Metric | Warwickshire | Northants | Combined |
|---|---|---|---|
| Companies reached | 26 | 39 | 65 |
| Warm replies | 2 (7.7%) | 2 (5.1%) | 4 (6.2%) |
| Opt-outs | 2 (7.7%) | 0 (0%) | 2 (3.1%) |
| Sequence completion (E1→E4) | 65% | 39% | — |
| Bounces | 0 | 3 (8%) | 3 (4.6%) |

### Compound Evaluation Scores

**L1 (Deliverability):** Warwickshire 100%, Northants 92%. Warks scores higher — zero bounces. Northants had 3 bounces (MBH Construction, Brennan Building, A-Span).

**L2 (Holdout — Northants as unseen test set):** Warm reply rate 5.1% vs 7.7% training. Inconclusive due to sample size, but zero opt-outs in Northants is a genuine positive signal — v2 email clarity improvements likely reduced friction.

**L3 (Trade Segment Split):** The critical finding. Overall 6.2% reply rate hides a dramatic split:

| Trade Classification | Firms | Warm Replies | Rate | Opt-Outs |
|---|---|---|---|---|
| **Site-based trades** (Groundworks, Brickwork, Scaffolding) | 19 | 4 | **21.1%** | 0 |
| **Office-managed trades** (Electrical, HVAC, Roofing, Drainage) | 34 | 0 | **0%** | 2 |

This is the [[majority-class-trap]] in campaign data. The overall rate masks a strong signal with noise.

### Warm Reply Profile

All four warm replies share characteristics:
- **Trade:** Physical, on-site trades only (Groundworks ×2, Brickwork ×1, Scaffolding ×1)
- **Size:** Small firms (5–18 employees), owner-operator reading own email
- **Reply timing:** Email 3 (the Mark introduction) in 3 of 4 cases
- **Contact quality:** Named personal contact in all cases

### Key Insight: Planning Data Serves Site Trades, Not Supply-Chain Trades

Planning-sourced leads have high value for trades that win work directly from developers (Groundworks, Brickwork, Scaffolding) and low value for trades subcontracted through supply chains (Electrical, HVAC). This maps to [[market-efficiency-varies-within-domain]] — the lead source must match the trade's business development pattern.

See [[planning-data-serves-site-trades]] for the full principle.

### Skip-Gap Problem

Northants had 9 skipped outreach entries. Drainage (5 firms, 0 reached Email 4), Roofing (5 firms stuck at Email 2), and HVAC (4 firms stuck at Email 2) were most affected. The strict explicit-only matching rule correctly prevents bad leads, but these trades never progress past Email 2 because their work doesn't appear in planning data.

### V2 Improvement Assessment

| Change | Evidence | Verdict |
|---|---|---|
| Clearer "who I am" in Email 1 | 0 opt-outs (vs 2 in Warks) | Likely positive |
| Shorter Mark intro (95→45 words) | JDW replied at Email 3 | Promising |
| Strict explicit-only matching | No irrelevant sends; caused skip-gaps | Correct but limiting |
| A-B-C subject rotation | No pattern visible in replies | Inconclusive |

## Technical Architecture

Same two-skill model as managed Mark:

### Weekly Lead Finding Skill (Northants v2)
- Searches PlanIt GeoRSS feeds (4 Northamptonshire authorities)
- Mandatory tender portal search for Electrical, Roofing, HVAC, Scaffolding (Find-a-Tender, Construction Enquirer, contractor supply chains)
- Tags leads by size (Small = 21 day expiry, Medium = 42 days, Large = 56 days)
- Trade confidence: Explicit vs. Inferred
- Finds named contacts (70% target)
- Deduplicates against existing Opportunities tab
- Maintains 70%+ small-to-medium project mix

### Daily Outreach Skill (Northants v2)
- Reads leads from Opportunities tab
- Matches to today's prospect batch using: trade (explicit-only for hard trades) + size-fit + freshness
- Email validation: MX record checks
- Creates Gmail drafts (never sends directly)
- Prepares LinkedIn tasks
- Updates tracker (Companies, Outreach_Log, Opportunities, LinkedIn_Tasks tabs)

## Email Sequence (4 Weeks)

### Email 1 (Value + Who I Am)
**Subject:** Cycles A-B-C formats:
- A: `Spotted this for you — [Project], [Town]`
- B: `[Project], [Town] — could be relevant for you`
- C: `New [trade] work near you — [Project]`

Content: 2 leads, ~65 words. Opens with "I track upcoming construction projects... I'm not involved in these — I just find them and pass them on."

### Email 2 (Value + Decision Maker)
**Subject:** `[Project] — found the contact too`

Content: 1 lead with named contact, ~75 words. Includes "PS I'm finding 10-20 of these a week. Let me know if you'd like to keep getting them."

### Email 3 (Value + Decision Maker + Introduce Mark)
**Subject:** `Spotted another one for you — [Project], [Town]`

Content: 1 lead with contact. Introduces Mark:
> "I find these every week using something I've built called Mark. He finds local projects, works out who's running them, and gets in touch on your behalf — so you're in front of the right people without doing the legwork yourself. If that sounds useful, happy to jump on a quick call and show you how it works."

**Copy locked** — do not rewrite or allow tool to alter this paragraph.

### Email 4 (Final Value + Last Chance)
**Subject:** `Last one from me — [Project], [Town]`

Content: 2 leads, ~80 words. "If you'd like me to set this up properly for your firm, happy to have a quick chat."

### Skip-Gap Check-In (If No Matching Leads 2+ Weeks)
**Subject:** `Keeping an eye out for you`

Content: Brief, warm acknowledgement. Does NOT count as a numbered email. Max one per prospect.

## Construction Intelligence (New Product Tier -- April 2026)

A lower-commitment entry product sitting below the managed Mark service:

- **Price:** £75/month (vs £200/month for managed Mark)
- **What it is:** Data feed of construction project opportunities in the prospect's region and trade, delivered weekly
- **What it isn't:** No outreach, no email sequences, no lead contact -- just the intelligence
- **First live test:** 12-firm re-engagement batch sent 13 April 2026 using this pitch
- **Monitoring window:** Results expected 18--19 April 2026

**Direction-of-Initiation Hypothesis (1 data point):**
Cold outreach prospects convert to Construction Intelligence (low commitment) first. Inbound prospects convert straight to managed Mark. Evidence: JDW Brickwork (inbound) skipped the intelligence tier entirely and went straight to £500 setup + £200/month. Needs second data point to confirm -- watch re-engagement batch results.

**Strategic fit:** This is the [[position-next-stage-not-bigger-commitment]] principle applied to product architecture. Cold prospects who didn't respond to the £200/month pitch may convert at £75/month for data only.

## Pricing & Conversion Path

**Two-tier funnel (from April 2026):**

| Path | Entry Product | Upgrade Path |
|------|--------------|-------------|
| Cold outreach (no prior response) | Construction Intelligence £75/month | → Managed Mark £200/month |
| Inbound / warm referral | Managed Mark direct | £250-£500 setup + £200/month |

**Typical flow for engaged prospects:**

1. Week 1-4: Email + LinkedIn sequence (value prop: consistent lead stream)
2. Week 4 Email 3: Introduction to Mark and offer for ongoing service
3. Warm reply or inbound meeting request → Discovery call
4. Transition to managed [[mark]] contract (£250-£500 setup + £200/month ongoing)

**Josh Warren (JDW Brickwork) flow:**
- Inbound lead from Email 1 campaign
- Showed interest ("I'd like to hear more about this")
- Scheduled discovery meeting 14 April
- **CONVERTED** -- same-day close, £500 setup invoiced (TTAI-004), build 21-25 April

## Tracker Structure

**Single shared tracker** (Mark-Lite Northants Outreach Tracker) with 5 tabs:

1. **Companies** — 39 prospect records (email, contact name, trade, size-fit, email status, LinkedIn status, last email drafted, notes)
2. **Opportunities** — All leads found + their allocation to prospects
3. **Outreach_Log** — Every draft created (date, company, email #, subject, status, notes)
4. **LinkedIn_Tasks** — Manual tasks (connect on Email 1, message on Emails 2-4)
5. **Daily_Batches** — Batch assignments by day + status (Pending, In Sequence, Complete)

## Key Guardrails

- **Explicit-only for hard trades:** Electrical, HVAC, Roofing, Drainage, Scaffolding require explicit trade mentions in planning data or tender documents
- **Size-fit enforcement:** Never send a "Small jobs only" prospect a Large lead
- **70%+ small-to-medium mix:** Campaigns stall if dominated by mega-projects
- **No duplicate leads to same prospect:** Track in Opportunities tab `Used In Email To` column
- **MX record checks mandatory:** Before sending, verify domain has valid MX records
- **Contact rate target:** 50%+ of leads should have named decision-maker emails
- **LinkedIn only for personal profiles:** Skip firm company pages (no connection requests possible)
- **All emails are drafts:** Gmail MCP creates drafts; prospects review and hit send manually

## Prospects for Next Expansion

- **Midlands region** (beyond Warwickshire + Northamptonshire) — different council authorities, same trade types
- **Other sectors** — plumbing, electrical, HVAC, mechanical services (not construction-focused)
- **Professional services** — accountants, solicitors (different lead sources, same skill architecture)

## Links

- [[mark]] — Managed service model (client owns the service)
- [[mark-lite-daily-outreach-northants-v2]] — Daily skill detail
- [[mark-lite-weekly-lead-finding-northants-v2]] — Weekly skill detail
- [[planit-api]] — Planning data source
- [[email-infrastructure]] — Email validation, domain management
- [[email-quality-over-volume]] — Short, confident email principle
- [[strict-trade-matching]] — Trade-specific prospect matching principle
- [[selectivity-is-everything]] — Lead qualification selectivity
- [[planning-data-serves-site-trades]] — New principle from April 2026 campaign analysis
- [[compound-evaluation]] — L1–L3 framework applied to campaign data
- [[majority-class-trap]] — Trade segment split mirrors this betting principle

## Re-Engagement Campaign (April 2026)

**Batch details:** 17 re-engagement drafts created (12 April), 12 confirmed sent (13 April). 5 scaffolding drafts not found in Sent/Drafts -- treating as parked.

| Metric | Value |
|--------|-------|
| Emails sent | 12 (of 17 drafted) |
| Monitoring window | 13--19 April |
| Replies (day 2) | 0 (excl. Danny/Tippercrete handled separately) |
| Bounces | 0 |
| Product pitched | Construction Intelligence £75/month |

Office-managed trades (Electrical, HVAC, Roofing, Drainage) formally parked as of 12 April based on 0% engagement rate across 34 firms.

## Sources

- /sessions/brave-vigilant-gauss/mnt/Projects--Think Through AI/raw/mark/FULL_PROJECT_CONTEXT.md
- Mark-Lite Warwickshire Skills (SKILL 4, SKILL 5)
- Mark-Lite Northamptonshire v2 SKILL files
- Mark-Lite Campaign Analysis April 2026 (tracker data analysis, 2026-04-12)
- Mark-Lite Daily Reports: 2026-04-12, 2026-04-13, 2026-04-15
