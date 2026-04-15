# Derivative Markets Harder Than Primary
> Props and secondary markets are structurally harder to predict than primary markets.
> Last updated: 2026-04-08

## The Principle
Predicting who wins (primary market) is harder than predicting specific props/derivatives (corners, assists, etc.), but props have irreducible randomness that exceeds primary-market randomness by multiples. Example: corner count has σ ≈ 3.0 per match. This floor of randomness makes props much harder to beat systematically.

## Where Discovered
[[football-corners]] — attempted corner-count prediction. Statistical analysis showed σ ≈ 3.0 inherent randomness per match. After fitting features, residual σ remained near 2.8. The model captured minimal signal; most variation was irreducible randomness. ROI was persistently negative.

Contrast with [[nba]] (primary market: who wins): σ is lower because win/loss is a binary outcome; the signal-to-noise ratio is much cleaner. Elo-based and rating-based architectures work well.

## The Fix
- Focus on primary markets where theoretical signal-to-noise is higher
- If tackling derivatives, stratify by variation type: is the randomness systematic (exploitable) or truly random?
- Use predictability ceiling analysis before building a model
- Ensemble multiple data sources if attempting derivatives

## Where It Applies
- [[nba]] (primary: match winner) vs props (points scored, assists, etc.)
- [[tennis-atp]] (primary: match winner) vs props (aces, breaks, etc.)
- [[football-corners]] (derivative: corner count) vs primary (match winner)
- Any sport with both match betting and prop betting
- [[snooker]] frame betting (primary) vs specific-shot props (derivative)

## Exceptions
- Very liquid derivative markets can be more efficient, reducing edge, but also have more traders hunting the same inefficiency
- Some derivatives have external drivers (e.g., rain in cricket affecting deliveries) that create exploitable structure
- Live in-play derivatives can have different signal-to-noise than pre-match

## Links
- [[nba]]
- [[tennis-atp]]
- [[football-corners]]
- [[snooker]]
- [[phantom-value]]

## Sources
- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/daily-skill-lessons-learned.md
