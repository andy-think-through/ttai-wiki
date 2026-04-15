# Active Betting Rules
> All current rules. Last updated: 2026-04-15

See [[betting-portfolio]] for portfolio overview and domain details.

| Rule | Domains | Evidence | Status |
|------|---------|----------|--------|
| [[injury-veto-80pct]] | NBA | MIL without Giannis (36/68 games) won at 5.00; MIN without Edwards won; DET without Cunningham won | Active |
| [[away-team-threshold]] | NBA | Higher variance on road eliminates value unless edge exceeds 20% | Active |
| [[never-back-predicted-loser]] | NBA, Tennis | 0/18 paper bets; Fred recommended formalising 2026-04-14 | Active (paper); formalisation pending Andy |
| [[grass-veto]] | Tennis | -20% ROI on 86 grass bets despite high apparent edge (phantom value) | Pending (implement before mid-June) |
| [[predicted-loser-rule]] | NBA, Tennis | Paper tracking. 0/18 across sports. 2 bets short of 20-bet threshold. | Active |

## Rule Definition Index
- [[injury-veto-80pct]] — Only skip if player in 80%+ of games
- [[away-team-threshold]] — 20%+ edge for away underdogs (NBA)
- [[never-back-predicted-loser]] — Don't bet on model's predicted loser
- [[grass-veto]] — Tennis: no bets on grass (pending implementation)
- [[predicted-loser-rule]] — 0/18, 2 bets short of 20-bet threshold

## Implementation Notes
- **Grass veto**: Current state is logging predictions without betting. Deadline for automation: before mid-June grass season begins.
- **Predicted-loser rule**: Currently at 18/20 bets (NBA 8/8, Tennis 10/10). Fred recommended early formalisation on 2026-04-14 at regular-season close. Decision flagged for Andy.
