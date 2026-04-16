# Connectors Beat Computer Use

> Default to structured connectors (APIs, MCP servers) over visual browser automation. Computer Use is a fallback, not the primary path.
> Last updated: 2026-04-16

## The Principle

When building agents that need to access external systems, default to structured connectors (APIs, MCP servers, direct integrations) rather than visual browser automation (Computer Use). Computer Use should be a fallback for situations where no connector exists, not the default approach.

## Where It Was Discovered

**Wiki Agent migration (2026-04-15):** The old Cowork-based Wiki Agent used Computer Use (Min browser) to scan Claude.ai conversations for new information. Runtime was 15-30 minutes with frequent failures (timeouts, UI changes, sandbox restrictions). The Routines-based replacement uses MCP connectors for Slack, Google Drive, and GitHub. Runtime dropped to 5-15 minutes with no browser failures.

## Evidence

| Metric | Computer Use (Cowork) | Connectors (Routines) |
|--------|----------------------|----------------------|
| Runtime | 15-30 min | 5-15 min |
| Failure rate | Frequent (CU timeouts, UI changes) | Rare (clean tool calls) |
| Cost | High (vision tokens) | Lower (no vision overhead) |
| Reliability | Fragile (depends on UI state) | Robust (structured responses) |
| Interaction | One-way (email) | Two-way (Slack + API) |

## Where Else It Applies

- **Agent Browser optimisation roadmap:** The three-layer cost reduction plan (prompt caching -> deterministic routing -> action caching) follows the same principle. Layer 2 (deterministic routing) is the product equivalent -- replace expensive visual interactions with cheaper structured ones where possible.
- **Fred migration:** Fred currently uses Computer Use for Betfair odds fetching. If a Betfair API connector became available, it would be faster and more reliable.
- **Mark-Lite migration:** Mark-Lite uses Desktop Commander for local file access. Migrating to Google Sheets MCP connector would remove the local machine dependency.
- **Any new employee:** Start with connectors. Only add Computer Use for tasks where no structured alternative exists.

## Exceptions

- **No API available:** Some platforms (Betfair UI, certain legacy systems) genuinely require visual interaction.
- **Exploration/discovery:** When investigating a new system or process, Computer Use can be faster for initial reconnaissance before building structured integrations.
- **One-off tasks:** If a task is truly one-time, building a connector isn't worth the effort.

## Relationship to Other Principles

- Extends [[scheduled-tasks-need-zero-intervention]] -- connectors are more reliable unattended
- Supports [[trust-the-agent-not-dom]] -- but at the infrastructure level (don't build around UI when API exists)
- Cross-validates the [[agent-browser]] optimisation roadmap

## Links

- [[claude-code-routines]] -- Platform where this principle was proven
- [[wiki-agent-SKILL]] -- First employee to benefit from migration
- [[agent-browser]] -- Product where the same principle applies to cost reduction
- [[cowork-pipeline]] -- Predecessor system that relied on Computer Use

## Sources

- Wiki Agent migration session (2026-04-15)
