# Connectors Beat Computer Use

> Default to structured API/connector access over visual browser automation. Computer Use is a fallback, not the primary path.
> Last updated: 2026-04-16

## The Principle

When building AI agents or autonomous employees, prefer connector-based data access (APIs, MCP servers, structured tool calls) over Computer Use (visual browser automation). Computer Use should be reserved for tasks where no structured alternative exists.

## Where It Was Discovered

Wiki Agent migration from Cowork to Routines (2026-04-15). The old Cowork version used Computer Use (Min browser) to scan Claude.ai conversations -- slow (15-30 min), expensive, and fragile. The Routines version uses Slack and Google Drive connectors -- faster (5-15 min), cheaper, and reliable.

## Where It Applies

- **All TTAI employees:** Slack connector for reporting, Google Drive/Sheets for data, Gmail for email -- not browser scraping
- **Agent Browser product:** The three-layer optimisation roadmap (prompt caching -> deterministic routing -> action caching) is the same principle applied at product level. Layer 2 (deterministic routing) replaces expensive visual interactions with cheaper structured ones.
- **Any agent architecture:** Default to APIs; use Computer Use only when the target has no API or the interaction is genuinely visual

## Evidence

| Approach | Runtime | Reliability | Cost |
|----------|---------|-------------|------|
| Cowork + Computer Use (old Wiki) | 15-30 min | Frequent failures (timeouts, sandbox) | High (screenshot tokens) |
| Routines + Connectors (new Wiki) | 5-15 min | Clean tool calls, no failures | Low |

## Exceptions

- Websites with no API (Betfair UI, some planning portals)
- Tasks that are inherently visual (screenshot analysis, UI testing)
- Exploration of unfamiliar interfaces

## Links

- [[repos-are-employee-memory]] -- Companion principle from the same migration
- [[wiki-agent-SKILL]] -- Employee that proved this principle
- [[browser-agent-arch]] -- Architecture where Computer Use is still the right tool
- [[trust-the-agent-not-dom]] -- Related: when you do use a browser agent, trust the visual agent over DOM scripts

## Sources

- Wiki migration session (2026-04-15)
