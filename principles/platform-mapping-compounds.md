# Platform Mapping Compounds

> Once the platform-mapping methodology is proven on one feature, subsequent features are mechanical — 1–2 hours per feature vs. days for the first.
> Last updated: 2026-04-20

## The Principle

The first feature of a platform is expensive to automate because you are inventing the methodology — figuring out what counts as a "feature", how to map UI interaction points, which gotchas exist (dropdowns fail, Shadow DOM fights, scroll-outside-textarea, etc.), and how to compress that knowledge into prompt fragments an agent can consume.

The second and subsequent features are fundamentally cheaper, because the methodology stops being the unknown. You're running a known playbook against a new target.

**Rule of thumb from Hike audit (17 Apr 2026):**
- Original bottom-up estimate: 24 days to map 20 features.
- Actual mapping via Chrome MCP once Onsite Optimizer had proven the pattern: 1–2 hours for all 20.
- ~100x speedup. Worth checking the maths before quoting platform discovery.

## Where It Was Discovered

[[agent-browser]] — Hike SEO platform audit (April 2026). Onsite Optimizer took days because the methodology was being invented in the process. Applying the same methodology to the remaining 19 features took 1–2 hours total.

## Where Else It Applies

- **Evolution MX (KW Bell, Model A).** The first invoice-OCR-correction workflow will be expensive; the second, third, and fourth (whatever else lives in Evolution MX) will be dramatically cheaper. Factor this into any Evolution MX day-rate quote once the first workflow is proven.
- **Any future vertical platform play.** Agent Browser's commercial pitch can lean on this — you pay full rate for the first workflow, everything after is discounted because the platform knowledge is reused.
- **[[mark]] onboarding** — each new client Mark variant reuses the planning-portal + email-infra methodology from earlier builds. Hawks was expensive; Mercia, JDW, Holmes got progressively cheaper to stand up.
- **Analogue in [[autostrategy]]** — the first AutoStrategy domain (NBA) taught the L1–L5 evaluation pattern; subsequent domains reused the pattern at a fraction of the cost.

## Counterexamples / Boundary Conditions

- **Cross-platform doesn't compound.** Moving from Hike (web app) to Evolution MX (Windows native) resets most of the mapping knowledge — only the high-level methodology transfers, not the specific gotchas.
- **Dynamic UIs can re-inject cost.** Platforms that change their UI unpredictably (shadow DOM additions, A/B UI tests) can claw back the compound gain. See [[trust-the-agent-not-dom]] — visual agents are more resilient to UI churn than scripted DOM selectors, which is partly why the Hike speedup held.
- **The first feature must be done thoroughly.** Cutting corners on the first feature means the methodology itself is undercooked, and the compound gain never lands.

## Commercial Framing

When quoting Model A (see [[agent-browser]]) work:
- Feature 1 = day-rate build
- Features 2+ = meaningfully discounted (or rolled into retainer)

This protects the first-feature margin while giving the client a reason to expand the scope with TTAI rather than shop around.

## Links

- [[agent-browser]] — Where the principle landed (Hike audit, April 2026)
- [[kw-bell]] — Next place to apply it (Evolution MX expansion)
- [[trust-the-agent-not-dom]] — Helps the compound gain stick despite UI churn
- [[position-next-stage-not-bigger-commitment]] — Commercial pairing: quote feature 1, let the discount on feature 2 be the natural pull

## Sources

- 2026-04-17 Hike Agent Browser Proposal chat (Claude.ai, Agent Browser project)
- [[agent-browser]] — Hike proposal section
