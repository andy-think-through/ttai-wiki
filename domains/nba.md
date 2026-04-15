# NBA
> Live daily betting with Elo-based margin-of-victory model and injury-aware veto rules.
> Last updated: 2026-04-14

## Model
Elo-based with margin-of-victory multiplier and team-specific home court advantage. Streak dampening has been REMOVED after walk-forward diagnostic confirmed double-counting of recent form in player movement data.

Backtest accuracy: 64.7%

## Status
Live

## Key Results
- **Actual P&L**: +£28.90 (regular season closed 2026-04-13 after CHI @ DAL loss of -£10)
- **Paper P&L**: +£79.40 (through April 13)
- **Strategy**: Back underdogs with 15%+ edge (£10 stake) or 10-15% edge (£5 stake). Away underdogs require 20%+ edge minimum. Execute via Betfair Exchange.
- **Predicted-loser experiment**: 8/8 paper bets lost in NBA. Combined with tennis: 18/18 paper bets lost. [[never-back-predicted-loser]] now at or past the 20-bet formalisation threshold — recommend formalising as active rule.
- **Regular season: complete.** Play-in starts 2026-04-14. Postseason strategy decision pending.
- **Key edge**: Market overreacts to star player injuries on deep teams. Players on deep rosters (bench strength mitigates absence) see excessive line movement; players on thin rosters see insufficient movement.

## Active Rules
- [[injury-veto-80pct]] — Skip bet only if star player has played 80%+ of season and newly ruled out
- [[away-team-threshold]] — Away underdogs must show 20%+ edge (vs 15% for home underdogs)
- [[never-back-predicted-loser]] — Do not back model's predicted loser, even with edge

## Market Structure (Betfair Exchange)

Fred's Betfair exploration (2026-04-13) revealed significant spread asymmetry:

| Selection Type | Pre-Match Spread | In-Play Spread | Notes |
|---|---|---|---|
| Favourites | 0.8-1.8% | 3.3% | Tight; efficient execution |
| Underdogs | 2-8% | 10-12% | Wide; hidden execution cost |
| Extreme dogs (30+) | 60%+ | N/A | Untradeable |

**Implication:** Paper P&L on underdogs overstates real performance by the spread amount (typically 3-5%). The 20% away-underdog threshold is justified not only by calibration but by execution cost. In-play betting on underdogs is structurally uneconomic.

Typical match liquidity: £15K-52K pre-match (regular season), up to £190K for marquee matchups. End-of-season tanking-scenario matches (e.g., Nets/Raptors) show extreme favourite pricing (1.02/34) with essentially zero underdog tradability.

See [[execution-cost-varies-by-selection]] for the full cross-sport analysis.

## Decision Log
- 2026-04-14: Regular season ended. Final actual P&L +£28.90 (-£10 on final CHI @ DAL bet 2026-04-12). Predicted-loser experiment hit 8/8 NBA, 18/18 combined with tennis — formalisation threshold crossed. Postseason/play-in strategy decision required.
- 2026-04-13: Betfair spread analysis added. Underdog execution cost is 2-8% pre-match, reinforcing 20% away threshold. Paper ROI likely overstates real performance. In-play betting ruled out.
- 2026-04-08: Removed streak dampening after diagnostic showed double-counting with player movement
- 2026-03-15: Formalised injury-veto rule to distinguish genuine new information from Elo-embedded absence

## Links
- [[autostrategy]] — Strategy optimization methodology
- [[results-diagnostic]] — Post-hoc diagnostic framework
- [[compound-evaluation]] — Multi-level evaluation (L1-L5)
- [[walk-forward-validation]] — Rolling-fold testing where discovered
- [[betting-portfolio]] — Portfolio container
- [[probability-calibration]] — Calibration methodology
- [[active-rules]] — Core rules used in this domain
- [[injury-veto-80pct]] — Domain-specific rule
- [[away-team-threshold]] — Domain-specific rule
- [[never-back-predicted-loser]] — Domain-specific rule
- [[execution-cost-varies-by-selection]] — Spread asymmetry discovered via Betfair exploration

## Sources
- raw/autostrategy/autostrategy_STATUS.md
- raw/autostrategy/AutoStrategy_Paper_v6.md
