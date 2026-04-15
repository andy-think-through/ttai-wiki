# Walk-Forward Validation

> Rolling-fold evaluation for regime-dependent domains. Replaces single train/holdout split with 7 rolling folds to guard against overfitting to a specific time period.
> Last updated: 2026-04-08

## The Problem: Regime Shifts and Hidden Overfitting

A strategy can achieve excellent performance in a single train/holdout split and fail catastrophically in production. This happens when:

1. **Regime shifts**: The market, platform, or environment changes between training and deployment (player trades in sports, algorithm updates in platforms, volatility spikes in crypto)
2. **Luck**: The holdout period happens to be favourable to your strategy by chance
3. **Non-stationarity**: Historical patterns don't hold going forward

**Example (Crypto Discovery)**:
- Single holdout evaluation: +3.55 Sharpe ratio (excellent)
- Walk-forward evaluation (7 folds): Average -0.82 Sharpe ratio, with one fold at -3.67 (disaster)
- Conclusion: Strategy was overfitted to a lucky holdout period (bull market 2023). Failed in bear market (2024) and sideways market (2025).

Traditional single train/holdout validation misses this entirely. Walk-forward validation catches it by forcing the strategy to prove itself across multiple regime shifts.

## How Walk-Forward Validation Works

### 7 Rolling Folds Architecture

Divide historical data into 7 consecutive time periods. Each fold is:
- Training period: Folds 1-6 (or subsets)
- Test period (holdout): Fold 7 (or next sequential fold)
- Strategy trained on earlier data; evaluated on later data (forward-only, no look-ahead)

Example timeline (2 years of daily data = 500 trading days):
```
Fold 1: Days 1-100     (training)
Fold 2: Days 101-200   (training)
Fold 3: Days 201-300   (training)
Fold 4: Days 301-400   (training)
Fold 5: Days 401-500   (training)
Fold 6: Days 501-600   (NEW DATA, training)
Fold 7: Days 601-700   (TEST, holdout)
```

For each fold configuration:
1. Train strategy on all earlier folds
2. Freeze strategy parameters
3. Evaluate on the next fold (holdout)
4. Record metrics
5. Move forward (fold 2 uses folds 1+2 as training, fold 3 as test; etc.)

### Evaluation Rule

Strategy must achieve **positive metrics on majority of folds (minimum 5/7)**:
- If 6/7 folds pass: Strategy is robust (one regime shift tolerated)
- If 5/7 folds pass: Strategy is marginally robust (edge case regime causes failure)
- If 4/7 or fewer pass: Strategy fails; revert or redesign

**Metrics consistency**: Use the same L1–L5 compound score on each fold. Report:
- Mean score across folds (average performance)
- Min score across folds (worst-case regime)
- Std dev (consistency)

Example output:
```
Walk-Forward Results:
Fold 1: L5 = 0.71
Fold 2: L5 = 0.82
Fold 3: L5 = 0.65
Fold 4: L5 = 0.78
Fold 5: L5 = 0.84
Fold 6: L5 = 0.59
Fold 7: L5 = 0.70
Mean: 0.72, Min: 0.59, Std Dev: 0.09
Result: 7/7 PASS (robust across all regimes)
```

## Regime-Dependent Domains (Where This Applies)

Walk-forward validation is critical in any domain where:
- **Time matters**: Outcomes depend on external state that changes over time
- **Regime shifts occur**: The system's dynamics change (market crashes, platform policy changes, seasonal effects)
- **History doesn't repeat perfectly**: Past is useful but not identical to future

**Applicable domains**:
- Financial markets (crypto, equities, commodities): volatility regime, correlation structure, liquidity
- Sports (tennis, NBA, EFL): player form, team composition, coaching changes
- E-commerce / SaaS: user behaviour shifts, platform algorithm changes, competitive landscape
- Betting (sports, value): odds distribution, market efficiency, crowd psychology

**Not applicable**:
- Pure prediction tasks without time dependence (image classification, NLP without temporal component)
- Stationary domains where past = future (constants, fixed physical laws)

## Discovered Application: Crypto (2025)

Andy discovered walk-forward validation necessity during crypto value-betting optimisation:

**Initial approach**: Single train/holdout split on 2023-2024 data
- Result: +3.55 Sharpe ratio (promising)
- Decision: Deploy to live trading

**Reality check**: Applied walk-forward validation retrospectively (7 folds across 2021-2025)
- Results: Mean Sharpe -0.82 across 7 folds
- Breakdown:
  - Folds 1-3 (2021-2023, bull market): +1.2 to +2.1 Sharpe (strategy thrives)
  - Folds 4-5 (2024, bear market): -1.5 to -3.67 Sharpe (catastrophic failure)
  - Folds 6-7 (2025, sideways): -0.3 to +0.1 Sharpe (barely breaks even)
- Conclusion: Only 3/7 folds pass. Strategy fails.

**Root cause**: The original +3.55 evaluation was on 2023-2024 data, which happened to include both a bull market and transition to bear. But the strategy was optimised to the bull market characteristics (high volatility, trend-following signals work). In bear market, those signals reversed.

**Action taken**:
- Redesigned strategy with separate logic for bull/bear/sideways regimes
- Re-evaluated with walk-forward: 5/7 folds now pass (marginal but acceptable)
- Planned live A/B test to validate regime detection works in real-time

## Applying Walk-Forward Validation

### Step 1: Define Fold Boundaries

**Time-based**: Divide data chronologically into equal-duration chunks (each fold = ~15% of total data)
- For 2 years of daily data: ~100 days per fold
- For 10 years of data: ~500 days per fold
- Minimum: 30 observations per fold

**Regime-aware** (optional): If you know regime shifts occurred at specific dates, align fold boundaries with shifts
- Example: 2023 bull → 2024 bear transition → align fold boundary to Jan 2024
- Trade-off: Reduces sample size per fold, but tests strategy against known regime changes

### Step 2: Iterate Within Each Fold

For each fold:
1. Train strategy on all prior folds (forward-only, no future data)
2. Lock parameters
3. Evaluate on current fold
4. Move to next fold (don't retrain; frozen parameters apply to all future folds)

**Alternative (more computationally expensive)**: Retrain from scratch on each fold boundary. More robust but slower. Recommended for strategic validation.

### Step 3: Aggregate and Interpret

Compute:
- **Mean L5 score**: Average across all folds (overall robustness)
- **Min L5 score**: Worst fold (worst-case regime)
- **Pass rate**: Number of folds where L5 ≥ threshold (must be 5/7 or higher)
- **Consistency (Std Dev)**: Low std dev = consistent across regimes; high std dev = strategy is regime-dependent (fragile)

Interpretation rules:
- **7/7 pass, low std dev**: Excellent. Strategy is regime-robust.
- **6/7 pass**: Good. One regime shift causes minor degradation.
- **5/7 pass**: Marginal. Acceptable if that one failing fold is known edge case (e.g., market halt).
- **4/7 or fewer**: Fail. Strategy is not viable; redesign required.

### Step 4: Root-Cause Analysis (For Failed Folds)

If any fold fails (L5 below threshold):
1. Identify the fold's regime: What was the market/environment like during that period?
2. Analyse strategy performance in detail: Which decisions failed? Which features were unreliable?
3. Hypothesise fix: Does the strategy need separate logic for this regime? Missing feature? Different thresholds?
4. Test fix on failed fold only; then re-validate across all 7 folds

**Example (Tennis)**:
- Fold 4 fails (grass court season). Analysis shows strategy underperforms on grass courts.
- Hypothesis: Grass is fast; serves dominate; H2H % (a feature) becomes less predictive.
- Fix: Add court-surface adjustment. Reduce H2H weight on grass; increase serve-speed weight.
- Re-validate: Now all 7 folds pass.

## Implementation Checklist

- [ ] Define time-based fold boundaries (7 folds, chronological)
- [ ] Align fold boundaries with known regime shifts (if applicable)
- [ ] Ensure each fold has minimum 30 observations
- [ ] Implement forward-only training (no look-ahead bias)
- [ ] Automate fold iteration loop
- [ ] Compute L1–L5 metrics for each fold
- [ ] Track mean, min, std dev across folds
- [ ] Implement pass/fail rule (5/7 minimum)
- [ ] Root-cause analysis for failed folds
- [ ] Iterative redesign with re-validation loop
- [ ] Final documentation: "Walk-forward validation passed 6/7 folds. Failure regime: X. Mitigation: Y."

## Differences from Standard Cross-Validation

| Aspect | Standard K-Fold CV | Walk-Forward Validation |
|--------|-------------------|------------------------|
| Fold order | Random | Temporal (chronological) |
| Training scope | Random subset | All prior data |
| Use case | Stationary data | Time-dependent data |
| Look-ahead bias risk | Low | Zero (forward-only enforced) |
| Regime robustness | Not tested | Core purpose |

## Key Principle

**Walk-forward validation answers the question**: "If I deploy this strategy today, and the regime shifts tomorrow, will it still work?" A single train/holdout split cannot answer this. A walk-forward validation can.

## Links

- [[autostrategy]] — Integrates walk-forward validation for regime-dependent strategies
- [[compound-evaluation]] — L1–L5 metrics applied to each walk-forward fold
- [[results-diagnostic]] — Root-cause analysis for failed folds
- [[crypto]], [[tennis-atp]], [[nba]] — Domains where walk-forward validation caught overfitting

## Sources

- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/AutoStrategy_SKILL_v3.md
- Andy Allen's crypto strategy discovery (2025)
