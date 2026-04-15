# Majority-Class Trap
> Imbalanced domains produce majority-class predictors unless evaluation penalizes this.
> Last updated: 2026-04-08

## The Principle
In domains where one outcome dominates (e.g., 95% matches have no upset), a model trained with standard loss functions will learn to predict the majority class and achieve high accuracy while completely failing on the minority. A model claiming 54.5% accuracy but 0/6 upset predictions is a majority-class coaster.

## Where Discovered
[[tennis-atp]] — model achieved 54.5% accuracy overall but predicted 0 upsets out of 6 actual upset opportunities in the test set. The model was learning to predict the favorite 95% of the time and never risking an upset prediction.

## The Fix
- Use [[results-diagnostic]] to decompose performance by outcome class
- Enforce minority-class metrics in level-3 evaluation (recall, precision, F1 on minority class)
- Penalize base-rate coasting in level-5 evaluation (e.g., require minimum upset prediction rate that scales with true upset frequency)
- Use weighted loss functions that penalize minority-class misses more heavily

## Where It Applies
Any classification domain with imbalanced outcomes:
- [[tennis-atp]] — upset detection (majority: favorite wins)
- [[nba]] — come-from-behind prediction (majority: leader holds)
- [[snooker]] — frame recovery (majority: leader holds)
- [[horse-racing]] — long-shot detection (majority: favorites win)
- [[consulting]] — churn prediction (majority: client stays)

## Exceptions
- Some imbalance is acceptable if you're explicitly using the model for high-specificity predictions (e.g., only predicting upsets with very high confidence)
- In cost-asymmetric domains, ignoring the minority class can be optimal (e.g., if false positives are very expensive)

## Links
- [[tennis-atp]]
- [[nba]]
- [[snooker]]
- [[horse-racing]]
- [[consulting]]
- [[results-diagnostic]]

## Sources
- raw/autostrategy/daily-skill-lessons-learned.md
- raw/autostrategy/autostrategy_STATUS.md
