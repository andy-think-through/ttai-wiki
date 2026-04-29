# Belle Agent

> First commercial Agent Browser deployment -- a DOM-selector browser agent automating invoice data entry in Evolution MX for KW Bell.
> Last updated: 2026-04-29

## What It Is

Belle is a browser agent that automates supplier invoice data entry in Evolution MX (EvoMX), KW Bell's cloud-hosted finance system. It is the first Model A deployment -- AI as infrastructure installed inside a client's own system, sold per-client. See [[agent-browser]] for Model A vs Model B framing.

KW Bell's core pain point: OCR processing supplier invoices at ~50% error rate, forcing the finance team to manually verify on a split screen. Belle replaces that manual correction loop with high-accuracy automated data entry.

## Architecture

Belle uses a **DOM-selector architecture** rather than the visual/Computer Use pattern used for Hike. DOM selectors work because EvoMX is standard enterprise SaaS -- no Shadow DOM or React complexity like Hike's cross-origin iframes. This makes Belle cheaper to build than the visual pattern for most enterprise SaaS targets.

Architecture chain: Claude Code -> browser agent -> Evolution MX (cloud-hosted, no public API, network-locked).

**Modular build structure** designed for future scalability across multiple platforms -- the same architecture can be reused for other enterprise SaaS targets where DOM selectors are viable.

## The Name

Naming the agent "Belle" was a deliberate strategy. It shifted Gareth from the mindset of buying software to hiring an employee -- unlocking a 7-skill expansion pipeline beyond the initial invoice automation scope. The name creates a relationship framing that makes ongoing investment feel natural rather than transactional.

## Commercial

- **Initial build:** £3,000 quoted (starting cost)
- **Monthly retainer:** TBD -- Cord flagged: pre-commitment principle says write the target number down before v1 ships
- **Signed off by:** [[gareth-hunt]] (KW Bell FD) on 27 April 2026

## Training Strategy

Phased training approach for reconciliation with comprehensive scenarios (duplicate prevention etc). Gareth coordinating with Payton and team for training data -- video recordings or training manual to feed into AI training.

## Status

Signed off. Build not yet started. Gareth providing training data and coordinating team access.

## Links

- [[kw-bell]] -- client
- [[agent-browser]] -- parent product and technical architecture
- [[consulting]] -- discovered during audit work with KW Bell
- [[gareth-hunt]] -- KW Bell FD, signed off the project
- [[platform-mapping-compounds]] -- why DOM-selector mapping compounds across features once the first is built

## Sources

- Gemini meeting notes: Andy/Gareth catch-up (2026-04-27)
- KW Bell client page wiki history
