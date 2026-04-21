# Phase It If Dependency Fragile

> Split scope at dependency boundaries so fragile integrations don't block the whole project. Discovered during Tonic Health scoping.
> Last updated: 2026-04-21

## The Principle

When a project has both reliable and fragile components, split the scope at the dependency boundary. Deliver the reliable part first at a fixed price. Quote the fragile part separately, or defer it until the dependency is validated. Don't let one broken integration hold up everything.

## Origin

Tonic Health build (2026-04-16). Trustpilot scraping was reliable and tested ($1.04, 521 reviews, 59 seconds). Amazon scraping was fragile (two scrapers tested, both failed on free tier). Rather than bundle both into a single £1,750 quote and risk Amazon blocking delivery, Andy phased the project:
- **Phase 1:** Trustpilot only (£1,750) -- ship now
- **Phase 2:** Amazon (price TBD) -- add later when a working scraper is confirmed

This protected both Andy (didn't commit to undeliverable scope) and Sunna (got working product quickly rather than waiting for everything).

## Where Else It Applies

- **[[mark]] onboarding:** If CRM integration is blocking email sends, launch with a simpler send method first and add CRM integration as a Phase 2.
- **[[mercia-flooring]]:** The Outlook/Entra dependency has blocked the entire Mercia engagement for weeks. Had the project been phased (Phase 1: Gmail send-as, Phase 2: native Outlook), school outreach would already be running.
- **[[agent-browser]]:** Phase KW Bell PoC as invoice OCR first (known workflow), then expand to other EvoMX workflows.

## Relationship to Other Principles

- Paired with [[test-before-quoting]] -- test first, phase if you can't.
- Applies [[position-next-stage-not-bigger-commitment]] to project scoping: each phase is a smaller commitment that builds trust.

## Links
- [[tonic-health]] -- Origin engagement
- [[test-before-quoting]] -- Companion principle
- [[mercia-flooring]] -- Cautionary example of not phasing

## Sources
- Tonic Health build scoping (2026-04-16)
