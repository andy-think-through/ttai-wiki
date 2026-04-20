# Active Betting Rules
> All current rules. Last updated: 2026-04-20

See [[betting-portfolio]] for portfolio overview and domain details.

| Rule | Domains | Evidence | Status |
|------|---------|----------|--------|
| [[injury-veto-80pct]] | NBA | MIL without Giannis (36/68 games) won at 5.00; MIN without Edwards won; DET without Cunningham won | Active |
| [[away-team-threshold]] | NBA | Higher variance on road eliminates value unless edge exceeds 20% | Active |
| [[never-back-predicted-loser]] / [[predicted-loser-rule]] | NBA, Tennis, all AutoStrategy domains | 0/18 paper bets (NBA 8/8 + Tennis 10/10) | **FORMALISED (2026-04-16)** |
| [[grass-veto]] | Tennis | -20% ROI on 86 grass bets despite high apparent edge (phantom value) | Pending (implement before mid-June) |

## Rule Definition Index
- [[injury-veto-80pct]] — Only skip if player in 80%+ of games
- [[away-team-threshold]] — 20%+ edge for away underdogs (NBA)
- [[never-back-predicted-loser]] / [[predicted-loser-rule]] — Don't bet on model's predicted loser. **Formalised 2026-04-16.** First AutoStrategy rule to complete full evidence cycle.
- [[grass-veto]] — Tennis: no bets on grass (pending implementation)

## Implementation Notes
- **Predicted-loser rule**: Formalised 2026-04-16 following Fred's 2026-04-14 recommendation and Andy's Slack authorisation. 18/18 paper bets lost — statistical threshold comfortably cleared. Now a permanent filter applied at the model output stage across all AutoStrategy domains.
- **Grass veto**: Current state is logging predictions without betting. Deadline for automation: before mid-June grass season begins.

## Methodological Significance
The predicted-loser formalisation (2026-04-16) is the first time an AutoStrategy rule has completed the full hypothesis → paper-trade → threshold → formalisation pipeline. Worth noting as validation of the methodology before it's stretched to newer domains ([[snooker]], [[darts]], [[ipl]], [[crypto]]).

## Next Candidates for Formalisation
- [[grass-veto]] — needs implementation deadline (mid-June) more than additional evidence
- [[away-team-threshold]] — already active; long-running data needed to confirm threshold
