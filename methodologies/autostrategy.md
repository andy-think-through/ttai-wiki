# AutoStrategy

> Extends Karpathy's autoresearch from parameter tuning to genuine strategy design through mutable strategy files, five-level compound evaluation, and dual-mode autoresearch loops.
> Last updated: 2026-04-20

## Overview

AutoStrategy is a methodology for algorithmically optimising strategies in domains where outcomes are measurable and iterative improvement is possible. It bridges the gap between Karpathy's parameter-tuning autoresearch and the qualitative nature of strategy design by making strategies explicitly mutable and evaluable.

The core insight is that strategy design can be treated as an optimisation problem: if you can encode a strategy as a mutable file (plain English instructions, decision trees, or rule sets), measure outcomes objectively, and systematically iterate, you can apply automated improvement loops.

## Three Core Components

### 1. Mutable Strategy File

The strategy is stored in a plain-text file that describes:
- What decisions the system should make
- When to make them
- How to evaluate success
- What to adjust based on feedback

This differs from traditional strategy documents (written once, reviewed quarterly) because it's designed to be modified programmatically and empirically tested after each change.

The strategy must be specific enough to execute consistently (so results are comparable) but flexible enough to be modified in meaningful ways.

### 2. Five-Level Compound Evaluation (L1-L5)

Rather than optimising a single metric, AutoStrategy evaluates improvements across five levels, each catching different failure modes:

**L1: Training Accuracy (20% weight)**
- Raw performance on the data your strategy sees
- Catches gross incompetence
- Fast feedback loop (can evaluate daily)
- On its own, meaningless (overfitting trap)

**L2: Holdout Generalisation (35% weight — most important)**
- Performance on unseen data (single holdout split)
- The real test of whether your strategy generalises
- If your strategy can't beat baseline here, it doesn't work
- Must be locked before you start iterating to avoid optimising the holdout

**L3: Synthetic Edge Cases + Minority-Class Checks (25% weight)**
- Explicit testing of boundary conditions (e.g., extreme market regimes)
- Mandatory minority-class accuracy check (the majority-class trap)
- Scenario: You optimise for tennis accuracy and hit 92% overall. But 87% of your test set is favourites, so you're really just picking favourites and getting them right. Your minority-class accuracy (underdogs) is 45%. L3 forces you to solve both.
- Prevents strategies that work by accidentally matching the prior distribution

**L4: LLM-as-Judge Coherence + Feature Influence Audit (20% weight)**
- Coherence: Does the strategy's reasoning hold up under scrutiny? Can an LLM validate that the output makes sense?
- Feature influence: Are you actually using the features you claim to use? Feature ablation or SHAP values to confirm
- Catches strategies that work by accident (right answer, wrong reason)

**L5: Compound Score with Penalties (aggregate)**
- Weighted average of L1–L4
- Subtract overfitting penalty: If training > holdout by >X%, reduce score
- Subtract base-rate coasting penalty: If strategy beats base rate by <margin-of-safety, flag as risky
- Only improvements that survive all five levels are incorporated

## Suggested Weights

- L1: 20% (speed/feedback, low trust)
- L2: 35% (generalisation, highest trust)
- L3: 25% (edge cases and fairness)
- L4: 20% (interpretability and mechanistic validation)

For Path B data (action-entangled), increase L3 weight and add two-stage simulation calibration (see Data Paths below).

## Dual-Mode Autoresearch Loop

### Exploitation (75% budget)

Iterate on the current best strategy:
1. Hypothesise a change (informed by recent results or diagnostic audit)
2. Modify the mutable strategy file
3. Evaluate on L1–L5
4. If L5 improves and L2 doesn't degrade: keep
5. Otherwise: revert

Exploitation converges on local optima. Keep the iteration cycle tight (nightly or bi-daily evaluation).

### Exploration (25% budget)

Step outside the current strategy:
1. Generate blank-slate alternatives (different logic, different feature set)
2. Evaluate against baseline on L5
3. If competitive: branch into new exploitation round
4. Otherwise: discard and try another direction

Exploration prevents convergence to mediocre local optima. Force it: at least 25% of your iteration budget should go to fundamentally different approaches.

## Data Paths

### Path A: Clean Backtest Data

Pre-collected, non-action-entangled data where historical outcomes are known.
- Example: tennis historical matches, crypto OHLCV bars
- Forward-only evaluation applies straightforwardly
- L1–L5 evaluation at full strength

**Mandatory**: Paper-trading audit before trusting backtests. Even clean backtest data has surprises (regime shifts, data quality issues, look-ahead bias).

### Path B: Action-Entangled Data

Data where the strategy's actions change the outcomes (e.g., if Mark decides not to contact a lead, we never learn whether that lead converted).
- Requires two-stage simulation calibration
- First stage: estimate counterfactual outcomes (what would have happened if we'd acted differently?)
- Second stage: evaluate strategy on calibrated estimates
- Increase L3 weight; add causal mechanism verification in L4
- More brittle than Path A; validate against live experiments

### Path C: No Data, Limited Historical Record

Applicable to novel strategies or newly launched products.
- L1 and L2 are unavailable
- Rely on L3 (synthetic testing) and L4 (coherence audit)
- Slower convergence; higher risk
- Pair with rapid live-experiment cycles (A/B tests, controlled rollouts)

## Forward-Only Evaluation (Critical Constraint)

Strategies must be evaluated on data in temporal order, never training on future data to predict past outcomes. This is non-negotiable in regime-dependent domains (financial markets, platform algorithm changes, seasonal businesses).

Use walk-forward validation to confirm regime robustness (see [[walk-forward-validation]]).

## Implementation Checklist

- [ ] Strategy file written in plain language (or decision tree format)
- [ ] L1–L5 metrics defined and automated
- [ ] Holdout split locked before iteration
- [ ] Forward-only data ordering enforced
- [ ] Minority-class accuracy explicitly checked in L3
- [ ] Feature influence audit in L4
- [ ] Overfitting and base-rate penalties calibrated
- [ ] Exploitation loop running (nightly or bi-daily)
- [ ] Exploration cycle (25% budget) scheduled
- [ ] Paper-trading or live-experiment audit planned before deployment
- [ ] **TASK.md explicitly requires Claude API / tool use to propose each strategy change** (see audit below)

## Audit: Pre-scripted Search vs Genuine Autoresearch (2026-04-14)

A post-hoc audit of Claude Code AutoStrategy sessions found two modes were being treated as equivalent when they are not:

1. **Genuine autoresearch.** The loop calls the Claude API (or uses Claude Code tool use) to *propose* each strategy change, then evaluates, then loops. Confirmed on NBA, Tennis, EFL.
2. **Pre-scripted strategy search.** The "loop" file contained ~20 pre-written strategies and iterated through them against the L1–L5 harness. No Claude-in-loop. Confirmed on IPL (see [[t20-cricket-ipl]]) and horse racing.

Pre-scripted search is still useful — it benchmarks known families against a good harness. But it is **not AutoStrategy as designed** because the search space is bounded by what the human pre-wrote. Reporting "31 experiments" from a pre-scripted run overstates the amount of novel search performed.

**Rule adopted:** Every TASK.md for an AutoStrategy Claude Code session must explicitly require that the iteration loop call the Claude API (or Claude Code tool use) to propose each next strategy change. Pre-scripted runs are still permitted but must be labelled as "strategy-bench runs", not "autoresearch runs", when results are summarised.

Applies to all future domain work including [[t20-cricket-ipl]], [[horse-racing]], [[snooker]], and any new domain added.

## Links

- [[autoresearch]] — Karpathy's original pattern and Andy's adaptations
- [[compound-evaluation]] — Detailed L1–L5 framework
- [[results-diagnostic]] — Post-hoc analysis and validation gates
- [[walk-forward-validation]] — Rolling-fold evaluation for regime-dependent domains
- [[probability-calibration]] — Isotonic regression for value-betting strategies
- [[nba]] — Walk-forward validation discovery; genuine autoresearch mode
- [[crypto]] — Walk-forward validation discovery
- [[t20-cricket-ipl]] — Pre-scripted search caveat discovered here
- [[betting-portfolio]] — Applied across sports domains (NBA, Tennis, Snooker, etc.)
- [[mark-lite]] — Applied to lead-finding skill optimization (v3→v4 improvements)

## Sources

- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/AutoStrategy_SKILL_v3.md
