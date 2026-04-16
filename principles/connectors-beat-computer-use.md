# Principle: Connectors Beat Computer Use

> When gathering information for automated agents, connector-based tools (APIs, MCP servers, filesystem) are faster, cheaper, and more reliable than browser automation via Computer Use.
> Last updated: 2026-04-16

## The Principle

**Use Computer Use as a fallback, not the default path.** If a connector exists for the information source (Slack, Google Drive, Gmail, GitHub), use it. Reserve Computer Use for tasks that genuinely require visual browser interaction.

## Where It Was Discovered

**Wiki Agent migration (2026-04-15).** The old Cowork version of Wiki used Computer Use (Min browser) to scan Claude.ai conversations for new information. Runtime was 15-30 minutes, with frequent failures from browser timeouts, screenshot capture issues, and login state problems.

The Routine version uses Slack and filesystem connectors instead. Runtime dropped to 5-15 minutes with no browser failures. Same information gathered, fundamentally more reliable.

## Evidence

| Metric | Computer Use (Cowork) | Connectors (Routine) |
|--------|----------------------|---------------------|
| Runtime | 15-30 min | 5-15 min |
| Failure rate | Frequent (timeouts, screenshots) | Rare (clean tool calls) |
| Cost | Higher (browser overhead) | Lower (direct API calls) |
| Information quality | Screenshot-dependent | Structured data |

## Where Else It Applies

- **Agent Browser strategy:** Computer Use is the product's core capability, but for internal agent operations (not the product itself), connectors should be preferred. The agent browser should offer Computer Use to users, but TTAI's own agents should minimise their use of it.
- **Fred migration:** Fred currently uses Computer Use for Betfair odds. If a Betfair API integration is possible, it would eliminate the most fragile part of Fred's daily loop.
- **Mark-Lite migration:** Mark-Lite uses Desktop Commander and browser tools. Migration to connectors (Google Sheets API, Gmail MCP) would improve reliability.
- **Any future employee:** Default to connectors. Only reach for Computer Use when no connector exists for the target system.

## Exceptions

- **Betfair Exchange:** No public API easily available to TTAI currently. Computer Use may remain necessary for odds fetching until API access is secured.
- **One-off research tasks:** Browsing unfamiliar websites, checking visual layouts, verifying UI state -- Computer Use is the right tool when the task is genuinely visual.

## Links

- [[wiki-agent-SKILL]] -- Where this principle was proven
- [[claude-code-routines]] -- The connector-based platform
- [[browser-agent-arch]] -- The Computer Use architecture (product, not internal ops)
- [[cowork-pipeline]] -- The predecessor system that relied on Computer Use
- [[known-failure-modes]] -- Documents Computer Use failure patterns

## Sources

- Wiki Agent migration session (2026-04-15)
