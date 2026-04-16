# Principle: Connectors Beat Computer Use

> Default to structured connectors (APIs, MCP tools) over visual browser automation. Computer Use is a fallback, not the primary path.
> Last updated: 2026-04-16

## The Principle

When building AI agents or autonomous employees, use structured data connectors (Slack MCP, Google Drive API, Gmail connector) as the default access method. Reserve Computer Use (visual browser automation) for situations where no structured access exists.

## Where It Was Discovered

**Wiki Agent migration (2026-04-15).** The old Cowork version used Computer Use to scan Claude.ai conversations via Min browser -- 15-30 minute runtime, frequent timeouts, fragile. The Routines version uses Slack + Google Drive + inbox folder connectors -- 5-15 minute runtime, no browser, clean tool calls.

## Where Else It Applies

- **Agent Browser product:** The three-layer cost optimisation roadmap (prompt caching -> deterministic routing -> action caching) is the product equivalent. Layer 2 (deterministic routing) replaces expensive visual interactions with cheaper structured ones.
- **Fred migration:** Fred's Cowork pipeline uses Computer Use for Betfair odds. Migration to Routines should explore API-first alternatives.
- **Any new employee:** Start with connectors. Only add Computer Use if structured access doesn't exist for a required data source.

## Evidence

| Metric | Cowork + Computer Use | Routines + Connectors |
|--------|----------------------|----------------------|
| Runtime | 15-30 min | 5-15 min |
| Failure rate | Frequent (timeouts, sandbox) | Rare |
| Cost per run | Higher (Computer Use tokens) | Lower |
| Reliability | Fragile | Robust |

## Exceptions

- Websites with no API (some betting exchanges, planning portals)
- Tasks requiring visual verification (screenshot comparison, UI testing)
- Exploration of unfamiliar tools where the UI is the only documentation

## Links

- [[wiki-agent-SKILL]] -- Where this principle was proven
- [[claude-code-routines]] -- Platform that enables connector-first access
- [[trust-the-agent-not-dom]] -- Related but different: when you must use a browser, trust the visual agent over custom DOM scripts
- [[employee-framework]] -- Universal operating model

## Sources

- Wiki Agent migration session (2026-04-15)
