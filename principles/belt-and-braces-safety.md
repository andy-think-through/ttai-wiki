# Belt and Braces on Safety Mechanisms

> When you have two independent safety mechanisms that don't conflict, keep both. Discovered during Tonic Health build.
> Last updated: 2026-04-21

## The Principle

When building automation with external API costs or irreversible actions, implement redundant safety mechanisms at different layers (server-side + client-side, config + code, hard limit + soft warning). If two independent mechanisms don't conflict, keep both. The one you remove is the one that would have caught the failure.

## Origin

Tonic Health build (2026-04-21). During Vitabiotics Trustpilot scraping, Claude Code caught that the SASWAVE actor was missing a server-side `maxReviews` cap. The client-side Python code had its own limit, but without the server-side parameter, a future SASWAVE actor update that silently drops the maxReviews support would cause runaway spend (~$70 estimated risk for Vitabiotics alone). Both caps were kept: server-side on the Apify actor + client-side in the Python orchestration.

## Where Else It Applies

- **All automation/agent builds with external API costs:** Double-cap pattern (actor-level + orchestration-level).
- **[[betting-portfolio]]:** Stake limits in both the model config and the execution layer.
- **[[mark]]:** Email send limits in both the campaign logic and the Gmail/Outlook layer.
- **Any system where a silent upstream change could cause cascading spend or damage.**

## Links
- [[tonic-health]] -- Origin engagement
- [[known-failure-modes]] -- Operational failure modes collection

## Sources
- Tonic Health build (2026-04-21), inbox ingest file
