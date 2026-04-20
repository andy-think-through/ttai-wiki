# Mark

> Productised AI lead-finding agent for trades and service businesses. Automates discovery, qualification, and outreach across email and planning portal monitoring. Managed service model at £200-£500 setup + £200/month ongoing.
> Last updated: 2026-04-20

## What Mark Does

**Mark** is Andy's core productised service: an AI agent that automates lead generation and outreach for small trade and service businesses. Andy runs Mark on behalf of clients (managed service model), not as a SaaS they self-operate.

### The Workflow

Mark executes a three-stage workflow:

1. **Lead Discovery** — Searches planning portals (PlanIt API, council portals) + tender sites + news sources for construction/service work relevant to the prospect's trade
2. **Contact Research** — Identifies the decision-maker and validates their email address
3. **Outreach** — Drafts and sends personalised cold emails (via Gmail or Outlook) + LinkedIn connection requests + sends summary reports

All outreach happens via the client's own email account or dedicated service email (warmed up via Lemwarm). This preserves the client's brand and domain reputation.

## Technical Architecture

### Core Platforms

- **Manus** — Execution platform where Mark skills are packaged and run. Skills are YAML/Markdown files zipped as `.skill` archives
- **Go High Level** — CRM for lead capture and qualification
- **Email Infrastructure**
  - **Gmail MCP / Outlook MCP** — for draft creation and sending
  - **Lemwarm** — email warm-up service for new sending domains
  - **Hunter.io** — email validation and verification
- **Planning Portal APIs** — PlanIt (primary), council-specific portals (secondary)
- **Google Sheets / XLSX** — Tracker spreadsheets (single source of truth for leads, prospects, outreach status)

### Skill-Based Architecture

Mark is built as a **two-skill system** per client variant:

1. **Weekly Lead Finding Skill** — (Runs once per week, credit-intensive)
   - Searches planning portals for new projects matching the client's target trades
   - Identifies lead size and trade-package confidence (explicit vs. inferred)
   - Finds decision-maker contacts
   - Updates tracker with new leads

2. **Daily Outreach Skill** — (Runs 1-5 times per week)
   - Reads leads from tracker
   - Matches leads to today's prospect batch (trade relevance + company size-fit)
   - Verifies email domains (MX records)
   - Creates email drafts + LinkedIn tasks
   - Updates tracker with outreach status

This split keeps credit costs reasonable (weekly heavy lifting) while maintaining daily engagement velocity.

## Service Model & Pricing

- **Setup:** £250–£500 one-time
  - Integration of client email account (Gmail or Outlook)
  - Initial prospect list research + enrichment
  - First batch of leads discovered and validated
  - Go High Level setup (if used)
  - **Calibration step** (see below) — test batch of 5–10 leads sent to the client for review before go-live

- **Ongoing:** £200/month
  - Twice-weekly lead discovery
  - Daily-to-weekly outreach (depends on client)
  - Tracker management + reporting
  - Optimisation based on reply feedback

**Exclusivity:** Client-specific agreements possible (e.g., Hawks Scaffolding has exclusive scaffolding in Warwickshire)

## Client Variants & Evolution

### Original: Hawks Scaffolding (v2)
**Live since 2026-02-12**

- **Trade:** Scaffolding services (Warwickshire, ~1.5hr radius of Rugby)
- **Lead Sources:** PlanIt Warwickshire + 7 council portals + developer news + main contractor news
- **Outreach:** Browser-based lead discovery → contact research → email validation → Outlook Web sends + LinkedIn
- **Status:** First live customer, strategic loss-leader at £500/month
- **v2 Improvements** (applied from Northants learnings):
  - Explicit-only scaffolding matching (removed inference)
  - 70/30 small-to-medium project size gate
  - Mandatory tender portal searches (scaffolding never appears in planning data)
  - Website-based email verification (not SMTP guessing)
  - A-B-C subject line rotation (fixed sequential rotation, not random)
  - 50% contact rate hard gate (no contact = no send)
  - Single persistent tracker (replaced 3 separate markdown files)

### Mercia Flooring Group (Client-Specific)
**Planned go-live: 2026-04-15**

- **Trade:** Education flooring (schools, primarily)
- **Approach:** DfE GIAS data (not planning portals) — schools are a static, known universe
- **Two Dedicated Skills:**
  - **School List Builder** — Downloads GIAS, filters to postcode area, enriches with SBM/site manager contacts, priority-flags by school size + FSM%, writes to tracker
  - **Email Drafter** — Reads school list, checks for replies, drafts two templates: Cold Intro (first contact) + "In Your Area" (follow-up when Peter visits area)
- **Seasonal:** Mid-Jan to early July only (schools outreach window); July-Sept = delivery; Oct-Dec = retail focus (out of scope)
- **Service Model:** Managed outreach — Andy triggers batches based on Peter's upcoming visit schedule (e.g., "I'm in Coventry on 15th, Reading on 16th")
- **Pricing:** £200 setup, £200/month ongoing, plus optional £300 Stannp add-on for physical letters to homeowners
- **Outlook Integration:** Pending IT admin access (Martin at Solaas IT)

### Midlands Bat Surveys (Mike McSweeney)
**Live and operational**

- **Business Model:** Domestic bat surveys tied to planning applications (ecologists + surveyors delivered by freelancers)
- **Lead Type:** Unique — planning portal monitoring (not traditional lead finding)
- **Two Dedicated Skills:**
  - **Weekly Lead Finding** — PlanIt queries for loft conversions, barn conversions, demolitions, re-roofing, listed building work. Identifies architect/planning consultant firms (agent outreach) or homeowners (for physical letter add-on, Option 2)
  - **Daily Outreach** — Emails architect/planning consultant firms with bespoke tone per firm type (architects vs. consultants vs. building surveyors)
- **Pricing:** £500 (Option 1: agent outreach only; confirmed). £800 with homeowner letter intelligence (declined). £300 add-on for automated Stannp physical letter sending (scoped, not built)
- **Rate Limiting:** PlanIt API strict 1 req/min; uses two region IDs (`auth=469` West Midlands + `auth=468` East Midlands) for combined queries
- **Key Gotcha:** 65% of domestic applications have NO agent (self-submitted) — these are parked for Option 2

## Variant: [[mark-lite]]

Mark-Lite is the **direct-sales variant** where Andy sells lead generation output directly to tradespeople as a time-bounded service (not ongoing retainer). Two live regions:

- **Warwickshire (v3)** — 26 trade prospects across 8 trades. Excludes scaffolding (Hawks exclusivity). Learned: small contained projects perform better than mega-schemes; explicit trade matches > inferred
- **Northamptonshire (v2)** — 39 trade prospects. Post-Warwickshire improvements: better email clarity, subject line rotation, strict explicit-only matching for Electrical/HVAC/Roofing/Drainage/Scaffolding

Both use the two-skill architecture (Weekly Lead Finding + Daily Outreach) but feed into a single tracker shared across all 39 prospects in the region. Email 1 introduces Mark; Email 3 pitches a trial; Email 4 final offer.

## Onboarding: The Calibration Step (formalised 2026-04-20)

Every new Mark build now includes a **calibration step** in the early part of the build week:

1. Generate a test batch of 5–10 candidate leads using the client-specific Weekly Lead Finding skill.
2. Send the batch to the client **before** any outreach goes out, asking three questions:
   - Trade fit — are these the kinds of projects you'd actually want to quote?
   - Size fit — are these companies the right scale for your team?
   - Contact fit — is the named decision-maker the person you'd want to be talking to?
3. Use the client's reply to retune trade tagging, size filters, and contact-type preferences **before** the first real send.

**Why:** Gives the client a low-commitment way to shape the agent's output, catches trade-match mistakes cheaply, and builds confidence that the first cold email is actually a well-aimed one. First formalised on [[jdw-brickwork]] build (21–25 Apr 2026); now a Mark onboarding default.

**Why it matters for Model B ([[agent-browser]]):** Mark is currently Manus-driven, but the calibration step is platform-agnostic — it applies equally when the backend migrates to a browser agent.

## Key Technical Patterns

### Email Infrastructure

- **Email Verification:** Hunter.io (preferred) > website-based checks (fallback if SMTP gets blocked)
- **Never fabricate emails** — only verified addresses or published website emails
- **Lemwarm warm-up** for new sending domains (mark@merciafloors.co.uk, midlandsbarsurveys@gmail.com)
- **Email templates locked** — personalise only specified placeholders; do not rewrite copy without client approval

### Planning Data

- **PlanIt API** — Rate limit 1 req/min; use JSON endpoint (not GeoRSS) for full descriptions; browser-based access preferred over curl/requests to avoid 429 lockout
- **Trade Confidence Tagging** — Explicit (directly mentioned) vs. Inferred (likely needed but not stated). Strict explicit-only rule for Electrical, HVAC, Roofing, Drainage, Scaffolding
- **Application Type Filtering** — Include HFUL, Full, Heritage/LBC, CLP. Exclude TCA, TPO, AOC, Discharge, SCR (Conditions applications are dead leads — ecology requirements already discharged)
- **Geographic Filtering** — Use region IDs (not circle searches, which time out); support OR operators for keyword combinations

### Tracker Management

- **Single Source of Truth** — Download from Google Drive (rclone), modify locally (openpyxl), re-upload
- **Critical Pattern** — Pre-formatted blank rows make `ws.max_row` unreliable; always filter with `any(cell is not None for cell in row)`
- **Deduplication** — Match on unique key (application ref, company name, URN for schools) before adding
- **Lead Expiry** — Size-based (Small = 21 days, Medium = 42 days, Large = 56 days); never use a lead past Use By date

## Active Clients & Prospects

| Client | Status | Model | Monthly | Notes |
|---|---|---|---|---|
| [[hawks-scaffolding]] | Live | Managed | £200 | First customer; v2 build; exclusive Warwickshire scaffolding |
| [[mercia-flooring]] | Go-live pending (Outlook verify 17 Apr) | Managed | £200 | Schools outreach; seasonal Jan-July; fix reported by Solaas IT 16 Apr |
| [[midlands-bat-surveys]] | Live | Managed | £500 | Planning portal variant; eco firms as targets; two region IDs |
| [[jdw-brickwork]] | Signed — build 21-25 Apr | Managed | £200 | First Mark-Lite → Mark conversion; £500 setup (INV-004); brickwork variant targets buyers/QSs at main contractors |
| [[holmes-workholding]] | Signed — build 5-7 May | Managed | £200 | Third paying Mark client; £250 setup (INV-006); precision-engineering vertical; kickoff 5 May 10:00 |
| Mark-Lite (Warwickshire) | Live | Time-bounded | N/A | 26-firm campaign; post-Warwickshire learnings |
| Mark-Lite (Northamptonshire) | Live | Time-bounded | N/A | 39-firm campaign; v2 improvements |

## Cross-Product Learnings

### From Warwickshire to Northamptonshire (v2 Updates)

- Email 1 now explicitly clarifies "I'm not involved in these — I just find them" (recipients assumed Andy was the client)
- Subject lines now rotate A-B-C pattern (fixed rotation, not random; prevents "looks automated")
- Email 3 Mark introduction cut from 95 to 45 words, no pricing (better conversion)
- Package language throughout ("groundworks and drainage packages") not planning-speak
- Strict explicit-only for Drainage, Electrical, HVAC, Roofing, Scaffolding (inferred matches = opt-outs)
- Warm replies distinguished from opt-outs in tracker (enables manual follow-up)

### Unresolved Patterns

- **Tender Portal Search Mandatory for Some Trades** — Electrical, HVAC, Roofing, Scaffolding never appear in planning applications; must search Find-a-Tender + Construction Enquirer + contractor supply chains separately
- **Size-Fit Matching Critical** — Sending large logistics parks to 5-person groundworks firms causes disengagement; 70%+ small-to-medium lead mix needed
- **Contact Rate Hard Gate** — No named contact = lower conversion; aim for 50%+ of leads with decision-maker emails
- **LinkedIn Threading** — Connection requests on Email 1; messages on Emails 2-4. Acceptance rates vary; if post-Week 2 acceptance is poor, Andy may pause LinkedIn tasks

## Future Directions

- **Physical Letter Add-On (Stannp)** — Bat Surveys Option 2 (homeowner letters) — scoped at £300, not yet built
- **Cowork/Claude Execution** — Alternative to Manus (Claude can run daily outreach via Gmail MCP; cannot access PlanIt due to network restrictions)
- **Sectoral Expansion** — Mark pattern proven; next candidates: trades in different regions, service sector (plumbing, electrical), professional services (accountants, solicitors)

## Links

- [[mark-lite]] — Direct-sales variant for tradespeople
- [[hawks-scaffolding]] — First live Mark customer
- [[mercia-flooring]] — Upcoming client (schools focus)
- [[midlands-bat-surveys]] — Planning portal variant
- [[jdw-brickwork]] — First build to formalise the calibration step
- [[email-infrastructure]] — Email validation, warm-up, MCP integration
- [[planit-api]] — Planning data source and technical patterns
- [[email-quality-over-volume]] — Email composition principle
- [[strict-trade-matching]] — Trade-specific lead matching principle
- [[selectivity-is-everything]] — Lead filtering and qualification principle
- [[agent-browser]] — Eventual Model B backend for Mark once migration is warranted

## Sources

- /sessions/brave-vigilant-gauss/mnt/Projects--Think Through AI/raw/mark/FULL_PROJECT_CONTEXT.md
- /sessions/brave-vigilant-gauss/mnt/Projects--Think Through AI/raw/mark/PROJECT_INSTRUCTIONS.md
- Hawks, Mercia, Bat Surveys, Mark-Lite SKILL files
