# Tonic Health

> Tonic Health: Series A UK vitamin/supplement brand (London SW11) with custom AI agent for competitive intelligence and ad creative generation.
> Last updated: 2026-04-14

## Overview
- **Company:** Tonic Nutrition Ltd (Tonic Health)
- **Shortname:** Tonic Health
- **Product(s):** Custom build (ad creative agent), potential [[knowledge-assistant]]
- **Status:** Accepted — build starting
- **Revenue:** £1,750 accepted (5 days @ £350/day). INV-003 pending issue.

## Key Contacts
- Sunna van Kampen — Founder/CEO — (Personal contact; Andy's friend)

## Current Status
Proposal sent 7 April. The project is a Python-based agent that:
- Scrapes Trustpilot daily for Tonic + 7 competitors
- Analyzes purchase triggers and sentiment patterns
- Maps insights to creative pillars
- Generates 2 ad briefs/day into Notion with Slack notifications

**Technical Stack:**
- Python agent (custom build)
- Apify SASWAVE scraper
- Amazon phase 2 infrastructure
- Estimated running cost: £50–60/month (no retainer)

**Two Output Layers:**
1. **Insight layer:** What customer reviews reveal about pain points, triggers, and preferences
2. **Creative layer:** Imaginative, non-default ad concepts based on insights

**Competitors Tracked:** Bassetts, Haliborange, Sambucol, Novomins, Chewy Vites, Vitabiotics, Mighty Kids

**Next Action:** Issue INV-003 (£1,750). Confirm Apify / Claude API / Notion access with Sunna, then kick off build.

## Interaction Log
| Date | Summary |
|------|---------|
| 2026-04-07 | Apify review scraper testing: SASWAVE Trustpilot scraper pulled all 521 Tonic Health reviews ($1.04, 59 seconds). Amazon scrapers failed on free tier (Axesso requires paid sub; WebDataLabs returned broken star ratings). Trustpilot scraper validated as production-ready at ~$2/1,000 reviews. |
| 2026-04-07 | Proposal sent; £1,750 (5 days @ £350) |
| 2026-04-14 | ACCEPTED. Sunna confirmed good to go on costs. First paid build for Tonic. INV-003 to be issued; need Apify / Claude API / Notion access from Sunna to start. |

## Links
- [[knowledge-assistant]] — Product: RAG-based staff knowledge chatbot (ideal for Tonic's growing team)
- [[consulting]] — Service category
- [[mark]] — potential Mark-Lite application if B2B outreach opportunities emerge

## Sources
- raw/ttai/claude.md
- raw/ttai/TTAI_Project_Context.md
