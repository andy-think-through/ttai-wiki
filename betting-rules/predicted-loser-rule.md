# Rule: Predicted Loser (Paper Tracking)
> Never back the model's predicted loser. Paper experiment at 0/18 bets, formalisation decision flagged for Andy.
> Last updated: 2026-04-15

## Status
**Paper tracking** — currently logging results but not yet a formal rule. Combined record now 0/18 across NBA and Tennis. Fred recommended formalising on 2026-04-14; decision pending Andy.

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

**Confidence**: Strong. NBA 8/8, Tennis 10/10, combined 18/18 as of 2026-04-14. 2 bets away from the 20-bet formalisation threshold. Fred recommended early formalisation in his 2026-04-14 NBA regular-season close update — at 18/18 the 95% CI on a 0% win rate is already well below any plausible edge threshold.

## Interpretation
The pattern suggests backing the predicted loser systematically extracts value from the weaker tail of the model's decision boundary. Even with superficial edge logic, the model's asymmetric confidence makes this unprofitable.

## Formalisation Threshold
- **Target**: 20 bets
- **Current**: 18 bets
- **Remaining**: 2 bets (or early formalisation per Andy)
- **Expected timeline**: Imminent
- **Trigger**: When 20 bets reached with ≤5% win rate (95% CI on 0%), formalise and apply across all sports

## Implementation Plan
Once formalised:
1. Add to [[active-rules]]
2. Implement as hard constraint in all sports where applicable (NBA, Tennis, Snooker, Darts, etc.)
3. Create automated betting rule to exclude predicted-loser bets

## Related
- [[never-back-predicted-loser]] (detailed rule)
- [[nba]]
- [[tennis-atp]]
- [[autostrategy]]

## Decision Log
- 2026-04-14: NBA regular-season close — NBA 8/8, Tennis 10/10, Combined 18/18. Fred recommended formalisation. Decision flagged for Andy.
- 2026-04-10: NBA record updated to 0/6. Total now 0/9 across all sports. Strong case for early formalisation building.
- 2026-04-08: Added to [[active-rules]] with formalisation path
- 2026-03-20: Tennis added (0/3)
- 2026-03-15: NBA experiment started (0/3)

## Sources
- Paper trading logs: raw/autostrategy/AutoStrategy_Paper_v6.md
