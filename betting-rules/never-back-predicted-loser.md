# Rule: Never Back Predicted Loser
> NBA + Tennis. Do not bet on model's predicted loser, even with edge.
> Last updated: 2026-04-15

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

All bets with apparent edge failed. 18/18 as of 2026-04-14 — 2 bets short of the formalisation threshold. Fred has recommended early formalisation.

## Rule
**Never place a bet where:**
- Model predicts team/player A with >50% probability
- Bet backs team/player B (predicted loser)
- Even if | Market Implied Prob(B) - Model Prob(B) | > edge threshold

**Exception**: None. This is an absolute rule.

## Implementation Status
- Active (paper tracking)
- Formalisation: At 20 bets with 0% win rate, make permanent across all sports

## Progress Toward Formalisation
- Current: 18/20 bets (0% win rate)
- Target: 20 bets to meet statistical threshold
- Timeline: Imminent — Fred recommended early formalisation on 2026-04-14

## Decision Log
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
