# Rule: Never Back Predicted Loser
> NBA + Tennis. Do not bet on model's predicted loser, even with edge.
> Status: **FORMALISED** (2026-04-16) — full evidence cycle complete.
> Last updated: 2026-04-20

> **Note:** This page and [[predicted-loser-rule]] describe the same rule and should be consolidated. Treat this page as the canonical entry in [[active-rules]] indexing; narrative/decision log lives on [[predicted-loser-rule]].

## Principle
When a model predicts team/player A will lose to team/player B, backing B (the predicted loser in a head-to-head) seems profitable if the model shows edge. However, this is a structural trap:

- The model's confidence is asymmetric: high confidence in A beating B
- The inverse (backing B) involves betting against the model's strongest signal
- Even with apparent edge in odds, backing the predicted loser extracts value from a weaker part of the model's decision boundary

**Result**: Consistently unprofitable in practice, despite superficial edge logic.

## Evidence
| Domain | Bets | Win Rate | Status |
|--------|------|----------|--------|
| NBA | 8 | 0/8 | Evidence complete |
| Tennis | 10 | 0/10 | Evidence complete |
| **Total** | **18** | **0/18** | **Formalised** |

The rule completed its full 18-bet evidence cycle with a 0% win rate — the first AutoStrategy rule to reach full formalisation through the paper-trading pipeline.

## Rule
**Never place a bet where:**
- Model predicts team/player A with >50% probability
- Bet backs team/player B (predicted loser)
- Even if | Market Implied Prob(B) - Model Prob(B) | > edge threshold

**Exception**: None. This is an absolute rule, now applied across all AutoStrategy domains (NBA, Tennis, Snooker, Darts, IPL, Crypto trading heuristics).

## Implementation Status
- **FORMALISED** 2026-04-16 at 18/18 bets (NBA 8/8 + Tennis 10/10)
- Authorised via Slack by Andy following Fred's 2026-04-14 recommendation
- Now a permanent filter at the model output stage, not a discretionary rule

## Decision Log
- 2026-04-16: **Formalised.** Andy authorised via [[ttai-slack-bridge]] in #ttai-employees
- 2026-04-14: Fred (AutoStrategy agent) recommended formalisation — threshold met earlier than originally projected (18 vs 20 bets, but 0% win rate held firm)
- 2026-04-08: Added to [[active-rules]]. Approaching formalisation at 20 bets
- 2026-03-20: Tennis revealed pattern (0/3 upsets)
- 2026-03-15: NBA experiment started (0/3)

## Significance
First rule to complete the full AutoStrategy evidence cycle: hypothesis → paper trading → statistical threshold → formalisation. Validates the cross-domain paper-trading methodology before it's applied to newer domains (Snooker, Darts, IPL, Crypto).

## Related
- [[predicted-loser-rule]] — detailed rule page with full history
- [[nba]]
- [[tennis-atp]]
- [[autostrategy]]
- [[ttai-slack-bridge]] — mechanism for Fred's recommendation + Andy's authorisation

## Sources
- Paper trading logs: raw/autostrategy/AutoStrategy_Paper_v6.md
- Slack thread: #ttai-employees (2026-04-14 → 2026-04-16)
