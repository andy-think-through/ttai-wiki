# Connectors Beat Computer Use

> Default to API-based connectors (Slack MCP, Gmail MCP, Google Drive) over visual browser automation. Computer Use is the fallback, not the primary path.
> Last updated: 2026-04-16

## The Principle

When building autonomous agents, use structured API connectors as the default data access method. Visual browser automation (Computer Use) should be reserved for tasks where no API or connector exists.

## Where It Was Discovered

Wiki Agent migration from Cowork to [[claude-code-routines]] (April 2026). The old Cowork version used Computer Use (Min browser) to scan Claude.ai conversations -- 15-30 minute runtime, frequent browser timeouts, fragile selectors. The Routines version uses Slack, Gmail, and Google Drive connectors -- 5-15 minute runtime, no browser, clean tool calls.

## Evidence

| Metric | Computer Use (Cowork) | Connectors (Routines) |
|--------|----------------------|----------------------|
| Runtime | 15-30 min | 5-15 min |
| Failure rate | Frequent (timeouts, selectors) | Rare (structured responses) |
| Cost | Higher (vision tokens) | Lower (text-only) |
| Reliability | Fragile | Robust |

## Where Else It Applies

- **[[agent-browser]]** -- The three-layer optimisation roadmap (prompt caching -> deterministic routing -> action caching) is this same principle applied to a product. Layer 2 (deterministic routing) replaces expensive visual interactions with cheaper structured ones.
- **Fred migration** -- Fred's Cowork version uses Computer Use for Betfair. Betfair API would be the connector equivalent (blocked by IP whitelisting requirements).
- **Any agent design** -- Default architecture should be: connector first, Computer Use as fallback for tasks without API coverage.

## Exceptions

- Tasks requiring genuine visual understanding (layout analysis, screenshot verification)
- Platforms with no API and no structured data export
- Exploration/discovery tasks where the visual context helps the agent make decisions

## Cross-References

- [[trust-the-agent-not-dom]] -- Related but distinct. That principle says the visual agent beats custom DOM scripts. This principle says structured connectors beat the visual agent. Together: connectors > visual agent > custom scripts.
- [[repos-are-employee-memory]] -- Companion infrastructure principle from the same migration.
- [[scheduled-tasks-need-zero-intervention]] -- Connectors are more reliable for unattended operation than Computer Use.

## Sources

- Wiki ingest: "Wiki Agent Migrated to Routines + Slack Bridge Deployed" (2026-04-15)
