# Crypto

> Paper trading concluded. Parked indefinitely after -16.8% multi-pair result. VPS deleted 29 Apr.
> Last updated: 2026-04-29

## Model
Branch_4 Donchian Channel Breakout with EMA(30) trend filter, volume surge requirement, and ATR expansion trigger. 4-hour candles.

Developed via walk-forward validation (1min -> overfitted, 5min -> no edge, 4hr -> genuine edge).

## Status
**Parked indefinitely** (decision 2026-04-29).

Multi-pair portfolio returned -16.8% with consistent stop-loss exits below backtest expectations. DigitalOcean droplet (159.65.18.20) deleted 29 Apr ~10:55 BST. Paper trading logs saved before deletion.

Cord recommended park (-16.8%). Andy confirmed and actioned.

## Key Results
- **BTC**: +0.25% (2 trades)
- **Multi-pair portfolio**: -16.8% (consistent stop-loss exits)
- **Combined**: negative
- **Root cause**: Stop-loss exits systematically tighter in live paper trading than backtest indicated. Multi-pair scanner did not reproduce backtest edge.

## Active Rules
- None (parked)

## Decision Log
- 2026-04-29: **PARKED INDEFINITELY.** -16.8% multi-pair. Andy deleted VPS. Logs saved. Cord routed rewrite to Wiki.
- 2026-04-08: Multi-pair underperformance flagged. Stop-loss exits consistent but tighter than backtest.
- 2026-03-27: Paper trading started
- 2026-03-15: Walk-forward validation completed (1min overfitting -> 5min no edge -> 4hr genuine edge)

## Links
- [[autostrategy]] -- Strategy optimization methodology
- [[walk-forward-validation]] -- Regime robustness testing (discovered 4hr timeframe)
- [[compound-evaluation]] -- L1-L5 evaluation framework
- [[results-diagnostic]] -- Analysis framework
- [[data-leakage-silent-killer]] -- Principle relevant to FX/crypto time-series data
- [[betting-portfolio]] -- Portfolio container
- [[phantom-value]] -- Apparent edge was structural illusion

## Sources
- raw/autostrategy/autostrategy_STATUS.md
- raw/autostrategy/AutoStrategy_Paper_v6.md
- Cord Channel session 2026-04-29 (droplet deletion confirmation)
