# Connectors Beat Computer Use

> Default to API connectors (Slack, Google Drive, Gmail MCP servers) over Computer Use (visual browser automation) for agent information gathering. Computer Use is a fallback, not the default path.
> Last updated: 2026-04-16

## The Principle

When building an AI agent that needs to gather information or interact with external systems, default to structured API connectors. Reserve Computer Use (visual browser automation) for tasks where no API or connector exists.

## Where It Was Discovered

**Wiki Agent migration (2026-04-15).** The old Cowork-based Wiki Agent used Computer Use (Min browser) to scan Claude.ai conversations for new information. Runtime: 15-30 minutes, frequent failures, expensive token usage. The new Routines-based Wiki Agent uses Slack, Google Drive, and GitHub connectors. Runtime: 5-15 minutes, reliable, cheap.

## Evidence

| Metric | Computer Use (old) | Connectors (new) |
|--------|-------------------|-------------------|
| Runtime | 15-30 min | 5-15 min |
| Reliability | Frequent failures (timeouts, element not found) | Clean tool calls |
| Cost | High (vision tokens + multiple screenshots) | Low (structured API calls) |
| Maintainability | Fragile (UI changes break workflows) | Stable (APIs versioned) |

## Where Else It Applies

- **Agent Browser strategy:** The three-layer cost optimisation roadmap (prompt caching -> deterministic routing -> action caching) is the product-level equivalent. Layer 2 (deterministic routing) replaces expensive visual interactions with cheaper structured ones -- same principle.
- **Fred migration:** Fred currently uses Computer Use for Betfair odds fetching. Betfair API would be the connector-first alternative (requires API credentials + IP whitelisting).
- **Any future agent:** If building for a client, check for API/connector availability before defaulting to browser automation.

## Exceptions

Computer Use is still the right choice when:
- No API exists for the target system
- The task requires visual judgment (layout, design, screenshot comparison)
- The interaction is one-off or exploratory (not worth building a connector integration)
- The target system actively blocks API access

## Links

- [[wiki-agent-SKILL]] -- Where this principle was first applied
- [[claude-code-routines]] -- Platform that enables connector-first architecture
- [[browser-agent-arch]] -- Agent Browser architecture (Computer Use is core, but deterministic routing is the connector-first layer)
- [[trust-the-agent-not-dom]] -- Related but distinct: this is about agent vs scripts, not connectors vs Computer Use
- [[cowork-pipeline]] -- Previous platform that relied heavily on Computer Use

## Sources

- Wiki Agent migration session (2026-04-15)
- Andy's Slack ingest message (2026-04-16)
