# Selectivity is Everything
> Value comes from identifying specific mispriced situations, not being right overall.
> Last updated: 2026-04-08

## The Principle
A model with 60% accuracy on all predictions can have -3.1% ROI. The same model betting only the highest-confidence predictions (15%+ edge) can have +92.5% ROI. The difference is selectivity: betting only when the model is most confident and the odds provide genuine value.

## Where Discovered
[[nba]] — betting all model predictions produced -3.1% paper ROI. Filtering to only predictions with 15%+ model edge (relative to market odds) produced +92.5% ROI. The accuracy was identical; selectivity made the difference.

## Where It Applies
- [[nba]], [[tennis-atp]], [[snooker]], [[darts]] — all value betting (only bet high-edge situations)
- [[mark]] — quality leads over volume (focus on prospects that fit the profile, not all prospects)
- [[consulting]] — right clients over more clients (boutique positioning: cherry-pick high-LTV, low-friction clients)
- Any matching/ranking system — confidence threshold separates winners from losers

## How to Implement
1. Calculate model confidence or edge for each prediction
2. Set a confidence/edge threshold (e.g., 15% for sports betting, 75% fit-score for leads)
3. Only act on predictions above the threshold
4. Track ROI separately for different confidence bands

## Exceptions
- Low-volume domains: if selectivity reduces volume too much, you may not have enough data to generate sustainable returns
- Relationship-dependent contexts: in [[consulting]] and [[mark]], turning away prospects harms long-term reputation and referral pipeline
- Regulatory constraints: some systems (e.g., credit lending) cannot be selective based on certain features

## Links
- [[nba]]
- [[tennis-atp]]
- [[snooker]]
- [[darts]]
- [[mark]]
- [[consulting]]

## Sources
- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/daily-skill-lessons-learned.md
