# Darts
> Live model, betting market constraint. 3-dart average dominant signal with Elo fallback.
> Last updated: 2026-04-13

## Model
3-dart average (avg_exp=50) as dominant signal with Elo fallback. 63 experiments. Loss metric: L5=0.6257.

**Overfit yellow flag**: Train accuracy 70.2% vs holdout 64.6%. Gap suggests some overfitting to historical data.

## Status
Live model; betting viability limited by market structure

## Key Results
- **Critical problem**: Floor event Betfair Exchange coverage is near-zero pre-match. Core edge thesis (3-dart average prediction) cannot be tested against live odds.
- **MODUS Super Series liquidity** (Fred Betfair exploration, 2026-04-13): £13-54 matched on most matches with 8-10% spreads. Two anomalous matches at £1.3-2.5K (likely a single trader). Getting £5 matched at the quoted price is uncertain. **The floor-event thesis is practically constrained by market structure, not just by model accuracy.**
- **Premier League (TV) liquidity**: £0-154 pre-match 4 days out (would build closer to event), but TV market identified as too sharp for edge.
- **Viable markets**:
  - Euro Tour
  - Players Championship Finals
  - Less-followed TV events
- **Non-viable markets**:
  - Premier League (sharp market, zero edge identified)
  - MODUS Super Series (insufficient liquidity for systematic betting)
- **Recommendation**: Run fill-rate test (5 x £5 on MODUS matches). If fewer than 3/5 fill at quoted price, park darts permanently. Do not wait for the full 2-week viability assessment -- liquidity data already points toward parking.

## Active Rules
- None at this time (awaiting market viability confirmation)

## Decision Log
- 2026-04-13: Fred Betfair exploration confirmed MODUS floor liquidity at £13-54 with 8-10% spreads. Practically untradeable at £5 stakes. Fill-rate test recommended before parking decision.
- 2026-04-08: Scheduled PC9/10 (April 13-14) as next Exchange coverage test
- 2026-03-18: Identified betting market constraint — Floor events have insufficient pre-match Exchange liquidity
- 2026-03-10: Overfit flag raised (train 70.2% vs holdout 64.6%)

## Links
- [[autostrategy]] — Strategy optimization methodology
- [[compound-evaluation]] — L1-L5 evaluation framework (L5=0.6257)
- [[walk-forward-validation]] — Forward-only validation method
- [[results-diagnostic]] — Analysis framework
- [[betting-portfolio]] — Portfolio container
- [[execution-cost-varies-by-selection]] — Spread data from Betfair exploration

## Sources
- raw/autostrategy/autostrategy_STATUS.md
- raw/autostrategy/AutoStrategy_Paper_v6.md
