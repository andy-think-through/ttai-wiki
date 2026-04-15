# Data Leakage: Silent Killer
> Forward-looking data in backtests inflates results beyond recognition.
> Last updated: 2026-04-08

## The Principle
Data leakage—using information from the future to predict the past—is the most insidious form of backtest inflation. A model claiming +72% ROI can collapse to -6.5% once leakage is removed. The most common source: aggregate statistics (win rates, averages, strike rates) calculated from the full dataset, including future data.

## Where Discovered
[[horse-racing]] — initial backtests showed +72% ROI. As leakage was systematically removed (forward-only evaluation of aggregate stats, proper train/test splits), ROI collapsed to -6.5%. The entire edge was phantom.

## The Fix
- Calculate all aggregate statistics in a forward-only manner (only using historical data available at prediction time)
- Use paper-trading audits to validate backtests
- Separate train/validation/holdout sets and never use holdout data to calculate features
- Audit the feature pipeline for any datetime-dependent calculations

## Where It Applies
Any predictive system with time-series data:
- [[nba]], [[tennis-atp]], [[snooker]], [[darts]] — all sports betting
- [[horse-racing]] — particularly vulnerable because aggregate stats are common
- [[mark]] — lead scoring that uses historical conversion rates
- [[consulting]] — engagement prediction that uses historical project outcomes

Leakage is hardest to spot in systems with many features or manual feature engineering.

## Exceptions
- Some leakage is acceptable if it's transparent and consistent (e.g., using season-to-date stats in mid-season betting, as long as you know you're using that information)
- Cross-validation that properly respects time ordering can mitigate but not eliminate leakage risk

## Links
- [[horse-racing]]
- [[nba]]
- [[tennis-atp]]
- [[snooker]]
- [[darts]]
- [[mark]]

## Sources
- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/daily-skill-lessons-learned.md
