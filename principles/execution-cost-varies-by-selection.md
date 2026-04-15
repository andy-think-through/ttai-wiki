# Execution Cost Varies By Selection Type

> Paper trading assumes you get matched at the mid-price. Real markets charge a spread that varies dramatically by selection type.
> Last updated: 2026-04-13

## The Principle

The cost of executing a bet is not fixed. Favourites have tight spreads (0.8-1.8% on NBA); underdogs have wide spreads (2-8% pre-match, 10-12% in-play). This spread cost eats directly into the model's estimated edge and is not captured in paper trading or backtesting.

A 15% model edge on a 4.6 underdog becomes ~11% after a 4.3% spread. A 15% edge on a 1.3 favourite loses only ~1% to spread.

## Where Discovered

Fred's first Betfair exploration (2026-04-13). Systematic scan of NBA, tennis, snooker, darts, and cricket markets revealed consistent pattern: underdog spreads are 2-8x wider than favourite spreads across all sports.

## Data

| Sport | Favourite Spread | Underdog Spread | Ratio |
|---|---|---|---|
| NBA pre-match | 0.8-1.8% | 2-8% | 2-5x |
| NBA in-play | 3.3% | 10-12% | 3-4x |
| Tennis ATP 500 | 0.7-3.1% | 2.7-12.5% | 2-4x |
| IPL Cricket | 0.5% | 0.9% | 1.8x |
| Snooker WC Quals | 8-30%+ | 8-30%+ | ~1x (both wide) |
| Darts MODUS | 8-10% | 8-10% | ~1x (both wide) |

## Where Else It Applies

- **All value-betting domains:** Any domain where Fred backs underdogs needs to account for spread cost in the edge calculation
- **Mark-Lite / consulting:** Analogous to "the cost of selling to hard-to-reach prospects is higher than selling to easy ones" -- not all leads are equal, even if the theoretical margin is the same
- **AutoStrategy methodology:** Paper ROI should include estimated spread cost as a deduction before comparing to live ROI

## Counterexamples / Boundary Conditions

- IPL cricket has remarkably tight spreads on both sides (0.5% / 0.9%) -- high liquidity markets with balanced action compress spreads
- Extreme mismatches (Nets/Raptors at 34/1.02) have enormous underdog spreads (62%) that make them completely untradeable regardless of model edge
- Spread is a snapshot -- it varies by time-to-event, day of week, and market attention

## Implications for Fred

1. **NBA away-underdog 20% threshold has additional justification** beyond calibration -- it also needs to cover 4-8% execution cost
2. **Consider adjusting edge thresholds** to be spread-aware: effective edge = model edge minus estimated spread cost
3. **Paper P&L overstates real performance** on underdogs by the spread amount. Historical paper ROI of +92.5% would compress in practice.

## Links

- [[away-team-threshold]] -- Existing rule that this principle reinforces
- [[selectivity-is-everything]] -- Another reason to be selective about which underdogs to back
- [[nba]] -- Primary domain where this was measured
- [[betting-portfolio]] -- Portfolio-level implication

## Sources

- Fred Betfair exploration report (2026-04-13)
