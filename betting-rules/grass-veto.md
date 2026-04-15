# Rule: Grass Court Veto (Tennis)
> Tennis only. No bets on grass matches. Pending implementation before mid-June.
> Last updated: 2026-04-08

## Principle
Grass courts introduce structural randomness that eliminates model edge despite high apparent signals. This is the same pattern observed in EFL League One/Two vs Championship: same market structure, different underlying randomness.

- **Grass court characteristics**: Fast court speed, low bounce, highly variable conditions (moisture, wear patterns)
- **Model signals on grass**: Appear strong but are **phantom value** — overfitting to weak patterns
- **ROI reality**: -20% on 86 bets despite superficially high edge signals

## Evidence
| Surface | Bets | ROI | Notes |
|---------|------|-----|-------|
| Clay | 67 | +8.3% | Strong edge, consistent |
| Hard | 72 | +3.1% | Solid |
| Grass | 86 | -20% | Phantom value despite strong signals |

**Interpretation**: Grass matches have ~3x higher randomness (σ) than other surfaces. Apparent edge signals are fitting to noise rather than genuine predictive patterns.

## Comparison: EFL Market Efficiency
This mirrors the Championship/League One discovery:
- **EFL Championship**: +2.2% ROI (same model, genuine edge exists)
- **EFL League One/Two**: -5% ROI (same model, no edge — higher randomness)
- **Reason**: Randomness in League One/Two outcomes overwhelms model signal

## Rule
**Current state** (until implementation):
- Log grass predictions
- Place bets normally
- Track performance separately

**Target state** (on or before mid-June):
- Do not place bets on grass matches
- Log predictions for diagnostic purposes only
- Formal implementation mandatory before Wimbledon fortnight

## Implementation Deadline
- **Grass season**: Late June onwards (primarily Wimbledon, some warm-up events in June)
- **Mandatory implementation**: Before June 15, 2026
- **Current status**: Pending (active logging, still betting)

## Active Rules
- None applied yet (pending implementation)

## Decision Log
- 2026-04-08: Added to [[active-rules]] as "Pending". Implementation deadline: mid-June.
- 2026-03-22: Grass phantom value confirmed. -20% ROI pattern locked in.
- 2026-02-28: Recognised grass surface issue during clay swing analysis

## Related
- [[tennis-atp]]
- [[efl-championship]] (analogous market-efficiency finding)
- [[autostrategy]]

## Sources
- Tennis match data and odds: raw/autostrategy/AutoStrategy_Paper_v6.md
- Surface analysis: raw/autostrategy/AutoStrategy_Paper_v6.md (March 2026 updates)
