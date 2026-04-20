# Principles Index
> All principles with origin and applicability.
> Last updated: 2026-04-20

## Consulting & Sales Principles (Phase 1)

| Principle | Origin | Applies To |
|-----------|--------|------------|
| [[dont-reveal-methodology-before-paid]] | TTAI consulting | All prospect-facing comms |
| [[position-next-stage-not-bigger-commitment]] | TTAI consulting | All sales conversations |
| [[let-clients-surface-pain-points]] | TTAI consulting, KW Bell, MJM | All discovery/audit work |
| [[email-quality-over-volume]] | TTAI email drafting | All email outreach |

## Betting & Predictive Model Principles (Phase 2)

| Principle | Origin | Applies To |
|-----------|--------|------------|
| [[raw-probabilities-lie]] | AutoStrategy EFL | All value betting, all sports |
| [[removal-as-valuable-as-addition]] | AutoStrategy NBA | Feature engineering, template/proposal simplification |
| [[trust-the-model-over-punditry]] | AutoStrategy NBA live | All betting, consulting (vs gut feel) |
| [[phantom-value]] | AutoStrategy Tennis, EFL | High-randomness sub-domains (grass, lower tiers) |
| [[data-leakage-silent-killer]] | AutoStrategy Horse Racing | Any predictive system with time-series data |
| [[selectivity-is-everything]] | AutoStrategy NBA | All value betting, lead qualification, client selection |
| [[majority-class-trap]] | AutoStrategy Tennis | Imbalanced classification domains |
| [[market-efficiency-varies-within-domain]] | AutoStrategy EFL | All domains with tiers or sub-strata |
| [[scheduled-tasks-need-zero-intervention]] | AutoStrategy daily ops | All scheduled Cowork skills, automation |
| [[strict-trade-matching]] | Mark-Lite outreach | Lead qualification, sales matching |
| [[derivative-markets-harder-than-primary]] | AutoStrategy Football Corners | Props/secondary market betting |
| [[execution-cost-varies-by-selection]] | Fred Betfair exploration (2026-04-13) | All value betting (underdogs cost more to execute), lead qualification analogy |

## Mark-Lite Campaign Principles (April 2026)

| Principle | Origin | Applies To |
|-----------|--------|------------|
| [[planning-data-serves-site-trades]] | Mark-Lite campaign analysis (L3 compound eval) | Mark, Mark-Lite, Construction Intelligence opportunity, planning portal monitoring |

## Agent Browser Principles (April 2026)

| Principle | Origin | Applies To |
|-----------|--------|------------|
| [[trust-the-agent-not-dom]] | Agent Browser schema workflow | Any decision about building custom scripts vs using the visual agent |
| [[platform-mapping-compounds]] | Hike platform audit 2026-04-17 | Any platform discovery work (Evolution MX, future Model A clients, [[mark]] variants) |

## Infrastructure & Operations Principles (April 2026)

| Principle | Origin | Applies To |
|-----------|--------|------------|
| [[connectors-beat-computer-use]] | Wiki Agent migration to Routines (2026-04-15) | Any agent design: default to APIs/connectors, not browser automation |
| [[repos-are-employee-memory]] | Wiki Agent branch proliferation incident (2026-04-16) | All employees on ephemeral infrastructure: commit state early and often |

## Cross-Principle Links

### By Domain
- **AutoStrategy (Betting):** [[raw-probabilities-lie]] → [[removal-as-valuable-as-addition]] → [[trust-the-model-over-punditry]] → [[phantom-value]] → [[data-leakage-silent-killer]] → [[selectivity-is-everything]] → [[majority-class-trap]] → [[market-efficiency-varies-within-domain]] → [[derivative-markets-harder-than-primary]] → [[execution-cost-varies-by-selection]]
- **TTAI Sales/Consulting:** [[dont-reveal-methodology-before-paid]] + [[position-next-stage-not-bigger-commitment]] + [[let-clients-surface-pain-points]] + [[email-quality-over-volume]]
- **Mark (Lead Qualification):** [[strict-trade-matching]] + [[selectivity-is-everything]] + [[trust-the-model-over-punditry]] + [[planning-data-serves-site-trades]]
- **Agent Browser:** [[trust-the-agent-not-dom]] + [[platform-mapping-compounds]]
- **Automation/Operations:** [[scheduled-tasks-need-zero-intervention]] + [[connectors-beat-computer-use]] + [[repos-are-employee-memory]]
- **Value Betting (Sports):** [[raw-probabilities-lie]] + [[probability-calibration]] + [[trust-the-model-over-punditry]] + [[selectivity-is-everything]]

### By Theme
- **Avoid overconfidence:** [[raw-probabilities-lie]] + [[phantom-value]] + [[trust-the-model-over-punditry]]
- **Subtraction beats addition:** [[removal-as-valuable-as-addition]] + [[selectivity-is-everything]]
- **Data quality:** [[data-leakage-silent-killer]] + [[majority-class-trap]]
- **Stratification matters:** [[market-efficiency-varies-within-domain]] + [[phantom-value]] + [[planning-data-serves-site-trades]]
- **Trust the system:** [[trust-the-model-over-punditry]] + [[trust-the-agent-not-dom]]

## Sources
- **Consulting:** raw/ttai/claude.md, raw/ttai/TTAI_Project_Instructions.md
- **Betting:** raw/autostrategy/AutoStrategy_Paper_v6.md, raw/autostrategy/daily-skill-lessons-learned.md, raw/autostrategy/autostrategy_STATUS.md
- **Operations:** raw/autostrategy/daily-skill-lessons-learned.md
- **Outreach:** raw/mark/outreach-lessons.md
- **Campaign Analysis:** Mark-Lite Campaign Analysis April 2026 (tracker data, compound eval L1–L3)
- **Agent Browser:** 2026-04-12-agent-browser-prompt-caching-and-optimisation-research.md
