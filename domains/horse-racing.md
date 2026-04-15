# Horse Racing
> Concluded. No edge found despite 8-factor model.
> Last updated: 2026-04-08

## Model
8-factor model on public form data. Forward-only evaluation methodology.

## Status
Concluded (no further work planned)

## Key Results
- **Forward-only ROI**: -6.5%
- **Finding**: Public form data cannot overcome SP (starting price) market efficiency
- **Lesson learned**: Data leakage is pervasive in betting model development

## Journey
- **Initial result**: +72% ROI (later identified as data leakage)
- **Honest evaluation**: -6.5% ROI (after data-leakage controls)
- **Model signals**: 8-factor model identified genuine but weak signals
- **Gap**: Genuine signals not large enough to overcome bookmaker's margin (typically 3-5%)

## Active Rules
- None (domain concluded)

## Decision Log
- 2026-01-15: Formally concluded. No further investigation planned.
- 2025-12-20: Data-leakage lesson cemented. Moved to concluded status.
- 2025-11-30: Discovered leakage in initial +72% ROI result

## Links
- [[data-leakage-silent-killer]] — Principle discovered in this domain
- [[autostrategy]] — Strategy optimization methodology
- [[compound-evaluation]] — L1-L5 evaluation framework
- [[walk-forward-validation]] — Forward-only validation method
- [[betting-portfolio]] — Portfolio container

## Sources
- raw/autostrategy/autostrategy_STATUS.md
- raw/autostrategy/AutoStrategy_Paper_v6.md
