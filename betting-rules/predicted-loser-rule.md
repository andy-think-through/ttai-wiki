# Rule: Predicted Loser (Formalised)
> Never back the model's predicted loser. Formalised 2026-04-16 at 0/18 record. Hard constraint, all sports.
> Last updated: 2026-04-16

## Status
**Formalised** -- active hard constraint across all sports. Combined record 0/18 (NBA 8/8, Tennis 10/10). Andy confirmed formalisation on 2026-04-16 after Fred recommended it on 2026-04-14. First rule to complete the full evidence cycle: paper experiment -> statistical threshold -> formalisation.

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

## Formalisation
- **Formalised:** 2026-04-16 by Andy (early, at 18/20 threshold)
- **Evidence at formalisation:** 0/18 across 2 sports (NBA 8/8, Tennis 10/10)
- **Rationale:** At 18/18 the 95% CI on a 0% win rate is already well below any plausible edge threshold. Waiting for 20 added procedural completeness, not statistical weight.

## Implementation
- Hard constraint in all sports (NBA, Tennis, Snooker, Darts, any future domain)
- Listed in [[active-rules]]
- Fred to enforce in daily portfolio management

## Related
- [[never-back-predicted-loser]] (detailed rule)
- [[nba]]
- [[tennis-atp]]
- [[autostrategy]]

## Decision Log
- 2026-04-16: **FORMALISED** by Andy. Hard constraint, all sports. First rule to complete the full paper -> threshold -> formalisation cycle.
- 2026-04-14: NBA regular-season close -- NBA 8/8, Tennis 10/10, Combined 18/18. Fred recommended formalisation. Decision flagged for Andy.
- 2026-04-10: NBA record updated to 0/6. Total now 0/9 across all sports. Strong case for early formalisation building.
- 2026-04-08: Added to [[active-rules]] with formalisation path
- 2026-03-20: Tennis added (0/3)
- 2026-03-15: NBA experiment started (0/3)

## Sources
- Paper trading logs: raw/autostrategy/AutoStrategy_Paper_v6.md
