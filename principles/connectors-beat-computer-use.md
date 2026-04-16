# Connectors Beat Computer Use

> Default to structured connectors (APIs, MCP tools, Slack connector, Google Drive) over visual browser automation. Computer Use is a fallback, not the primary path.
> Last updated: 2026-04-16

## The Principle

When building autonomous agents, always prefer connector-based data access (Slack MCP, Google Sheets API, filesystem reads) over Computer Use (visual browser automation). Computer Use is slower, more expensive, more fragile, and harder to debug. Reserve it for situations where no structured interface exists.

## Where It Was Discovered

**Wiki Agent migration (2026-04-15).** The old Cowork-based Wiki scanned Claude.ai conversations via Computer Use (Min browser). Runtime was 15-30 minutes with frequent failures. The Routines version uses Slack connector + inbox folder + Google Drive connectors -- runtime dropped to 5-15 minutes with clean, reliable tool calls.

## Where Else It Applies

- **Agent Browser optimisation roadmap:** The three-layer cost reduction plan (prompt caching -> deterministic routing -> action caching) follows the same gradient. Layer 2 (deterministic routing) is essentially "use structured paths instead of visual ones where possible." This principle argues for accelerating Layer 2.
- **Fred migration:** Fred currently uses Computer Use for Betfair odds fetching. Betfair API access would be the connector-first equivalent -- faster, cheaper, more reliable.
- **Mark-Lite migration:** Mark-Lite uses Computer Use for website research. Google Search API or structured data sources would be preferable where available.
- **Any future TTAI employee:** Default architecture should be connectors, with Computer Use as the exception path.

## Evidence

| Metric | Computer Use (Cowork) | Connectors (Routines) |
|--------|----------------------|----------------------|
| Runtime | 15-30 min | 5-15 min |
| Failure rate | Frequent (timeouts, UI changes) | Rare (structured responses) |
| Cost | Higher (vision tokens, retries) | Lower (text-only tool calls) |
| Debuggability | Hard (screenshots, DOM state) | Easy (structured JSON responses) |

## Exceptions

- **No API exists:** Some tools only have a web UI. Computer Use is the right choice here.
- **Visual verification:** Sometimes you need to see what a human sees (e.g., checking a website's layout, verifying a rendered page).
- **Exploration of unknown interfaces:** When you don't yet know what structured data is available, visual browsing is a reasonable discovery method.

## Cross-Validates

- [[trust-the-agent-not-dom]] -- Both principles argue against fighting with web interfaces when better paths exist. "Trust the agent" says use the visual agent when you must interact with UIs; "connectors beat Computer Use" says avoid UIs entirely when structured alternatives exist.
- [[scheduled-tasks-need-zero-intervention]] -- Connectors are more reliable for unattended operation than visual automation.

## Links

- [[wiki-agent-SKILL]] -- Primary evidence source
- [[claude-code-routines]] -- Platform that enables connector-first architecture
- [[employee-framework]] -- All employees inherit this principle
- [[trust-the-agent-not-dom]] -- Related principle (visual agent vs DOM scripts)

## Sources

- Wiki Agent migration session (2026-04-15)
- Wiki ingest file: "Wiki Agent Migrated to Routines + Slack Bridge Deployed"
