# Snooker
> Live with first real-money bets placed. Elo with format scaling, experience regression, and H2H blending.
> Last updated: 2026-04-13

## Model
Elo with format scaling, experience regression, H2H blend, and capped form. 30 experiments. Loss metric: L5=0.4662.

Out-of-sample validation on 2,242 matches: 66.8% accuracy. Holdout-to-OOS gap essentially zero — strong generalization.

**Key methodological note**: Uses accuracy-by-confidence tiers rather than raw edge for odds selection due to odds proxy artefact (see below).

## Status
Live (Tour Championship active; expansion in progress)

## Key Results
- **Tour Championship**: +£3.00 net (first real-money bets placed)
- **Bugs caught**: snookerdb winner-as-player_1 data issue; odds proxy artefact (odds appear predictive of outcome independent of model signal)
- **Model confidence**: Naturally underconfident — no calibration adjustment needed

## Coverage Status
**Current**: Tour Championship only (66.8% accuracy, proven edge)
**In progress**: WC Qualifiers (running now)
**Upcoming**: Main stage April 18-May 4

### Market Structure (Fred Betfair exploration, 2026-04-13)

WC Qualifier liquidity: £385-4,281 per match in-play, with spreads of 8-30%+. Several matches showed zero lay liquidity on one side. **Qualifiers are essentially untradeable for systematic betting.**

Outright winner market: £154,768 total, 115.1% overround. Top players (Zhao, Trump, O'Sullivan) have reasonable depth.

**Recommendation**: Restrict snooker betting to main draw Crucible matches only. Check main draw match liquidity when first round begins (April 18) -- expect £10K-50K pre-match with tighter spreads if the market follows the Tour Championship pattern.

## Active Rules
- None sport-specific at this time

## Decision Log
- 2026-04-13: Betfair exploration confirmed WC qualifier liquidity too thin for systematic betting (£385-4,281, 8-30% spreads). Restrict to main draw only. Check main draw liquidity April 18.
- 2026-04-08: WC Qualifiers now in live evaluation. Main stage begins April 18.
- 2026-03-22: Fixed snookerdb data issue where winner was incorrectly mapped to player_1
- 2026-03-15: Identified odds proxy artefact — odds contain information independent of model signal. Shifted from raw edge to accuracy-by-confidence tier selection.
- 2026-02-28: First real-money bets placed on Tour Championship

## Links
- [[autostrategy]] — Strategy optimization methodology
- [[probability-calibration]] — Calibration methodology (not needed here; naturally underconfident)
- [[compound-evaluation]] — L1-L5 evaluation framework (L5=0.4662)
- [[walk-forward-validation]] — OOS validation method
- [[results-diagnostic]] — Analysis framework
- [[betting-portfolio]] — Portfolio container

## Sources
- raw/autostrategy/autostrategy_STATUS.md
- raw/autostrategy/AutoStrategy_Paper_v6.md
