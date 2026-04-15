# Market Efficiency Varies Within Domain
> Edge is sub-domain specific; never aggregate across strata.
> Last updated: 2026-04-08

## The Principle
Market efficiency is not uniform within a domain. The Championship tier of [[efl-championship]] can be inefficient (positive ROI) while League One and League Two are efficient or exploitable-against (negative ROI). The difference is not mispricing; it's the signal-to-noise ratio. Lower tiers have more randomness, not more exploitable error.

## Where Discovered
[[efl-championship]] — Championship showed positive ROI in every experiment. League One/Two showed negative ROI in every experiment. Same league, same model, stratified results. The aggregated result was near-zero, which masked the sub-domain truth.

## The Fix
Always stratify by sub-domain:
- Sport/tier (Championship vs League One vs League Two)
- Event type (regular season vs playoffs vs finals)
- Surface (hard vs clay vs grass vs indoor)
- Other natural strata specific to the domain

Test each stratum independently. If a stratum shows persistent negative ROI, disable it in the live model.

## Where It Applies
- [[efl-championship]] by league tier
- [[tennis-atp]] by surface and tournament tier
- [[nba]] by season phase (regular season vs playoff)
- [[snooker]] by tournament type
- [[horse-racing]] by track condition and race class
- Any domain with hierarchical or multi-tier structure

## Exceptions
- Very high-volume strata can mask inefficiency through sample size alone
- Some strata (e.g., finals) may have too little data to draw conclusions
- Prior information about efficiency (e.g., published research) can override empirical stratification

## Links
- [[efl-championship]]
- [[tennis-atp]]
- [[nba]]
- [[snooker]]
- [[horse-racing]]
- [[phantom-value]]

## Sources
- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/autostrategy_STATUS.md
