# Phantom Value
> Apparent edge can be structural illusion, not real mispricing.
> Last updated: 2026-04-08

## The Principle
High disagreement between model predictions and market prices looks like mispricing. But in high-randomness sub-domains, the disagreement can be noise, not signal. The market price reflects true probabilities; the model's disagreement reflects overfitting to historical noise.

## Where Discovered
[[tennis-atp]] grass courts—model showed apparent 20% edge on grass-court predictions. Backtested ROI: -20%. The signal was phantom. Root cause: grass is lower-volume and higher-randomness than hard/clay; the model was fitting noise.

[[efl-championship]] League One/Two—similar pattern. Lower tier = more randomness = more apparent disagreement = less actual mispricing. ROI was consistently negative despite high model confidence.

## The Fix
Stratify by sub-domain (tier, surface, event type) and test each stratum independently. Don't aggregate across strata. If a stratum shows negative ROI, disable it.

## Where It Applies
Any domain with sub-categories of varying randomness:
- [[tennis-atp]] by surface (hard, clay, grass, indoor)
- [[nba]] by game type (regular season, playoff, back-to-back)
- [[efl-championship]] by tier (Championship, League One, League Two)
- [[snooker]] by tournament type
- [[horse-racing]] by track condition and class

## Exceptions
- In very low-randomness domains (e.g., chess rating prediction), high disagreement is more likely to be signal
- When there's a known data quality issue (e.g., outdated form), disagreement can be real signal even in high-randomness sub-domains
- Consensus models that aggregate many sources can be more trustworthy than single-model predictions

## Links
- [[tennis-atp]]
- [[efl-championship]]
- [[nba]]
- [[snooker]]
- [[horse-racing]]

## Sources
- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/autostrategy_STATUS.md
