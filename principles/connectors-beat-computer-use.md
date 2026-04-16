# Connectors Beat Computer Use

> Default to structured API connectors over visual browser automation. Computer Use is a fallback, not the default path.
> Last updated: 2026-04-16

## The Principle

When building AI agents or autonomous employees, default to API-based connectors (Slack MCP, Google Drive, GitHub) for information gathering and action. Use Computer Use (visual browser automation) only as a fallback for tasks where no structured API exists.

## Where It Was Discovered

**Wiki Agent migration (2026-04-15).** The old Cowork version of Wiki used Computer Use (Min browser) to scan Claude.ai conversations -- 15-30 minute runtime, frequent failures, expensive tokens. The Routines version uses Slack + inbox connectors -- 5-15 minute runtime, reliable, standard API cost.

## Evidence

| Metric | Computer Use (Cowork) | Connectors (Routines) |
|--------|----------------------|----------------------|
| Runtime | 15-30 min | 5-15 min |
| Failure rate | Frequent (timeouts, login issues) | Rare |
| Token cost | High (vision + interaction tokens) | Standard |
| Reliability | Brittle (UI changes break automation) | Stable (APIs are versioned) |

## Where Else It Applies

- **Agent Browser product:** The three-layer optimisation roadmap (prompt caching -> deterministic routing -> action caching) is the product equivalent. Layer 2 (deterministic routing) replaces visual interactions with structured ones where possible.
- **Fred migration:** Fred currently uses Computer Use for Betfair odds. Where possible, structured data sources should replace visual scraping.
- **Mark-Lite migration:** Email sending via Gmail MCP connector, not browser-based email composition.
- **Any future TTAI employee:** Connector-first architecture should be the default.

## Exceptions

Computer Use remains necessary when:
- No API exists (e.g., Betfair Exchange has limited free API access)
- The task requires visual verification (e.g., checking how a webpage renders)
- Exploring unfamiliar territory where structured access hasn't been set up yet

## Cross-References

- [[trust-the-agent-not-dom]] -- Related but different: that principle says the visual agent beats custom DOM scripts. This principle says structured connectors beat the visual agent. The hierarchy is: connectors > visual agent > custom scripts.
- [[scheduled-tasks-need-zero-intervention]] -- Connector-first architecture supports zero-intervention goals (fewer failure modes).

## Links

- [[wiki-agent-SKILL]] -- Primary evidence source
- [[claude-code-routines]] -- Platform enabling connector-first architecture
- [[employee-framework]] -- Universal employee model
- [[trust-the-agent-not-dom]] -- Related principle (different layer)

## Sources

- Wiki Agent migration session (2026-04-15)
