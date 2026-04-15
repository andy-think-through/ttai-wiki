# Rule: Predicted Loser (Paper Tracking)
> Never back the model's predicted loser. Paper experiment at 0/6 bets, approaching formalisation at 20.
> Last updated: 2026-04-10

## Status
**Paper tracking** — currently logging results but not yet a formal rule. Will formalise when reaching 20 bets with 0% win rate.

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
| NBA | 6 | 0 | 0% |
| Tennis | 3 | 0 | 0% |
| **Total** | **9** | **0** | **0%** |

**Confidence**: Strengthening. NBA pred-loser paper record confirmed 6/6 losses (Apr 6-10 daily ops). Matches tennis 0/10 pattern noted in earlier analysis. At 20 bets with 0% win rate, formalise as permanent rule.

## Interpretation
The pattern suggests backing the predicted loser systematically extracts value from the weaker tail of the model's decision boundary. Even with superficial edge logic, the model's asymmetric confidence makes this unprofitable.

## Formalisation Threshold
- **Target**: 20 bets
- **Current**: 9 bets
- **Remaining**: 11 bets
- **Expected timeline**: Q2 2026
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
- 2026-04-10: NBA record updated to 0/6. Total now 0/9 across all sports. Strong case for early formalisation building.
- 2026-04-08: Added to [[active-rules]] with formalisation path
- 2026-03-20: Tennis added (0/3)
- 2026-03-15: NBA experiment started (0/3)

## Sources
- Paper trading logs: raw/autostrategy/AutoStrategy_Paper_v6.md
