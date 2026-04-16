# Rule: Predicted Loser (FORMALISED)
> Never back the model's predicted loser. Formalised 2026-04-16 by Andy at 0/18. Hard constraint, all sports.
> Last updated: 2026-04-16

## Status
**FORMALISED** -- Andy approved formalisation on 2026-04-16 at 18/18 record (0% win rate). Hard constraint across all sports. First rule to complete the full evidence cycle: paper experiment -> statistical threshold -> formalisation.

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

**Confidence**: Strong. NBA 8/8, Tennis 10/10, combined 18/18. At 18/18 the 95% CI on a 0% win rate is well below any plausible edge threshold. Formalised early (at 18, not 20) per Fred's recommendation and Andy's approval.

## Interpretation
The pattern suggests backing the predicted loser systematically extracts value from the weaker tail of the model's decision boundary. Even with superficial edge logic, the model's asymmetric confidence makes this unprofitable.

## Formalisation
- **Formalised:** 2026-04-16 at 18/18 (early, 2 short of original 20-bet target)
- **Decision by:** Andy, on Fred's recommendation
- **Rationale:** At 18/18 with 0% wins, the remaining 2 bets add near-zero statistical weight. Procedural threshold honoured in spirit.

## Implementation
- Added to [[active-rules]] as hard constraint
- Applies to all sports (NBA, Tennis, Snooker, Darts, any future domain)
- Fred to enforce when back online

## Related
- [[never-back-predicted-loser]] (detailed rule)
- [[nba]]
- [[tennis-atp]]
- [[autostrategy]]

## Decision Log
- 2026-04-16: **FORMALISED.** Andy approved at 18/18. Hard constraint, all sports. First rule to complete full evidence cycle.
- 2026-04-14: NBA regular-season close -- NBA 8/8, Tennis 10/10, Combined 18/18. Fred recommended formalisation. Decision flagged for Andy.
- 2026-04-10: NBA record updated to 0/6. Total now 0/9 across all sports. Strong case for early formalisation building.
- 2026-04-08: Added to [[active-rules]] with formalisation path
- 2026-03-20: Tennis added (0/3)
- 2026-03-15: NBA experiment started (0/3)

## Sources
- Paper trading logs: raw/autostrategy/AutoStrategy_Paper_v6.md
