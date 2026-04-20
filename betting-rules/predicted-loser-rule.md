# Rule: Predicted Loser (FORMALISED)
> Never back the model's predicted loser. Formalised 2026-04-16 by Andy at 18/18 live paper record across NBA and Tennis. Hard constraint, all sports.
> Last updated: 2026-04-20

## Status
**FORMALISED** — permanent hard constraint across all sports. First AutoStrategy rule to complete the full evidence cycle: paper experiment → statistical threshold → formalisation.

- Paper tracking: 2026-03-15 onward
- Early formalisation recommendation from Fred: 2026-04-14
- Andy authorised formalisation: 2026-04-16

## Experiment Design
### Hypothesis
Backing the model's predicted loser should generate value if market misprices the losing side. However, the model's confidence is asymmetrically distributed, making this a structural trap.

### Method
Track every bet where:
- Model predicts A will beat B (e.g., A > 60% probability)
- Odds suggest value betting on B (predicted loser)
- Place the bet and log outcome

### Results at formalisation
| Domain | Bets | Wins | Win Rate |
|--------|------|------|----------|
| NBA | 8 | 0 | 0% |
| Tennis | 10 | 0 | 0% |
| **Total** | **18** | **0** | **0%** |

**Confidence**: Strong. 0/18 across two live domains (NBA 8/8, Tennis 10/10) over ~6 weeks. At 18/18 the 95% CI on a 0% win rate is well below any plausible edge threshold. Formalised early (at 18, not 20) per Fred's 2026-04-14 recommendation and Andy's 2026-04-16 approval. No further paper tracking required.

## Interpretation
The pattern suggests backing the predicted loser systematically extracts value from the weaker tail of the model's decision boundary. Even with superficial edge logic, the model's asymmetric confidence makes this unprofitable.

## Formalisation
- **Formalised:** 2026-04-16 at 18/18 (early, 2 short of original 20-bet target)
- **Decision by:** Andy, on Fred's recommendation
- **Rationale:** At 18/18 with 0% wins, the remaining 2 bets add near-zero statistical weight. Procedural threshold honoured in spirit.

## Implementation
Now active as a hard constraint in all sports where AutoStrategy is deployed (NBA, Tennis, Snooker, Darts, Crypto paper, IPL queued):
1. Listed in [[active-rules]] as FORMALISED
2. Fred enforces on every bet recommendation when back online
3. Automated betting rule excludes predicted-loser bets pre-placement

## Related
- [[never-back-predicted-loser]] (detailed rule spec)
- [[nba]]
- [[tennis-atp]]
- [[autostrategy]]
- [[selectivity-is-everything]] — same underlying principle: don't force value where the model's signal is weak

## Decision Log
- 2026-04-16: **FORMALISED** per Andy's instruction. Status flipped from "paper tracking" to "formalised" across all three rule pages. Hard constraint, all sports. First rule to complete the full evidence cycle.
- 2026-04-14: NBA regular-season close — NBA 8/8, Tennis 10/10, Combined 18/18. Fred recommended early formalisation. Decision flagged for Andy.
- 2026-04-10: NBA record updated to 0/6. Total then 0/9 across all sports. Strong case for early formalisation building.
- 2026-04-08: Added to [[active-rules]] with formalisation path.
- 2026-03-20: Tennis added (0/3).
- 2026-03-15: NBA experiment started (0/3).

## Sources
- Paper trading logs: raw/autostrategy/AutoStrategy_Paper_v6.md
- Fred recommendation: operations/fred-decision-log.md (2026-04-14)
- Andy formalisation instruction: Slack #ttai-employees (2026-04-16 20:51)
