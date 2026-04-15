# Rule: Away Team Edge Threshold
> NBA only. Away underdogs require 20%+ edge (vs 15%+ for home underdogs).
> Last updated: 2026-04-08

## Principle
Road games carry additional variance due to:
- Travel fatigue
- Hostile crowd environment
- Non-standard court conditions
- Shorter rest windows (especially on back-to-backs)

Away teams must overcome a higher bar to constitute value, because even with a true edge, the additional volatility makes smaller edges unprofitable.

## Rule
| Situation | Minimum Edge | Stake |
|-----------|--------------|-------|
| Home underdog | 15%+ | £10 |
| Home underdog | 10-15% | £5 |
| Away underdog | 20%+ | £10 |
| Away underdog | 15-20% | £5 |
| Away underdog | <15% | Do not bet |

## Rationale
- **Home teams**: Baseline 15% edge threshold captures value after controlling for home-court advantage
- **Away teams**: 20% edge threshold accounts for ~5% additional variance on the road
- Both ensure ROI > bookmaker margin (~3-5%) with adequate buffer for standard error

## Implementation Status
- Active
- Applied in all NBA bets since March 2026

## Decision Log
- 2026-03-15: Formally codified after observing higher volatility in away-team bets
- 2026-03-01: Identified variance differential through walk-forward diagnostics

## Related
- [[nba]]
- [[autostrategy]]

## Sources
- NBA travel/schedule data via ESPN
- Backtest variance analysis: raw/autostrategy/AutoStrategy_Paper_v6.md
