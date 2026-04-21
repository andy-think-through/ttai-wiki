# Research Spikes Before Scrapers

> Run a cheap manual research spike before building an automated scraper. Discovered during Tonic Health build.
> Last updated: 2026-04-21

## The Principle

Before investing engineering time in a scraper or automated data pipeline, spend 20 minutes doing the research manually in a browser. If the manual spike produces actionable insight, you've validated the source. If it doesn't, you've saved days of build time. Either way, the spike itself often produces the most valuable deliverable.

## Origin

Tonic Health build (2026-04-21). Two research spikes:
1. **Reddit brand-discussion spike** ($0, 20 mins): Killed the Reddit scraper idea immediately. Forum discussions about supplements are fragmented, gated behind community rules, and platforms actively resist scraping. The 20-minute manual browse produced more useful signal than a scraper would have in 6 months.
2. **Parenting pain research spike** (2x20 mins, two independent runs): Reshaped the entire creative layer. Discovered that forum language is ad-hook language while review language is landing-page language. The resulting pain taxonomy (market_psychology.yaml) became a standalone strategic deliverable.

## Where Else It Applies

- **[[mark]] onboarding:** Before building a lead-finding pipeline for a new trade, manually search planning portals for 20 minutes. If the trade doesn't appear, no amount of automation will fix it (see [[planning-data-serves-site-trades]]).
- **Any TTAI project involving external data sources:** Default to "manual spike first" before committing to scraper/API integration.
- **[[agent-browser]]:** Before automating a workflow, manually walk through the UI to identify blockers.

## Relationship to Other Principles

- Extends [[test-before-quoting]] -- the spike IS the test, done before any engineering commitment.
- Mirrors [[selectivity-is-everything]] -- be selective about what you automate.

## Links
- [[tonic-health]] -- Origin engagement
- [[test-before-quoting]] -- Related principle
- [[planning-data-serves-site-trades]] -- Example of where manual research would have flagged the issue

## Sources
- Tonic Health build (2026-04-21), inbox ingest file
