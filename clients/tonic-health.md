# Tonic Health

> Tonic Health: UK vitamin/supplement brand (now registered in West Sussex) with custom AI agent for competitive intelligence and ad creative generation. Build in progress -- Phase 1 Trustpilot w/c 20 April.
> Last updated: 2026-04-21

## Overview
- **Company:** Tonic Nutrition Ltd (Tonic Health)
- **Shortname:** Tonic Health
- **Product(s):** Custom build (ad creative agent), potential [[knowledge-assistant]]
- **Status:** Build in progress
- **Revenue:** £1,750 invoiced (INV-005, 5 days @ £350/day). Target completion end of w/c 27 April 2026.
- **Registered office (from July 2024):** The Courtyard, Shoreham Road, Upper Beeding, Steyning, West Sussex, BN44 3TN (previously 21 Vardens Road, London SW11 1RQ)
- **Audience:** 1.5M+ followers across platforms, 50M+ monthly organic views; Channel 4 podcast live.

## Key Contacts
- Sunna van Kampen -- Founder/CEO -- (Personal contact; Andy's friend)

## Current Status
Build in progress. The project is a Python-based agent that:
- Scrapes Trustpilot daily for Tonic + 7 competitors
- Analyzes purchase triggers and sentiment patterns
- Maps insights to creative pillars
- Generates 2 ad briefs/day into Notion with Slack notifications

**Technical Stack:**
- Python agent (custom build)
- Apify SASWAVE scraper
- Amazon phase 2 infrastructure
- Estimated running cost: £50--60/month (no retainer)

**Apify issue (17 Apr):** Free $5 monthly platform usage exceeded; all running actors were aborted. Andy will need a paid Apify subscription (or Sunna's account) to continue scraping at production volumes.

**Two Output Layers:**
1. **Insight layer:** What customer reviews reveal about pain points, triggers, and preferences
2. **Creative layer:** Imaginative, non-default ad concepts based on insights

**Competitors Tracked:** Bassetts, Haliborange, Sambucol, Novomins, Chewy Vites, Vitabiotics, Mighty Kids

**Build Architecture:** Apify (SASWAVE Trustpilot scraper, ~$2/1,000 reviews) -> Python orchestration -> Claude API (analysis + creative generation) -> Notion API (output doc) -> Slack webhook (notification). Hosted on Railway. Strategy doc (positioning, 7 insights, 5 pillars) baked in as static context + guardrails. 2 briefs/day.

**Phasing:** Phase 1 Trustpilot only (confirmed reliable; all 521 Tonic reviews pulled in 59 seconds at $1.04). Amazon deferred to Phase 2 -- Axesso required paid sub, WebDataLabs returned broken star ratings. Phase-it principle: ship what works, add fragile sources later.

**Ongoing cost model:** No retainer. Sunna pays Apify (~£30-40/mo), Claude API (~£20/mo), hosting (~£5/mo) directly on her accounts. Andy does ad hoc fixes only.

**Creative quality bar (from Sunna):** Agent must produce genuinely imaginative executions, not data summaries. Example: "two AI agents in a therapy session talking about ADHD" rather than generic founder-to-camera scripts.

## Interaction Log
| Date | Summary |
|------|---------|
| 2026-04-07 | Apify review scraper testing: SASWAVE Trustpilot scraper pulled all 521 Tonic Health reviews ($1.04, 59 seconds). Amazon scrapers failed on free tier (Axesso requires paid sub; WebDataLabs returned broken star ratings). Trustpilot scraper validated as production-ready at ~$2/1,000 reviews. |
| 2026-04-07 | Proposal sent; £1,750 (5 days @ £350) |
| 2026-04-14 | ACCEPTED. Sunna confirmed good to go on costs. First paid build for Tonic. |
| 2026-04-16 | INV-005 issued (£1,750). Build approved; w/c 20 April start, target completion w/c 27 April. Python chosen over n8n (cleaner, cheaper, full control over scraping). Two new principles captured: *test before quoting* and *phase it if a dependency is fragile*. |
| 2026-04-17 | **Apify free usage exceeded.** $5 monthly platform usage limit hit; all running actors aborted. Paid subscription needed to continue production scraping. |
| 2026-04-18 | **Day 2 build complete.** 950 reviews extracted to `tonic.db` via insight-layer JSON schema. Pillar distribution analysis complete -- `proof_conversion` dominates, `brain_focus` only at 0.2%. Diagnosis: **data composition issue, not prompt failure**. Parents of Tonic kids' omega-3 do not self-report "focusing better at school" -- they write about taste and fewer sick days. Decision: **don't re-extract** (re-extract with more aggressive brain_focus prompts would create false positives). brain_focus as a Day-3 creative pillar must be driven by Tonic's positioning doc + the few genuine signals in the data, not by review volume. |
| 2026-04-18 | **Ops lesson -- Claude Code worktrees:** Day 2 Python files (`src/analysis/*`, `config/strategy.yaml`, `scripts/validate_pillar_mapping.py`) were committed to a feature-branch worktree (`.claude/worktrees/clever-bell-74c67b/...`) and not merged to main, so they were invisible in the default working tree. `tonic.db` updated fine (writes work). Before closing a Claude Code session now: merge worktree branches into main with `git log --oneline -10` on main to confirm. [[known-failure-modes]] updated. |
| 2026-04-20 | INV-005 (£1,750) sent to Sunna via email. Andy mentioned he'd made a good start on the build over the weekend. |
| 2026-04-21 | Andy/Sunna catch-up call (30 min, Google Meet, 9:30am). Gemini meeting notes auto-generated. |

## Links
- [[knowledge-assistant]] -- Product: RAG-based staff knowledge chatbot (ideal for Tonic's growing team)
- [[consulting]] -- Service category
- [[mark]] -- potential Mark-Lite application if B2B outreach opportunities emerge
- [[known-failure-modes]] -- Claude Code worktree / main-branch visibility gotcha captured here
- [[sunna-van-kampen]] -- Key contact

## Sources
- raw/ttai/claude.md
- raw/ttai/TTAI_Project_Context.md
- Gmail thread: "Platform usage exceeded" (Apify, 2026-04-17)
- Gmail thread: "Invoice - Ad Creative Agent Build (INV-005)" (2026-04-20)
- Google Calendar: "Catch up" with Sunna (2026-04-21)
