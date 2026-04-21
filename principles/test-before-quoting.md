# Test Before Quoting

> Validate fragile dependencies before pricing a project. Discovered during Tonic Health scoping.
> Last updated: 2026-04-21

## The Principle

Before quoting a fixed price for a project that depends on external tools, APIs, or integrations, test those dependencies first. If a dependency doesn't work (or works differently than assumed), the scope and cost change fundamentally. Quoting before testing means either eating the cost difference or renegotiating -- both bad.

## Origin

Tonic Health build (2026-04-16). The project required Apify scrapers for Trustpilot and Amazon reviews. Trustpilot worked perfectly ($1.04, 59 seconds for 521 reviews). Amazon scrapers failed -- Axesso required a paid subscription, WebDataLabs returned broken star ratings. Had Andy quoted a single fixed price for both Trustpilot + Amazon, the Amazon failure would have blown the scope.

Instead, the project was phased: Phase 1 (Trustpilot only, confirmed working) at £1,750, with Amazon deferred to Phase 2. This kept the quote honest and the delivery achievable.

## Where Else It Applies

- **[[mark]] onboarding:** Test the email/CRM integration (Outlook, Gmail, Manus) before committing to a go-live date. Mercia Flooring's Outlook/Entra block is the cautionary tale.
- **[[agent-browser]] PoC:** Test EvoMX access and DOM structure before quoting the KW Bell solution design.
- **Any consulting engagement with integration dependencies:** Default to phasing if you can't test upfront.

## Relationship to Other Principles

- Paired with [[phase-it-if-dependency-fragile]] -- if you can't test, at least scope the fragile part separately.
- Applies [[selectivity-is-everything]] to scoping: be selective about what you commit to at a fixed price.

## Links
- [[tonic-health]] -- Origin engagement
- [[phase-it-if-dependency-fragile]] -- Companion principle
- [[mercia-flooring]] -- Counter-example: dependency wasn't tested before go-live was scheduled

## Sources
- Tonic Health build scoping (2026-04-16)
