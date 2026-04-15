# Active Betting Rules
> All current rules. Last updated: 2026-04-08

See [[betting-portfolio]] for portfolio overview and domain details.

| Rule | Domains | Evidence | Status |
|------|---------|----------|--------|
| [[injury-veto-80pct]] | NBA | MIL without Giannis (36/68 games) won at 5.00; MIN without Edwards won; DET without Cunningham won | Active |
| [[away-team-threshold]] | NBA | Higher variance on road eliminates value unless edge exceeds 20% | Active |
| [[never-back-predicted-loser]] | NBA, Tennis | 0/6 paper bets successful; approaching 20-bet formalisation | Active |
| [[grass-veto]] | Tennis | -20% ROI on 86 grass bets despite high apparent edge (phantom value) | Pending (implement before mid-June) |
| [[predicted-loser-rule]] | NBA, Tennis | Paper tracking. 0/6 successful. Formalise at 20 bets. | Active |

## Rule Definition Index
- [[injury-veto-80pct]] — Only skip if player in 80%+ of games
- [[away-team-threshold]] — 20%+ edge for away underdogs (NBA)
- [[never-back-predicted-loser]] — Don't bet on model's predicted loser
- [[grass-veto]] — Tennis: no bets on grass (pending implementation)
- [[predicted-loser-rule]] — 0/6, approaching formalisation at 20

## Implementation Notes
- **Grass veto**: Current state is logging predictions without betting. Deadline for automation: before mid-June grass season begins.
- **Predicted-loser rule**: Currently at 6/20 bets. When reaching 20 bets with 0% win rate, formalise as permanent rule across all sports.
