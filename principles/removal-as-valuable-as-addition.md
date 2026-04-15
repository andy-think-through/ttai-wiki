# Removal as Valuable as Addition
> Removing features can be as valuable as adding them; exploitation loops never remove.
> Last updated: 2026-04-08

## The Principle
Feature engineering is typically thought of as additive—new features, new signals, new inputs. But subtractive engineering (removing noisy or redundant features) can deliver equal or greater gains. The exploitation loop never explores subtraction because it's structured around iterating within a fixed baseline.

## Where Discovered
[[nba]] live-betting model—a feature called "streak dampening" was part of the working baseline. Removing it improved holdout validation ROI by +0.7% and held +0.8% on validation set. The feature was adding noise, not signal.

The [[results-diagnostic]] framework can systematically identify subtraction opportunities by analyzing per-feature contribution and noise ratios.

## Where It Applies
Any system where complexity has accumulated:
- [[nba]] — feature removal in predictive models
- [[mark]] — email template simplification (fewer sections, clearer call-to-action)
- [[consulting]] — proposal simplification (fewer use cases, tighter narrative)
- Any accumulation system — codebases, processes, product features

The principle is: if a feature isn't pulling its weight, removing it is a valid optimization path.

## Exceptions
- Features with occasional but critical impact (e.g., injury flags in sports) should not be removed just because average contribution is low
- Features that enable interpretability or compliance should not be removed even if they reduce accuracy
- Network effects: removing a feature can break downstream dependencies even if the feature itself is low-value

## Links
- [[nba]]
- [[mark]]
- [[consulting]]
- [[results-diagnostic]]

## Sources
- raw/autostrategy/daily-skill-lessons-learned.md
- raw/autostrategy/autostrategy_STATUS.md
