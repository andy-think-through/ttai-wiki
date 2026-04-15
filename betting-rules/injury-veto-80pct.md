# Rule: Injury Veto (80% Threshold)
> NBA only. Skip bet only if star player has played 80%+ of season and is newly ruled out.
> Last updated: 2026-04-08

## Principle
When a star player is ruled out, the question is: **Is this new information, or is it already reflected in the Elo model?**

- If a player has played 80%+ of games: Their typical presence/absence pattern is fully embedded in team Elo. A sudden withdrawal is **genuine new information** and may warrant skipping the bet.
- If a player has played <80% of games: The model has already adapted to frequent absences. The bet reflects their typical availability pattern. A withdrawal is **not surprising** and the bet stands.

## Evidence
| Team | Player | Games Played | Season | Outcome | Notes |
|------|--------|-------------|--------|---------|-------|
| MIL | Giannis Antetokounmpo | 36/68 | 2025/26 | Won at 5.00 | Below 80% threshold. Veto did not apply. Bet successful. |
| MIN | Anthony Edwards | 42/75 | 2024/25 | Won | Below 80% threshold. Veto did not apply. Bet successful. |
| DET | Cade Cunningham | 38/70 | 2025/26 | Won | Below 80% threshold. Veto did not apply. Bet successful. |

**Interpretation**: All three examples show that backing teams missing frequently-absent stars generates value. The veto rule correctly avoids false positives.

## Application
**Do not skip bet if:**
- Player has been injured/unavailable frequently throughout the season (threshold: <80% games played)
- Elo model has already adjusted to their typical absence rate

**Do skip bet if:**
- Player has played 80%+ of games (established as reliable)
- Suddenly ruled out (genuine new information)
- New information might not be reflected in pre-game odds

## Implementation Status
- Active
- Used in NBA domain evaluation since March 2026

## Decision Log
- 2026-03-15: Formalised 80% threshold after observing wins on Giannis (36/68), Edwards, Cunningham absences
- 2026-03-01: Initial rule concept: distinguish Elo-embedded absences from new information

## Related
- [[nba]]
- [[autostrategy]]

## Sources
- NBA injury data via ESPN
- Backtest results: raw/autostrategy/AutoStrategy_Paper_v6.md
