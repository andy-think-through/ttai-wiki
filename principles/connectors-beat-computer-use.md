# Principle: Connectors Beat Computer Use

> Default to API connectors (MCP servers, SDKs, direct API calls) over browser automation (Computer Use). Computer Use is the fallback, not the primary path.
> Last updated: 2026-04-16

## The Principle

When building agents that need to gather or act on external data, use structured connectors (APIs, MCP servers, database queries) as the default path. Reserve Computer Use / browser automation for situations where no connector exists or as a fallback when connectors fail.

## Where It Was Discovered

**Wiki Agent migration (2026-04-15):** The old Cowork-based Wiki Agent used Computer Use with Min browser to scan Claude.ai conversation histories -- 15-30 minute runtime, frequent browser timeouts, sandbox restrictions, fragile screenshot parsing. The Routines-based replacement uses Slack MCP connector + GitHub repo access -- 5-15 minute runtime, no browser, clean structured data, zero failures on first run.

## Evidence

| Metric | Computer Use (Cowork) | Connectors (Routines) |
|--------|----------------------|----------------------|
| Runtime | 15-30 minutes | 5-15 minutes |
| Failure rate | Frequent (timeouts, sandbox) | Zero on first run |
| Data quality | Screenshot parsing, lossy | Structured JSON, lossless |
| Cost | Computer Use tokens + session overhead | Tool call tokens only |
| Reliability | Depends on browser state, login sessions | Stateless, deterministic |

## Where Else It Applies

- **Agent Browser strategy:** Computer Use is powerful but expensive. The three-layer optimisation roadmap (prompt caching → deterministic routing → action caching) is really about reducing Computer Use dependency. Where a connector or API exists, use it.
- **Fred (AutoStrategy):** Fred's SKILL currently specifies Computer Use for Betfair odds. If Betfair API access is obtained, that entire Computer Use dependency disappears. Same principle.
- **Mark-Lite:** Email sending via Gmail MCP connector vs browser-based email composition. Connector is faster, more reliable, and auditable.
- **Any future agent architecture:** When advising clients on agent design, default recommendation should be: connectors first, Computer Use for the gap.

## Relationship to Other Principles

- Extends [[trust-the-agent-not-dom]] -- both are about choosing the right abstraction layer, but this principle is broader (not just DOM vs visual agent, but structured API vs any browser interaction)
- Supports [[scheduled-tasks-need-zero-intervention]] -- connectors are more reliable than browser automation, reducing the chance of a scheduled task failing and needing human intervention

## Exceptions

- No API or connector exists for the target system (some legacy web apps, some internal tools)
- The connector is rate-limited or incomplete (e.g., a partial API that doesn't expose the needed endpoint)
- Exploration/research tasks where browsing is the point (e.g., checking competitor websites, visual verification)

## Sources

- Wiki Agent migration conversation (2026-04-15)
- Ingest file: 2026-04-16-wiki-agent-migration-routines-slack-bridge.md
