# Tennis ATP
> Live daily betting with clay swing active. Elo with surface-specific ratings and isotonic regression calibration.
> Last updated: 2026-04-10

## Model
Elo with surface-specific ratings. Adaptive rank/Elo blending and H2H correction (exp6c). Isotonic regression calibration integrated to prevent miscalibration across confidence tiers.

## Status
Live (clay swing active through April)

## Key Results
- **Actual P&L**: +£7.96 (through April 10). Previously +£5.53 as of April 8.
- **Monte Carlo Masters**: Active — clay swing in progress. Apr 6-7 results: Vacherot won (+£1.63), Cobolli won (+£3.15), Bublik won (+£2.65), Muller lost (-£5.00). Net +£2.43 from 4 bets (3W/1L). Cilic value bet recommended Apr 8 (Monte Carlo R32). QF stage reached — 0 value bets found Apr 10 (market priced efficiently).
- **Surface performance**:
  - Clay: 55.3% win rate (best surface)
  - Hard: Solid performance
  - Grass: -20% ROI on 86 bets despite high apparent edge signals (phantom value — see grass-veto below)
- **Strategy**: Back value picks where calibrated probability > market implied probability. £5 flat staking.

## Status
Live (grass veto pending)

## Active Rules
- [[never-back-predicted-loser]] — Do not back model's predicted loser, even with edge
- [[grass-veto]] (pending implementation) — MUST be implemented before grass season mid-June

## Decision Log
- 2026-04-10: Monte Carlo QF — 0 value bets found (market efficient at late tournament stage). 2 bets from Apr 1 still "Pending" settlement.
- 2026-04-08: Grass veto pending formal implementation. Current state: grass bets logged but still placed. Deadline: before mid-June grass season.
- 2026-03-20: Discovered majority-class trap where upsets (0/6) on paper experiment revealed need for L3 minority-class checks
- 2026-03-10: Integrated isotonic regression calibration after observing miscalibration across confidence tiers

## Links
- [[autostrategy]] — Strategy optimization methodology
- [[probability-calibration]] — Calibration methodology applied
- [[compound-evaluation]] — L1-L5 evaluation framework
- [[walk-forward-validation]] — Regime robustness testing
- [[phantom-value]] — Grass court discovery (high-randomness domain)
- [[majority-class-trap]] — Minority-class checks (upsets)
- [[betting-portfolio]] — Portfolio container
- [[grass-veto]] — Domain-specific rule
- [[never-back-predicted-loser]] — Domain-specific rule
- [[results-diagnostic]] — Analysis framework

## Sources
- raw/autostrategy/autostrategy_STATUS.md
- raw/autostrategy/AutoStrategy_Paper_v6.md
