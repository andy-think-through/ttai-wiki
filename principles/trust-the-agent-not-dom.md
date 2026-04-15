# Trust the Agent, Not the DOM

> When a scripted approach fights the DOM (Shadow DOM, React state, cross-origin iframes), let the visual browser agent handle it instead. Pixel-based agents bypass structural complexity that programmatic approaches get stuck on.
> Last updated: 2026-04-12

## The Principle

If you're spending significant time building a standalone Playwright/Puppeteer script to navigate complex web UI — and the DOM is fighting you (Shadow DOM encapsulation, React state management, cross-origin iframes, dynamic element IDs) — stop. The visual browser agent will likely handle the same task faster and cheaper by working at the pixel level, where none of that structural complexity exists.

## Where It Was Discovered

Agent Browser schema workflow (Onsite Optimizer Phase 3), April 2026. First attempt: a standalone Playwright script with Shadow DOM traversal to inject JSON-LD schema via Shopify's SEO settings modal. Failed after 2 hours of debugging — the modal's internal structure was encapsulated behind Shadow DOM boundaries and React state that Playwright couldn't reliably traverse.

Second attempt: the visual browser agent. Handled the same task in 14 iterations for $0.34. The agent simply saw the modal on screen, clicked the right fields, typed the content, and saved. Shadow DOM, React state, and iframe boundaries were invisible at the screenshot level.

## Where Else It Applies

- **[[agent-browser]]** — Core architectural decision. When scoping new workflows, default to the visual agent unless the task is simple enough for direct Playwright scripting (no complex UI, stable selectors, no dynamic content).
- **[[kw-bell]]** — Invoice OCR correction in Evolution MX. Evolution MX likely has complex UI patterns. Start with the visual agent rather than trying to script DOM interactions.
- **Any SaaS automation** — Modern SaaS apps increasingly use Shadow DOM, Web Components, and framework-specific state management. Visual agents sidestep all of this.
- **Deterministic routing hybrid** — The optimal pattern may be: use scripted Playwright for navigation and simple actions (where the DOM is predictable), then hand off to the visual agent for complex UI interactions (where the DOM fights back).

## Boundary Conditions

- **Cost:** The visual agent uses screenshots (tokens), so it's more expensive per-action than a scripted approach. For high-volume, highly repetitive tasks, investing in DOM scripting (or action caching) may be worthwhile once the pattern is proven.
- **Speed:** Scripted Playwright runs faster than the agent loop (no screenshot capture, no LLM round-trip). For latency-sensitive workflows, scripting wins if the DOM cooperates.
- **Stability:** DOM selectors break when apps update. Visual agents are more resilient to UI changes (buttons move but still look like buttons). This favours the agent for workflows that need to survive app updates.

## Related Principles

- [[removal-as-valuable-as-addition]] — Removing the scripted approach and trusting the agent saved 2 hours of debugging
- [[scheduled-tasks-need-zero-intervention]] — Visual agents are more likely to complete complex tasks without intervention than brittle DOM scripts

## Links

- [[agent-browser]] — Product this principle governs
- [[browser-agent-arch]] — Architecture context
- [[kw-bell]] — First external client where this will apply

## Sources

- 2026-04-12-agent-browser-prompt-caching-and-optimisation-research.md (wiki inbox)
