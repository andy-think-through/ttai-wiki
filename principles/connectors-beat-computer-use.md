# Connectors Beat Computer Use

> Default to structured connector/API access over visual browser automation. Computer Use is a fallback, not the primary path.
> Last updated: 2026-04-16

## The Principle

When building AI agents, prefer MCP connectors and APIs for data access over Computer Use (visual browser automation). Computer Use is slower, more expensive, more fragile, and harder to debug. Connectors provide structured, predictable data at a fraction of the cost.

## Where It Was Discovered

Wiki Agent migration (2026-04-15). The old Cowork-based Wiki used Computer Use (Min browser) to scan Claude.ai conversations -- 15-30 min runtime, frequent failures. The Routines version uses Slack + Google Drive + GitHub connectors -- 5-15 min, no failures, clean tool calls.

## Where It Applies

- **All TTAI employees:** Default to connectors for Slack, Google Drive, Gmail, GitHub. Only use Computer Use for tasks with no connector path.
- **Agent Browser product:** The three-layer cost optimisation roadmap (prompt caching -> deterministic routing -> action caching) is essentially this same principle applied at product level. Layer 2 (deterministic routing) replaces expensive visual interactions with cheaper structured ones.
- **Consulting advice:** Any client building agents should hear this. APIs first, browser automation as fallback.

## Exceptions

- Tasks where no API/connector exists (e.g., scraping websites without APIs)
- Exploration tasks where visual verification is needed
- Complex UI interactions that resist structured automation (but see [[trust-the-agent-not-dom]])

## Evidence

| Metric | Computer Use (Cowork) | Connectors (Routines) |
|--------|----------------------|----------------------|
| Runtime | 15-30 min | 5-15 min |
| Failure rate | Frequent (timeouts, UI changes) | Rare |
| Cost | Higher (screenshot tokens) | Lower (text-only) |
| Debuggability | Low (visual, non-deterministic) | High (structured tool calls) |

## Links

- [[wiki-agent-SKILL]] -- First employee to demonstrate this principle
- [[claude-code-routines]] -- Platform that enables connector-first access
- [[trust-the-agent-not-dom]] -- Related agent architecture principle
- [[agent-browser]] -- Product where this principle shapes the optimisation roadmap

## Sources

- Wiki Agent migration session (2026-04-15)
