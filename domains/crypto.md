# Crypto
> Paper trading since March 27. Donchian Channel Breakout with EMA trend filter on 4-hour candles.
> Last updated: 2026-04-08

## Model
Branch_4 Donchian Channel Breakout with EMA(30) trend filter, volume surge requirement, and ATR expansion trigger. 4-hour candles.

Developed via walk-forward validation (1min → overfitted, 5min → no edge, 4hr → genuine edge).

VPS: 159.65.18.20

## Status
Paper trading (since March 27, 2026)

## Key Results
- **BTC**: +0.25% (2 trades)
- **Multi-pair portfolio**: -2.36% (16 trades, 25% win rate)
- **Combined**: -1.06%
- **Concern**: Multi-pair scanner shows consistent stop-loss exits below backtest expectations

## Review Schedule
- 4-week review due ~April 24

## Active Rules
- None at this time

## Decision Log
- 2026-04-08: Multi-pair underperformance flagged. Stop-loss exits consistent but tighter than backtest.
- 2026-03-27: Paper trading started
- 2026-03-15: Walk-forward validation completed (1min overfitting → 5min no edge → 4hr genuine edge)

## Links
- [[autostrategy]] — Strategy optimization methodology
- [[walk-forward-validation]] — Regime robustness testing (discovered 4hr timeframe)
- [[compound-evaluation]] — L1-L5 evaluation framework
- [[results-diagnostic]] — Analysis framework
- [[data-leakage-silent-killer]] — Principle relevant to FX/crypto time-series data
- [[betting-portfolio]] — Portfolio container

## Sources
- raw/autostrategy/autostrategy_STATUS.md
- raw/autostrategy/AutoStrategy_Paper_v6.md
