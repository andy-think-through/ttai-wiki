# Rule: Predicted Loser (Formalised)
> Never back the model's predicted loser. Formalised 2026-04-16 at 0/18 by Andy's decision.
> Last updated: 2026-04-16

## Status
**Formalised** -- active rule across all sports. Combined record 0/18 across NBA and Tennis. Formalised by Andy on 2026-04-16 on Fred's recommendation, 2 bets short of the original 20-bet threshold. At 18/18 with 0% wins, the statistical evidence was conclusive regardless of threshold.

## Experiment Design
### Hypothesis
Backing the model's predicted loser should generate value if market misprices the losing side. However, the model's confidence is asymmetrically distributed, making this a structural trap.

### Method
Track every bet where:
- Model predicts A will beat B (e.g., A > 60% probability)
- Odds suggest value betting on B (predicted loser)
- Place the bet and log outcome

### Results
| Domain | Bets | Wins | Win Rate |
|--------|------|------|----------|
| NBA | 8 | 0 | 0% |
| Tennis | 10 | 0 | 0% |
| **Total** | **18** | **0** | **0%** |

**Confidence**: Conclusive. NBA 8/8, Tennis 10/10, combined 18/18 as of 2026-04-14. Formalised 2026-04-16 by Andy's decision.

## Interpretation
The pattern suggests backing the predicted loser systematically extracts value from the weaker tail of the model's decision boundary. Even with superficial edge logic, the model's asymmetric confidence makes this unprofitable.

## Formalisation
- **Formalised**: 2026-04-16 by Andy's decision
- **Original threshold**: 20 bets (reached 18/18 -- Andy accepted Fred's recommendation for early formalisation)
- **Applied to**: All sports (NBA, Tennis, Snooker, Darts, Cricket, any future domain)

## Implementation
- Added to [[active-rules]] as hard constraint
- Applies across all domains where AutoStrategy places bets
- Fred to enforce in daily portfolio management

## Related
- [[never-back-predicted-loser]] (detailed rule)
- [[nba]]
- [[tennis-atp]]
- [[autostrategy]]

## Decision Log
- 2026-04-16: **FORMALISED** by Andy. Accepted Fred's early formalisation recommendation at 18/18 (2 short of 20-bet threshold). Statistical evidence conclusive.
- 2026-04-14: NBA regular-season close -- NBA 8/8, Tennis 10/10, Combined 18/18. Fred recommended formalisation. Decision flagged for Andy.
- 2026-04-10: NBA record updated to 0/6. Total now 0/9 across all sports. Strong case for early formalisation building.
- 2026-04-08: Added to [[active-rules]] with formalisation path
- 2026-03-20: Tennis added (0/3)
- 2026-03-15: NBA experiment started (0/3)

## Sources
- Paper trading logs: raw/autostrategy/AutoStrategy_Paper_v6.md
