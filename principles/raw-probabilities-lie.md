# Raw Probabilities Lie
> Raw model probabilities systematically overstate value-bet edge.
> Last updated: 2026-04-08

## The Principle
LLM-generated and statistical model predictions output probabilities that look calibrated but systematically misalign with empirical frequencies. A model saying 67% happens only 45% of the time in reality. This gap inflates perceived edge in betting and can cause systematic overconfidence.

## Where Discovered
[[efl-championship]] value-betting experiment—model predicted 67% probability on a candidate set. When backtested, the actual conversion rate was 45%. This phantom 22-point edge translated to 345 "bets" at model confidence, but only ~102 were genuinely profitable on real odds.

## The Fix
Apply [[probability-calibration]] via isotonic regression or Platt scaling. Calibrate model outputs against holdout validation data before using them for value calculations.

## Where It Applies
Every value-betting domain where raw model scores are compared to market odds:
- [[nba]] — full season and live markets
- [[tennis-atp]] — match and point-level predictions
- [[snooker]] — match and frame predictions
- Future domains — any new sport or asset class

This is particularly acute in low-volume domains where sample sizes are small and chance variation can masquerade as calibration error.

## Exceptions
- When explicitly using a calibrated probability model (post-isotonic regression), the gap is reduced but not eliminated
- Ensemble methods that average multiple models can reduce the individual model bias
- Market-derived implied probabilities are already calibrated (that's the market's job), so comparing raw model probs to market-implied probs will always show a gap

## Links
- [[probability-calibration]]
- [[efl-championship]]
- [[nba]]
- [[tennis-atp]]
- [[snooker]]
- [[phantom-value]]

## Sources
- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/autostrategy_STATUS.md
