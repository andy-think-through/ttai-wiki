# Compound Evaluation

> Five-level framework (L1–L5) for evaluating strategies. Each level catches different failure modes. Together they provide richer feedback than single-metric optimisation.
> Last updated: 2026-04-08

## Why Not Just Optimise One Metric?

Single-metric optimisation (accuracy, Sharpe, ROI) is fast but blind to failure modes. AutoStrategy's five-level framework trades speed for depth: you evaluate across five dimensions, weight them, and compute a compound score that only improves when the strategy is genuinely better.

The cost is lower iteration speed (more metrics to compute). The benefit is avoiding local optima and strategies that work by accident.

## The Five Levels

### L1: Training Accuracy (20% weight)

**What it measures**: Raw performance on data the strategy has seen.

**Why it matters**: Quick sanity check. If your strategy can't beat baseline on training data, it's clearly broken.

**Why it's insufficient**: Training accuracy is meaningless without L2 (generalisation). You can achieve 99% training accuracy and 45% holdout accuracy (severe overfitting).

**Implementation**: 
- For classification: accuracy, precision, recall (record all three)
- For value-betting: ROI on bets the model marked as profitable
- For ranking: NDCG or AUC on training set
- Compute nightly; it's fast

**Red flag**: If L1 is high but L2 is low, your strategy is overfitting. Increase regularisation or reduce model complexity.

### L2: Holdout Generalisation (35% weight — most important)

**What it measures**: Performance on held-out data that the strategy has never seen during optimisation.

**Why it matters**: This is the true test. If your strategy can't beat baseline on unseen data, it doesn't generalise and won't work in production.

**Critical**: Lock the holdout split **before** you start iterating. Otherwise, you're optimising the holdout and it becomes training data.

**Implementation**:
- Single train/holdout split (e.g., 70/30)
- Same metrics as L1 (accuracy, ROI, NDCG, etc.)
- Frozen for the entire optimisation cycle
- If possible, use a separate holdout from a different time period (for regime-dependent domains, see [[walk-forward-validation]])

**Interpretation**: If L2 doesn't improve, the iteration didn't work. Revert, regardless of L1.

**Red flag**: If L2 improves by >1% per iteration, something is wrong. Either:
- The holdout is too small (high variance in metric)
- You're accidentally training on the holdout
- The domain is highly non-stationary (regime shifts between train and holdout)

### L3: Synthetic Edge Cases + Minority-Class Checks (25% weight)

**What it measures**: 
1. Performance on synthetic boundary conditions (extreme values, out-of-distribution inputs)
2. Accuracy on minority classes (the "majority-class trap")

**Why it matters**: Many strategies work by default on the easy cases and fail on edge cases. Without L3, you optimise for the common case and break the rare case.

**The Majority-Class Trap (Critical)**

Scenario: Your tennis prediction model achieves 92% accuracy on a holdout set. Sounds great. But 87% of your test set is matches where the favourite is heavily favoured. If you just always pick the favourite, you'd get 87% accuracy for free. Your real accuracy on the minority class (underdogs) is only 45%.

L3 forces you to measure and improve both:
- Majority-class accuracy (favourites in tennis)
- Minority-class accuracy (underdogs in tennis)
- Compound minority metric: if either drops below threshold, flag

**Implementation**:
1. Identify your minority class (rare outcomes, unusual market conditions, small-value transactions, etc.)
2. Compute accuracy separately for majority and minority
3. Require majority-class accuracy ≥ baseline AND minority-class accuracy ≥ baseline - 5% (or tighter)
4. Synthetic edge cases: generate inputs at extreme parameter values (max/min market volatility, zero liquidity, etc.) and verify graceful degradation

**Example (Crypto, from [[crypto]])**:
- Majority case: Normal market conditions, moderate volatility
- Minority case: Flash crashes, 50%+ intraday moves
- Requirement: Strategy must handle both, not just ignore the rare case

**Red flag**: If L2 is high but L3 is low, your strategy is overfitting to the easy cases. Add L3 penalty or restructure the strategy.

### L4: LLM-as-Judge Coherence + Feature Influence Audit (20% weight)

**What it measures**:
1. **Coherence**: Does the strategy's reasoning make sense? Can an LLM validate the logic?
2. **Feature influence**: Are you actually using the features you claim to use?

**Why it matters**: A strategy can score well on L1–L3 by accident (right answer, wrong reason). If your reasoning is flawed, the strategy will break under new conditions or when the data distribution shifts.

**Implementation**:

*Coherence Audit*:
- Describe the strategy to an LLM: "This strategy recommends action X because of features A, B, and C. Is this reasoning sound?"
- Provide example decisions (input → output) and ask the LLM to evaluate
- Score based on: logic consistency, alignment with stated goals, absence of contradictions
- Can be automated as part of the eval loop

*Feature Influence Audit*:
- Use SHAP values, permutation importance, or feature ablation to measure which features actually drive decisions
- Compare to the strategy's stated features
- If the strategy claims to use feature A but ablation shows it has zero influence, flag as inconsistent
- Requirement: stated features must be in top-3 drivers of output

**Example (Tennis)**:
- Strategy says: "I predict based on head-to-head win %, player form, and court surface"
- Ablation shows: head-to-head (42% influence), court surface (8% influence), form (3% influence), seed ranking (47% influence, not mentioned)
- Issue: The strategy is actually driven by seed ranking, which is just a proxy for historical strength. It's not capturing the stated logic.
- Action: Rewrite the strategy to explicitly use seed ranking, or restructure to actually isolate the three stated features

**Red flag**: If L4 is low despite high L1–L3, your strategy works by accident. Investigate and rewrite for clarity.

### L5: Compound Score with Penalties

**What it measures**: Weighted average of L1–L4, adjusted for overfitting and base-rate coasting.

**Implementation**:

```
L5 = (0.20 * L1 + 0.35 * L2 + 0.25 * L3 + 0.20 * L4) - overfitting_penalty - base_rate_penalty
```

*Overfitting Penalty*:
- If (L1 - L2) > threshold (e.g., >3%), subtract from L5
- Magnitude: 0.5 points per 1% gap above threshold
- Prevents strategies that memorise training data

*Base-Rate Coasting Penalty*:
- If (strategy_return - base_rate_return) < safety_margin (e.g., <1%), subtract from L5
- Magnitude: 0.3 points per 0.1% margin missed
- Prevents "beating the base rate by accident" (e.g., 50.1% accuracy on 50/50 coin flip)

**Decision Rule**:
- If L5(new) > L5(best) + threshold (e.g., 0.5 points), keep the change
- Otherwise, revert
- Threshold prevents random noise from driving decisions

## Suggested Weights (Adjustable by Domain)

**Default (Path A — Clean Backtest Data)**:
- L1: 20%
- L2: 35% (highest trust, most important)
- L3: 25%
- L4: 20%

**Path B (Action-Entangled Data)**:
- L1: 15%
- L2: 30%
- L3: 35% (increase for robustness to selection bias)
- L4: 20%

**Path C (No Historical Data)**:
- L1: 0% (unavailable)
- L2: 0% (unavailable)
- L3: 50% (synthetic testing only)
- L4: 50% (coherence and causal reasoning)

Adjust based on your domain. If minority-class performance is critical (healthcare, fraud detection), increase L3. If interpretability is regulatory requirement, increase L4.

## Implementation Checklist

- [ ] Define metrics for L1 (training accuracy)
- [ ] Lock holdout split before iteration
- [ ] Define metrics for L2 (holdout generalisation)
- [ ] Identify minority class or edge cases for L3
- [ ] Implement synthetic edge-case tests
- [ ] Set up LLM coherence audit for L4
- [ ] Implement feature influence audit (SHAP or ablation)
- [ ] Define overfitting penalty formula
- [ ] Define base-rate coasting penalty formula
- [ ] Compute L5 and keep/revert threshold
- [ ] Automated eval loop (nightly or more frequent)
- [ ] Logging of all five levels per iteration

## Example Eval Output

```
Iteration 42 (Strategy v5.2):
L1 Training Accuracy: 0.87
L2 Holdout Generalisation: 0.81
L3 Edge Cases & Minority Class:
  - Edge case (extreme volatility): 0.74 [PASS]
  - Minority class (rare outcomes): 0.76 [PASS, baseline 0.71]
L4 Coherence & Feature Influence:
  - LLM Coherence: 0.88 [PASS]
  - Feature alignment (SHAP): 5/5 stated features in top-6 drivers [PASS]
Overfitting penalty: -0.1 (gap: 6%, threshold: 3%)
Base-rate penalty: 0 (edge: +1.2%)
L5 Compound Score: 0.78 [KEEP] (improvement: +0.03 vs v5.1)
```

## Links

- [[autostrategy]] — Framework that uses compound evaluation
- [[results-diagnostic]] — Post-hoc analysis of L5 scores
- [[walk-forward-validation]] — Alternative to single holdout for regime-dependent domains
- [[nba]], [[crypto]], [[tennis-atp]], [[efl-championship]] — Domains where L3/L4 caught subtle issues

## Sources

- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/AutoStrategy_SKILL_v3.md
