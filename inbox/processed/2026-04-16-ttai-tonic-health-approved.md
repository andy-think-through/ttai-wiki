# Wiki Ingest: Tonic Health — Agent Build Approved

> Source: ttai conversation
> Date: 2026-04-16
> Packaged by: wiki-ingest skill

---

## Status Changes
- **[[tonic-health]]**: Moved to active build
  - Previous: Proposal sent 7 April, awaiting response
  - Current: Approved. £1,750 build fee confirmed. INV-005 issued. Build starts w/c 20 April, target completion end of w/c 27 April.

## Decisions
- **Tonic agent pricing**: £1,750 one-off (5 days at £350/day), invoiced up-front. No retainer; ad hoc if something breaks.
  - Affects: [[tonic-health]], [[invoicing]]
- **Python over n8n**: Python script chosen for the agent build. Cleaner, cheaper to run, full control over scraping edge cases.
  - Affects: [[tonic-health]], [[tools]]
- **Trustpilot only for Phase 1**: Amazon review scrapers tested and found unreliable (broken star ratings, login walls, low review caps). Trustpilot confirmed working. Amazon deferred to Phase 2.
  - Rationale: Ship something reliable rather than promise something fragile
  - Affects: [[tonic-health]]
- **Apify as scraping platform**: SASWAVE Trustpilot scraper on Apify confirmed as the scraping tool. Sunna pays Apify costs directly.
  - Affects: [[tonic-health]], [[tools]]
- **Ongoing costs on Sunna's accounts**: Apify (~£30-40/mo), Claude API (~£20/mo), hosting (~£5/mo). Total ~£50-60/month. No retainer from Andy.
  - Affects: [[tonic-health]]

## New Data
- **Apify test results (7 April)**: Axesso Amazon scraper failed on free tier (requires separate paid sub). WebDataLabs returned 5 reviews with broken star ratings and verified purchase fields. SASWAVE Trustpilot scraper pulled all 521 Tonic Health reviews in 59 seconds at $1.04 cost. Trustpilot data quality excellent.
  - Affects: [[tonic-health]], [[tools]]
- **Invoice tracker update**: INV-003 = Mercia (Mark retainer, April). INV-004 = JDW Brickwork (Mark build). INV-005 = Tonic Nutrition Ltd (agent build, £1,750).
  - Affects: [[invoicing]]
- **Tonic Nutrition Ltd registered office**: Moved from 21 Vardens Road, London SW11 1RQ to The Courtyard, Shoreham Road, Upper Beeding, Steyning, West Sussex, BN44 3TN (July 2024).
  - Affects: [[tonic-health]]
- **Tonic social following**: Now 1.5M+ followers across platforms, 50M+ monthly organic views. Channel 4 podcast launched.
  - Affects: [[tonic-health]]

## New Principles / Learnings
- **Test before quoting**: Scraping reliability varies wildly between platforms and tools. Always run a live test scrape before committing to a price on any build that depends on scraping.
  - Discovered in: Tonic Health agent scoping
  - Likely applies to: Any future agent build with external data dependencies
  - Evidence: Two Amazon scrapers failed or returned broken data; would have been a nasty surprise mid-build if not tested in advance.
- **Phase it if a dependency is fragile**: When part of a build relies on unreliable infrastructure, ship without it and add as Phase 2 rather than promising something fragile.
  - Discovered in: Tonic Health agent scoping (Amazon scrapers)
  - Likely applies to: Any multi-source agent build
  - Evidence: Framing Amazon as Phase 2 de-risked the quote and created a natural upsell.

## Product / Methodology Changes
- **Tonic ad creative agent architecture**: Apify (scraping) > Python script (orchestration) > Claude API (analysis + creative generation) > Notion API (output) > Slack webhook (notification). Hosted on Railway or similar.
  - Detail: Strategy doc (positioning, 7 insights, 5 pillars) baked into agent as static context and guardrails. Agent maps review insights to pillars and generates two-layer output: insight layer (what reviews reveal) + creative layer (imaginative ad concepts grounded in review language). Entry point doc structure used as output template. 2 briefs/day.
  - Affects: [[tonic-health]]
- **Sunna's creative quality bar**: Agent must produce genuinely creative ad executions, not just data summaries. Example from Sunna: "two AI agents in a therapy session talking about ADHD" rather than generic founder-to-camera scripts.
  - Affects: [[tonic-health]]

## New Contacts / Relationships
- **JDW Brickwork**: New Mark client (INV-004 issued for Mark build)
  - Linked to: [[mark]]

## Raw Context
This was a long scoping conversation covering Sunna's initial voicenote request through to approved proposal. Andy studied Tonic's internal strategy docs (Kids Omega Ad Creative Strategy + Emotional Entry Point test framework) to understand how the agent output should be structured. The WhatsApp messaging style with Sunna was refined during this conversation and saved to global memory. Tonic's head of ops had tried to build something similar themselves but couldn't; Sunna explicitly said "I know Andy, and Andy is good."

---

## Suggested Wiki Pages Affected
- [[tonic-health]] — full status update, architecture, pricing, timeline, registered office change
- [[invoicing]] — add INV-003, INV-004, INV-005
- [[tools]] — add Apify (SASWAVE Trustpilot scraper confirmed), note Amazon scraper limitations
- [[principles]] — add "test before quoting" and "phase it if a dependency is fragile"
- [NEW: jdw-brickwork] — new Mark client
