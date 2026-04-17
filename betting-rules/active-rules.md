# Active Betting Rules
> All current rules. Last updated: 2026-04-16

See [[betting-portfolio]] for portfolio overview and domain details.

| Rule | Domains | Evidence | Status |
|------|---------|----------|--------|
| [[injury-veto-80pct]] | NBA | MIL without Giannis (36/68 games) won at 5.00; MIN without Edwards won; DET without Cunningham won | Active |
| [[away-team-threshold]] | NBA | Higher variance on road eliminates value unless edge exceeds 20% | Active |
| [[never-back-predicted-loser]] | All sports | 0/18 bets. Formalised 2026-04-16. | **FORMALISED** -- hard constraint |
| [[grass-veto]] | Tennis | -20% ROI on 86 grass bets despite high apparent edge (phantom value) | Pending (implement before mid-June) |
| [[predicted-loser-rule]] | All sports | 0/18 across sports. Formalised 2026-04-16 at Andy's instruction. | **FORMALISED** |

## Rule Definition Index
- [[injury-veto-80pct]] — Only skip if player in 80%+ of games
- [[away-team-threshold]] — 20%+ edge for away underdogs (NBA)
- [[never-back-predicted-loser]] — Don't bet on model's predicted loser
- [[grass-veto]] — Tennis: no bets on grass (pending implementation)
- [[predicted-loser-rule]] — 0/18, 2 bets short of 20-bet threshold

## Implementation Notes
- **Grass veto**: Current state is logging predictions without betting. Deadline for automation: before mid-June grass season begins.
- **Predicted-loser rule**: FORMALISED 2026-04-16 at 18/18 (NBA 8/8, Tennis 10/10). Andy approved early formalisation per Fred's recommendation. Hard constraint across all sports. First rule to complete the full evidence cycle.
