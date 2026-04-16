# Rule: Never Back Predicted Loser
> All sports. Do not bet on model's predicted loser, even with edge. Formalised 2026-04-16.
> Last updated: 2026-04-16

## Principle
When a model predicts team/player A will lose to team/player B, backing B (the predicted loser in a head-to-head) seems profitable if the model shows edge. However, this is a structural trap:

- The model's confidence is asymmetric: high confidence in A beating B
- The inverse (backing B) involves betting against the model's strongest signal
- Even with apparent edge in odds, backing the predicted loser extracts value from a weaker part of the model's decision boundary

**Result**: Consistently unprofitable in practice, despite superficial edge logic.

## Evidence
| Domain | Bets | Win Rate | ROI |
|--------|------|----------|-----|
| NBA | 8 | 0/8 | Paper loss |
| Tennis | 10 | 0/10 | Paper loss |
| **Total** | **18** | **0/18** | **Paper loss** |

All bets with apparent edge failed. 18/18 as of 2026-04-14. Formalised by Andy on 2026-04-16 at Fred's recommendation.

## Rule
**Never place a bet where:**
- Model predicts team/player A with >50% probability
- Bet backs team/player B (predicted loser)
- Even if | Market Implied Prob(B) - Model Prob(B) | > edge threshold

**Exception**: None. This is an absolute rule.

## Implementation Status
- **Formalised** -- active hard constraint across all sports (2026-04-16)
- Enforced by Fred in daily portfolio management

## Decision Log
- 2026-04-16: **FORMALISED** by Andy. Hard constraint, all sports. First rule to complete paper -> threshold -> formalisation cycle.
- 2026-04-14: NBA regular-season close pushed record to 8/8 NBA, 10/10 Tennis, 18/18 combined. Fred recommended formalisation. Decision flagged for Andy.
- 2026-04-08: Added to [[active-rules]]. Approaching formalisation at 20 bets.
- 2026-03-20: Tennis revealed pattern (0/3 upsets)
- 2026-03-15: NBA experiment started (0/3)

## Related
- [[nba]]
- [[tennis-atp]]
- [[autostrategy]]

## Sources
- Paper trading logs: raw/autostrategy/AutoStrategy_Paper_v6.md
