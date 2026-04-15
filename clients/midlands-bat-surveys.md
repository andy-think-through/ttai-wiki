# Midlands Bat Surveys

> Domestic bat survey service (Mike McSweeney, same person as Hawks Scaffolding). Planning portal monitoring variant of [[mark]]. Agent outreach (architects, planning consultants, building surveyors) + scoped homeowner letter add-on. £500 confirmed, £800 option declined, £300 Stannp add-on pending.
> Last updated: 2026-04-08

## Client Profile

- **Owner/Director:** Mike McSweeney (same person as [[hawks-scaffolding]])
- **Company:** Midlands Bat Surveys
- **Email:** midlandsbarsurveys@gmail.com
- **Business Model:** Domestic bat survey service (Preliminary Roost Assessments) tied to planning applications. Licensed ecologists on staff; delivers work through freelancer network
- **Service Area:** Midlands (West + East)
- **Seasonal:** Year-round (unlike Hawks or Mercia; planning applications are constant)

## Market & Service

**Domestic bat surveys** are required under UK ecology law when planning applications involve work that could disturb potential bat roosting sites. Common triggers:
- Loft conversions (roof void disturbance)
- Barn conversions
- Demolition of outbuildings
- Roof extensions/re-roofing
- Listed building work
- Garage conversions with roof work
- Change of use of agricultural buildings

**Mike's Service Stack:**
- Scopes enquiries from architects/planning consultants/building surveyors
- Deploys licensed freelance ecologists for site visits
- Delivers Preliminary Roost Assessment (PRA) reports
- Goal: Quick turnaround, planning-officer-friendly reports, minimal back-and-forth

## Mark Workflow (Planning Portal Monitoring Variant)

Unlike traditional Mark (which targets fixed prospect lists), Midlands Bat Surveys uses a **discovery-and-outreach** model:

1. Weekly skill searches planning portals for applications likely to trigger bat surveys
2. Identifies the architect/planning consultant firm (the outreach target)
3. Daily skill emails those firms with bat survey offer

This is fundamentally different from [[hawks-scaffolding]] (which finds commercial projects for a single scaffolder).

### Weekly Lead Finding (v1)

**PlanIt Coverage:**
- `auth=469` — West Midlands (32 planning authorities: Birmingham, Coventry, Solihull, Warwick, etc.)
- `auth=468` — East Midlands (40 planning authorities: Derby, Leicester, Nottingham, Northampton, etc.)
- Combined in single query: `auth=469,468`

**Primary Query:**
```
https://www.planit.org.uk/api/applics/json?auth=469,468&recent=7&search=loft+conversion+or+barn+conversion+or+demolition+or+roof+extension+or+re-roofing+or+listed+building+or+outbuilding&pg_sz=500&select=uid,description,address,start_date,area_name,url,app_type,agent_company
```

- Covers entire Midlands in ONE call (no 429 rate limiting)
- Uses JSON endpoint (GeoRSS truncates descriptions)
- `recent=7` for weekly run (returns ~40-60 results)
- `agent_company` field in response identifies architect/planning consultant firm

**Fallback Strategy (if timeout):**
1. Split by region (West + East, 60 seconds apart)
2. If still timing out, break into individual keywords per region (up to 14 calls)
3. Always wait 60+ seconds between API calls (strict 1 req/min rate limit; lockout up to 380 seconds if exceeded)

**Application Filtering:**

| Include | Exclude |
|---|---|
| HFUL (Householder Full Planning) | TCA/TPO/TDD (Tree works) |
| Full (Full Planning) | AOC/Conditions/DOC/DIS/Discharge (Approval/Discharge — dead leads) |
| Heritage/LBC (Listed Building Consent) | SCR (Screening) |
| CLP/CLPD/Outline (Certificate of Lawfulness) | ADV (Advertisement) |
| Amendment (if relevant) | TEL (Telecoms) |
| | AGR (Agricultural unless barn conversion) |

**Critical Gate:** Exclude ALL Conditions/Discharge applications — these are follow-ups where ecology requirements were already discharged in the original permission. Accounts for ~15% of results but are dead leads.

**Non-Domestic Filtering:** Exclude schools, churches, commercial warehouses, retail, offices, local authority/housing association projects unless roof/structure alteration on older buildings.

**Heritage Scrutiny:** Heritage/LBC applications need extra filtering — exclude minor work (window replacements, signage, cosmetic changes). Include only roof alteration, extension, demolition, structural envelope changes, conversions.

### Bat Survey Likelihood Scoring

| Likelihood | Criteria |
|---|---|
| **High** | Barn/agricultural conversion; listed building/conservation area; roof void/attic/loft work; pre-1960s property; demolition of outbuildings; ecology/bat/PRA mentioned in description; ecclesiastical building |
| **Medium** | Loft conversion or roof extension (no high indicators); re-roofing; garage/outbuilding conversion; rural/semi-rural location |
| **Low** | Single-storey rear extension only; new-build on cleared site; modern post-2000 property; internal alterations only |

**Target mix:** 70%+ High/Medium leads.

### Agent Firm Identification & Classification

**Key Finding:** 65% of domestic applications have NO agent (homeowners self-submit). Of 35% with agents:
- ~55% Architects/Architectural Designers — **TARGET (primary)**
- ~15% Planning Consultants — **TARGET (secondary)**
- ~10% Building Surveyors — **TARGET (tertiary)**
- ~20% Non-relevant (sign companies, roofing contractors, suppliers, etc.) — **SKIP**

**Dry Run Finding:** Classification regex missed firms like "Wellspace Architects", "ORMEROD SUTTON ARCHITECTS", "Thomas Wilson Architects" — keyword "architect" or "architectural" anywhere in name (case-insensitive) should classify as Architect/Designer. Ambiguous firms (e.g., "Naylor Sale & Widdows LLP") tag as "Unknown" for manual review.

**Homeowners (No Agent):** Still record in Applications tab with `Agent Firm` = blank. Parked for future Option 2 (physical letters via Stannp). Do NOT contact until that channel is built.

### Daily Outreach (v1)

**Step 0 — Check for Replies (BEFORE DRAFTING)**
Search Gmail for all firms currently in sequence. Read reply content to classify:
- **Replied — Interested** — Engagement, questions, interest in services
- **Replied — Not Interested** — Decline, already have ecologist, want removal
- **Replied — Wrong Contact** — Person no longer at firm or not the right contact

Update Firms tab. Stop all future actions for ANY reply type.

**Step 1 — Select Today's Batch**
Read Daily_Batches tab. Filter rows where Day = today and Status = "Queued" or "In Sequence".

For each firm:
- `Email` (from Firms tab)
- `Contact Name` (first name for greeting)
- `Last Email # Drafted` (determines which template to draft today: # + 1)
- `Applications Found` (references linking firm to relevant applications)
- `Outreach Status`

**Skip if:**
- Firm has replied (any type)
- Email blank
- Last Email # = 3 (sequence complete)

**Step 2 — Enrich Application Context**
Look up applications in Applications tab. Extract:
- Address
- Description
- Bat Survey Likelihood (High/Medium/Low)
- Council

Prefer High likelihood applications. If multiple, pick most compelling (barn conversion > loft conversion > general extension).

**Step 3 — Create Email Drafts**
Use Gmail MCP (`gmail_create_draft`). All drafts are for Mike to review, never auto-sent.

**Pre-Draft Checklist:**
- Greeting uses first name ("Hi Warren,") or "Hi there," if none found
- Under 150 words, plain text, no links/images/HTML
- References specific application firm submitted (address + description)
- Sign-off exactly "Thanks, Mike"
- Subject follows template rotation (A-B-C)
- Tone: Professional, direct, not salesy

### Email Sequence (3 Emails Over 3 Weeks)

**EMAIL 1 (Introduction + Specific Application)** — ~100 words

Subject line rotation (A-B-C):
- A: `Bat survey for your project at [Address/Location]`
- B: `[Address/Location] — might need a bat survey?`
- C: `Quick question about [Address/Location]`

Template:
```
Hi [Name],

I spotted your client's planning application for [brief description, e.g., 
"a loft conversion at 14 Oak Lane, Rugby"] and thought I'd reach out. [One line 
on why it likely needs a bat survey, e.g., "Loft conversions that alter the 
roof void usually need a Preliminary Roost Assessment before the council will 
approve."]

I run a bat survey service covering the Midlands. We've got licensed ecologists 
who can turn around a PRA quickly so it doesn't hold up the planning process 
for your client.

If it's useful, happy to chat or send over a quote.

Thanks,
Mike McSweeney
Bat Survey Midlands
07946 323012
```

**EMAIL 2 (Follow-Up + Value Add)** — ~90 words

Subject: `Following up — bat surveys for your projects`

Template:
```
Hi [Name],

Just a quick follow-up on my email about [Address/Location]. Wanted to check 
if your client still needs a bat survey arranged for that one.

We work with several architects across the Midlands and try to make the ecology 
side as painless as possible — quick site visits, straightforward reports that 
planning officers accept first time, and no drawn-out back and forth.

If you've got any other projects coming up that might need ecology input, 
happy to be a useful contact for those too.

Thanks,
Mike McSweeney
Bat Survey Midlands
07946 323012
```

Alternative if new applications found: Reference new application instead of following up on original.

**EMAIL 3 (Final + Standing Offer)** — ~80 words

Subject: `Last one from me — standing offer for bat surveys`

Template:
```
Hi [Name],

I'll keep this brief — last email from me.

If you ever need a bat survey arranged for a project, I'm a quick call or 
email away. We cover the whole Midlands, our ecologists are licensed and 
experienced, and we know how to produce reports that keep planning officers happy.

No pressure — just wanted to make sure you know we're here if you need us.

Thanks,
Mike McSweeney
Bat Survey Midlands
07946 323012
```

**Language Rules:**

| Always Use | Never Use |
|---|---|
| Your clients, your projects | Your leads, your pipeline |
| Planning applications that need a bat survey | Opportunities, prospects |
| We can help with the ecology side | We provide ecological consultancy services |
| Our ecologists, our surveyors | Our team of qualified professionals |
| Quick turnaround | Efficient delivery |
| Happy to chat | Please don't hesitate to contact us |
| Noticed, spotted | Identified, flagged |
| Looks like it might need a bat survey | May require a Preliminary Roost Assessment |

**Batch Sizing:** 2-3 firms per day (smaller than Northants due to new firm discovery each week and building pipeline gradually).

**Step 4 — Update Tracking Sheet**
- **Firms tab:** Set `Last Email # Drafted`, `Date Email X Drafted`, `Outreach Status` = "In Sequence"
- **Outreach_Log tab:** One row per draft (Firm Name, Email Address, Email #, Subject, Date Drafted, Status = "Drafted", Application Referenced, Notes)
- **Weekly_Batches tab:** Update Status from "Queued" to "In Sequence" (first email) or "Complete" (Email 3)

Upload via rclone back to Google Drive.

**Step 5 — Send Daily Summary to Mike**
**Recipient:** Mcsweeney2013@hotmail.co.uk (Mike's personal email, not business)

Subject: `Mark Daily Summary — [Today's Date, e.g., Monday 25 March 2026]`

Template:
```
Hi Mike,

Here's what Mark did today:

DRAFTS CREATED: [X]
1. [Firm Name] (Email [#])
   Contact: [Contact Name] | [Phone if known, or "No phone on file"]
   Property: [Application Address]
   Project: [Brief description]
   Council: [Council name]

2. [Firm Name] (Email [#])
   ...

[Repeat for each firm]

REPLIES FOUND: [X]
[If any: - [Firm Name]: [Classification] — [Summary]
If none: None today.]

SKIPPED: [X]
[If any: - [Firm Name]: [Reason]
If none: None.]

---
Drafts are in your Gmail — review and send when ready.
```

## Service Pricing & Status

- **Option 1 (Confirmed £500):** Agent outreach only (architects, planning consultants, building surveyors)
- **Option 2 (Declined £800):** Agent outreach + homeowner letter intelligence (for future Stannp add-on)
- **Option 3 (Scoped, not built, £300):** Fully automated physical letter sending to homeowners via Stannp API

**Current Status:** Option 1 fully built and operational. Dry run completed with issues found and fixed. LIVE.

## Tracker Structure

**"Mark Bat Surveys Midlands Tracker"** — 4 tabs:

1. **Applications** — Every qualifying planning application found
   - Columns: Application Ref, Address, Description, Application Type, Council, Bat Survey Likelihood, Likelihood Reason, Agent Firm, Applicant Name (homeowner if found), PlanIt URL, Council Portal URL, Date Found, Status
   
2. **Firms** — Every unique architect/planning consultant firm discovered
   - Columns: Firm Name, Firm Type (Architect/Consultant/Surveyor/Unknown), Contact Name, Email, Phone, Website, LinkedIn, Location, Applications Found, Application Count, Priority (A/B/C), Date Found, Status, Outreach Status, Last Email # Drafted, Notes
   
3. **Outreach_Log** — Every email drafted
   - Columns: Firm Name, Email Address, Email #, Subject Line, Date Drafted, Status, Application Referenced, Notes
   
4. **Weekly_Batches** — Firms assigned to outreach days
   - Columns: Firm Name, Day (Mon-Fri), Week Added (ISO week), Status (Queued/In Sequence/Complete)

## Key Gotchas & Learnings

- **65% no agent:** Homeowners self-submit; these are NOT outreach targets until Option 2 (Stannp) is built
- **Rate limiting strict:** PlanIt API 1 req/min lockout severe (up to 380 seconds). Spacing critical.
- **Conditions applications are dead:** ~15% of results are Discharge/Approval of Conditions. These are already past ecology requirements. Filter aggressively.
- **Heritage needs scrutiny:** Many Heritage/LBC applications are minor cosmetic work. Must filter to roof/structure/conversion only.
- **Contact enrichment critical:** Firms without emails cannot be contacted. Aim for 80%+ enrichment rate for Priority A/B firms.
- **Small batches preferred:** 2-3 per day (not 6-8 like Mark-Lite) due to new firm discovery nature and building sustainable relationships

## Links

- [[mark]] — Managed service model
- [[planit-api]] — Planning portal + API patterns
- [[email-infrastructure]] — Email + domain management

## Sources

- /sessions/brave-vigilant-gauss/mnt/Projects--Think Through AI/raw/mark/Bat Surveys Midlands Skills/mark-bat-surveys-weekly-lead-finding-SKILL.md
- /sessions/brave-vigilant-gauss/mnt/Projects--Think Through AI/raw/mark/Bat Surveys Midlands Skills/mark-bat-surveys-daily-outreach-SKILL.md
- /sessions/brave-vigilant-gauss/mnt/Projects--Think Through AI/raw/mark/FULL_PROJECT_CONTEXT.md
