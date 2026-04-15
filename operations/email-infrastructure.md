# Email Infrastructure

> Email systems, validation, warm-up, and integration patterns used across Mark projects. Covers Lemwarm, Hunter.io, Gmail/Outlook MCPs, email validation, domain reputation.
> Last updated: 2026-04-08

## Overview

Mark operates multiple email sending domains (one per client or service). Email success depends on:

1. **Domain Reputation** — New domains start cold; warm-up is essential
2. **Validation** — Don't send to invalid/bouncy addresses
3. **Integration** — Use Gmail MCP (preferred) or Outlook MCP for draft creation
4. **Tracking** — Distinguish sent vs. skipped addresses; monitor reply patterns

## Email Domains in Use

| Domain | Service | Client | Status | Warm-up Service |
|---|---|---|---|---|
| mark@merciafloors.co.uk | Mercia Flooring outreach | Mercia Flooring | Pre-launch (go-live 15 April) | Lemwarm |
| midlandsbarsurveys@gmail.com | Bat Survey outreach | Midlands Bat Surveys | Live | — (Gmail native) |
| hawkscaffolding@outlook.com | Hawks Scaffolding outreach | Hawks Scaffolding | Live | — (Outlook native) |
| [Andy's personal Gmail] | Mark-Lite Northants outreach | Mark-Lite Northants | Live | — (Gmail native) |

## Email Warm-Up (Lemwarm)

### Purpose
New sending domains have zero reputation. ISPs and Gmail flag them as spam initially. **Lemwarm** gradually builds reputation by:
- Sending warm-up emails to engaged, known addresses
- Monitoring open rates, reply rates, forwarding behavior
- Increasing send volume as reputation improves
- Bypassing spam filters for client's real outreach

### Setup for Mercia Flooring (mark@merciafloors.co.uk)

- Domain: mark@merciafloors.co.uk
- Service: Lemwarm
- Status: Pending Outlook admin access (Martin at Solaas IT)
- Warm-up schedule: [Lemwarm manages; typically 10-20 days before sending real campaigns]

### When Warm-Up is NOT Needed

- **Gmail domains** (Gmail's own infrastructure has strong reputation; new addresses are "trusted" by default)
- **Outlook domains** (Microsoft's infrastructure similarly trusted)
- **Established domains** (if domain has prior sending history)

## Email Validation

### Why Validation Matters

Sending to invalid addresses:
- Bounces back (mail delivery failure)
- Hurts sender reputation (ISPs see high bounce rate = spam indicator)
- Wastes credit/infrastructure
- Looks unprofessional to client

**Target:** Validate 100% of outreach addresses before sending. Never guess or fabricate.

### Validation Methods (Priority Order)

**Method 1: Hunter.io (Preferred)**
- Free tier: 25-50 verifications/month
- API: POST with email address, receive validity status
- Result codes: VALID, RISKY (catch-all domain), INVALID, UNKNOWN
- Recommendation: Use VALID and RISKY; skip INVALID

**Method 2: ZeroBounce**
- Free tier: 100 verifications/month
- Similar result codes
- Good fallback if Hunter quota exhausted

**Method 3: NeverBounce**
- Free tier: 1,000 verifications for new accounts
- Larger bulk; good for bigger campaigns
- Slightly slower API

**Method 4: Fallback — SMTP Validation (Python)**
- Check MX records for domain
- Attempt SMTP conversation (without sending)
- Identifies if mailbox accepts mail
- NOT website-based; less reliable for catch-alls

**Method 5: Website Verification**
- Visit prospect's website homepage, footer, contact page
- Find published email address
- Use that address over guessed patterns
- Example: If website shows `enquiries@example.co.uk`, use that (don't guess `info@`)

### Validation Workflow for Mark Skills

1. **Before drafting any email:** Extract prospect email from tracker
2. **Run validation:** Hunter.io > ZeroBounce > NeverBounce > SMTP check
3. **Mark result:** Domain VALID, RISKY, INVALID, or UNKNOWN in Companies tab
4. **Send only VALID/RISKY:** Skip INVALID addresses entirely
5. **Log:** Outreach_Log tab notes any skipped addresses (e.g., "Email validation failed: INVALID domain")
6. **Report:** Final report includes validation summary (total validated, valid/risky/invalid counts)

### Common Invalid Patterns

- Domain doesn't exist (NXDOMAIN)
- Email address doesn't exist but domain does (bounce)
- Catch-all domain that doesn't actually receive mail
- Typos in address (e.g., `info@compny.co.uk` instead of `company`)
- Outdated email (contact has left company; address closed)

## Gmail MCP Integration

### Platforms

- **Manus:** `manus-mcp-cli tool call gmail_create_draft` or `gmail_send_messages` (with `draft: true`)
- **Claude/Cowork:** `mcp__a6be9123-c551-4744-a331-b9a95905c567__gmail_create_draft`

### Capabilities

- **Create drafts** (no auto-send) — emails appear in user's Drafts folder for review + manual send
- **Search messages** — find replies from specific domains or senders
- **Get profile** — retrieve authenticated Gmail account info

### Usage Patterns in Mark

**Step 1: Check for Replies**
```bash
manus-mcp-cli tool call gmail_search_messages --server gmail --input '{
  "query": "from:(@domain1.co.uk OR @domain2.co.uk OR @domain3.com)",
  "maxResults": 50
}'
```

**Step 2: Create Drafts**
```bash
manus-mcp-cli tool call gmail_create_draft --server gmail --input '{
  "to": "prospect@example.co.uk",
  "subject": "Subject line",
  "body": "Email body text"
}'
```

Or (if only send_messages available, with draft flag):
```bash
manus-mcp-cli tool call gmail_send_messages --server gmail --input '{
  "messages": [{"to": ["prospect@example.co.uk"], "subject": "Subject", "content": "Body", "draft": true}]
}'
```

### Important Notes

- **Drafts, not sends:** Always use `draft: true` when calling send_messages
- **Batch drafts:** Create all drafts for the day's batch in one API call (not per-prospect)
- **Reply checking:** Search before drafting to avoid re-emailing prospects who replied
- **Domain:** Drafts created via authenticated Gmail account (e.g., midlandsbarsurveys@gmail.com for Bat Surveys)

## Outlook MCP Integration (Pending for Mercia)

### Status

- **Outlook account:** mark@merciafloors.co.uk (created, being warmed via Lemwarm)
- **OAuth access:** Pending Martin at Solaas IT (Peter's IT company) admin consent
- **Expected capabilities:** Similar to Gmail MCP (draft creation, search, etc.)

### Gotcha

- Outlook requires admin-level OAuth approval for third-party apps
- Martin must grant consent before Manus can access mark@merciafloors.co.uk
- Timeline: Wait for Martin's response; cannot proceed with Mercia outreach until granted

## Subject Line Patterns

### A-B-C Rotation (Mark-Lite)

**Purpose:** Avoid "looks automated" fatigue. Change subject format across prospects in same batch.

**Strict Rotation (not random):**
- Prospect 1 gets Format A
- Prospect 2 gets Format B
- Prospect 3 gets Format C
- Prospect 4 gets Format A (cycle repeats)

**Example (Northants Email 1):**
- A: `Spotted this for you — [Project], [Town]`
- B: `[Project], [Town] — could be relevant for you`
- C: `New [trade] work near you — [Project]`

Prospects on same day get different formats (Tuesday has 8 prospects, so they'd get A-B-C-A-B-C-A-B).

### Bat Surveys Email 1 Rotation

- A: `Bat survey for your project at [Address/Location]`
- B: `[Address/Location] — might need a bat survey?`
- C: `Quick question about [Address/Location]`

## Reply Handling

### Classification

**Warm reply:**
- Engagement, questions, asks for more info
- Update tracker: "Replied — Warm"
- Add flag: `ACTION: Manual follow-up needed — [reason]`
- Action: Andy's team reaches out manually (client call, detailed proposal, etc.)

**Opted out:**
- "Stop emailing", "not interested", "remove from list"
- Update tracker: "Replied — Opted Out"
- Action: Stop all future emails to this prospect immediately

**Wrong contact:**
- "I've left the company", "this person doesn't work here anymore"
- Update tracker: "Replied — Wrong Contact"
- Add notes: New contact info if provided
- Action: Research correct contact and potentially re-reach with right person

### Never Re-Email Opted Outs

**Guardrail:** Once a prospect's Email Status is "Replied — Opted Out", skip them in all future daily outreach runs, even if a day comes up where they'd normally be scheduled.

## Email Copy Guardrails

### Never

- **Rewrite locked copy** — Email 3 Mark paragraph (Northants) is verbatim locked. Client templates (Mercia) are locked. Never "improve" without approval.
- **Fabricate addresses** — If not found via Hunter/website, leave blank. Don't guess patterns.
- **Send before validation** — MX/Hunter check BEFORE drafting. Skipped = logged in tracker, not sent.
- **Use outdated email** — Refresh contact enrichment periodically (Mercia: every 6-8 weeks; Northants: weekly for new leads)
- **Over-personalise** — Stick to specified placeholders. Don't add extra sentences.

### Always

- **Use first names** — "Hi Josh," not "Hi there," (unless no name found)
- **Plain text** — No HTML formatting, images, fancy fonts
- **Under word limit** — Email 1 ~65 words, Email 2 ~75, Email 3 ~100, Email 4 ~80
- **Package language** — Trade-speak not planning-speak
- **Sign-off exactly** — "Thanks, Andy" or "Thanks, Mike McSweeney" (client's name, not generic)

## Bounce Rate Monitoring

### Target

- **Bounce rate:** <5% (across all clients)
- **Valid delivery:** >95% of sent emails reach the inbox

### Tracking

- Outreach_Log tab includes Status column (Drafted, Sent, Bounced, Delivered, Replied)
- Post-campaign: Andy reviews Gmail activity (bounces, unsubscribes, spam reports) and updates tracker

### If Bounce Rate High

1. Check domain reputation (use MXToolbox, Google Postmaster Tools)
2. Verify Lemwarm is running (if new domain)
3. Audit prospect list for quality (validation may have been skipped)
4. Check email copy for spam triggers (all-caps, multiple exclamation marks, suspicious links)

## Links

- [[mark]] — Managed service using email infrastructure
- [[mark-lite]] — Direct outreach service using email
- [[planit-api]] — Parallel data source (not email, but same infrastructure)

## Sources

- /sessions/brave-vigilant-gauss/mnt/Projects--Think Through AI/raw/mark/FULL_PROJECT_CONTEXT.md
- Mark SKILL files (Hawks, Mercia, Bat Surveys, Mark-Lite Northants)
