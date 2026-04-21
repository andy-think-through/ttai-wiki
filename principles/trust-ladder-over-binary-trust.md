# Trust Ladder Over Binary Trust

> Don't give full autonomy after one good run. Graduate through stages. Discovered during Mark-Lite v2 safety review.
> Last updated: 2026-04-21

## The Principle

For any employee that communicates with external humans, trust should be graduated through stages rather than flipped from "supervised" to "autonomous" after a single good run. The cost of a bad external communication (wrong email to a live prospect, poorly timed follow-up) is much higher than the friction of approving drafts for a defined period.

## The Mark-Lite Trust Ladder

1. **Drafts-only** for minimum 14 days, 20 reviewed drafts, 90% approval rate
2. **Standard sends** for routine outreach (after explicit GRADUATE command from Andy)
3. **Permanently drafts-only** for: re-engagement emails, prospects Andy has spoken to, adapted copy, warm-reply prospects

Graduation requires explicit command: `GRADUATE MARK-LITE TO SEND MODE`. Never auto-graduates.

## Origin

Mark-Lite v2 safety review (2026-04-21). External review flagged that v1's "first run drafts, second run sends" model was too aggressive for an agent talking to real prospects with money on the line. A bad email to Danny Fordham (Tippercrete) or Paul Saunders (Oakwood Scaffolding) could burn a warm lead permanently.

## Where Else It Applies

- **Any future employee with external-facing communication:** Karen (invoicing emails), Cord (client updates if applicable)
- **[[mark]] onboarding:** Each new Mark client should start in supervised mode regardless of how many previous clients ran smoothly
- **Fred (AutoStrategy):** Bet placement could follow a similar graduated pattern (paper -> small stakes -> full stakes)

## Relationship to Other Principles

- Extends [[position-next-stage-not-bigger-commitment]] to internal operations -- each trust tier is a "next stage"
- Pairs with [[scheduled-tasks-need-zero-intervention]] -- the goal is zero intervention, but you earn it through the ladder

## Links
- [[employee-framework]] -- Framework where this is defined
- [[mark-lite]] -- First implementation
- [[position-next-stage-not-bigger-commitment]] -- Analogous principle in sales

## Sources
- Mark-Lite v2 prompt development (2026-04-21), inbox ingest file
