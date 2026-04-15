# Results Diagnostic

> Post-hoc analysis of live or backtest results to identify actionable insights, validate that improvements are real, and generate hypotheses for the next iteration.
> Last updated: 2026-04-08

## Overview

AutoStrategy's inner loop (evaluation and iteration) optimises on a fixed set of metrics (L1–L5). But metrics can be gamed, and real-world performance often reveals insights that metrics miss. Results Diagnostic is the feedback bridge: it takes the raw outcomes from live execution or backtests and extracts actionable findings that inform the next round of strategy refinement.

The process is systematic enough to automate (fast loop, fortnightly on live results) but thorough enough to catch subtle issues (slow loop, walk-forward on historical data).

## Six-Step Diagnostic Process

### Step 1: Split and Profile

**What**: Divide results by key dimensions and compute aggregate metrics for each.

**How**:
- By outcome (win/loss, profit/loss, conversion/no-conversion)
- By input features (player rank, market volatility, prospect company size)
- By time period (week-over-week, month-over-month)
- By confidence (high-confidence predictions vs low-confidence)

**What to look for**:
- Unexpected patterns (e.g., high confidence + low accuracy, or accuracy degrades with specific feature value)
- Rare categories that don't have enough data to draw conclusions (sample size <30)
- Temporal degradation (week 1 vs week 4 accuracy drift)

**Example (Tennis)**:
- Split by player rank: top-50 accuracy 81%, rank 50-100 accuracy 64%
- Insight: Strategy overconfident on lower-ranked players (may be fitting to historical seed strength rather than current form)

### Step 2: Enrichment

**What**: Add context to each prediction that metrics don't capture.

**How**:
- Gather relevant external data (market moves, weather, competing actions)
- Flag predictions that were "close" (edge = 0.5% vs edge = 5%)
- Mark predictions that were against base rate (betting on heavy underdogs)
- Tag predictions with domain labels (e.g., "fast court", "clay court" in tennis; "high-growth startup", "established SME" in sales)

**What to look for**:
- Categories where the strategy systematically underperforms (e.g., all "clay court" predictions lose)
- Predictions that were close calls (within confidence margin) that shouldn't guide strategy changes
- Base-rate violators (strategy went against majority, need to verify it was correct reasoning, not just lucky)

### Step 3: Feature Comparison

**What**: For wins vs losses (or high-confidence correct vs incorrect), compare feature distributions.

**How**:
- Compute mean feature values for wins and losses separately
- Highlight features that differ substantially between the two groups
- Use statistical tests (t-test, chi-squared) to assess significance (not just difference, but confidence in the difference)

**What to look for**:
- Features that are much more common in wins (candidate for increased weight or new rule)
- Features that are equally common in wins and losses (candidate for removal, as it's not driving outcomes)
- Features where the direction of influence flipped (e.g., "higher rank" = more wins, but you coded it in reverse)

**Example (Tennis)**:
- Wins: avg. H2H % = 52%, avg. serve speed = 118 mph, avg. rank = 42
- Losses: avg. H2H % = 48%, avg. serve speed = 115 mph, avg. rank = 67
- Feature comparison: H2H % and rank differ substantially. Serve speed barely differs (feature added no signal).
- Action: Weight H2H and rank higher; drop serve speed.

### Step 4: Loss Autopsy

**What**: For each loss (or significant error), ask why.

**How**:
- Categorise losses into types:
  - *Skill deficiency*: The strategy didn't have the right information or logic (feature or rule missing)
  - *Input surprise*: The feature values were within normal range, but outcome was extreme (model didn't handle this regime)
  - *Random noise*: Outcome was within base-rate variance (don't over-fit to single losses)
  - *External shock*: Something changed in the world that no historical data captured (new competitor, market halt, etc.)
- For skill deficiency losses, dig into feature values at prediction time. What signal did you miss?
- For input surprise, check if L3 (synthetic edge cases) would have caught this

**What to look for**:
- Systematic loss categories (e.g., all losses in category A suggest missing feature for category A)
- Surprise losses that seem random (may indicate non-stationarity; see [[walk-forward-validation]])
- External shocks that require strategy rewrite, not iteration

**Example (Tennis)**:
- Loss: Model predicted Nadal over Djokovic on clay (H2H: 55%, rank: similar). Djokovic won in straight sets.
- Root cause: Model didn't account for recent shoulder injury affecting Nadal's serve (new information that wasn't in historical H2H).
- Action: Add injury flag as feature (or rely on external data feed).

### Step 5: Win Validation

**What**: For wins, verify you were right for the right reasons.

**How**:
- For high-edge predictions (>3% expected value): check feature values. Do they align with stated strategy logic?
- For low-edge predictions (0.5-1.5% expected value): relax scrutiny (edge could be noise). But if many low-edge wins cluster in a feature subgroup, investigate.
- Compute feature influence (SHAP or ablation) on the predictions. Did the model actually use the stated features?

**What to look for**:
- Wins driven by features the strategy doesn't mention (sign of drift from stated logic, may not generalise)
- Wins where all stated features were null/missing (strategy succeeded by accident)
- Wins with very low edge (noise; don't design strategy around these)

**Example (EFL Championship, from [[efl-championship]])**:
- Win: Predicted home team victory in League Two with edge 1.2%. Team won, margin +0.5 pts (soft metric).
- Feature check: Model used "strength of schedule" (stated feature) + "recent form" (stated feature).
- But model also overweighted "home crowd effect", which isn't in stated logic.
- Action: Rewrite logic to explicitly include home crowd; reduce overweight on strength of schedule.

### Step 6: Hypothesis Generation

**What**: Synthesise findings from steps 1-5 into 3-5 concrete hypotheses for the next iteration.

**How**:
- Candidate 1 (high confidence): "Feature X is underweighted. Increasing X's coefficient by +0.2 should improve accuracy by ~1-2%."
- Candidate 2 (medium confidence): "Category Y (e.g., clay courts) requires separate logic. Test branch-by-category."
- Candidate 3 (low confidence, exploration): "Could loss autopsy Category A be solved by adding feature Z (not currently available)? If so, invest in data engineering."

**What to look for**:
- Hypotheses grounded in data (not hunches)
- Mix of high-confidence tweaks (for exploitation) and exploratory directions (for 25% exploration budget)
- Prioritised by impact (which hypothesis, if correct, has biggest payoff?)

## Two-Speed Architecture

Results Diagnostic runs at two different cadences:

### Fast Loop (Fortnightly on Live Results)

**Cadence**: Every 2 weeks (or 1 week if fast domain like daily betting)

**Scope**: 
- Recent wins/losses (last 500 predictions or 2 weeks of live data)
- Focus on quick fixes: rule tweaks, threshold adjustments, feature reweighting
- Step 4 (loss autopsy) is manual or LLM-assisted

**Output**: 1-2 high-confidence hypotheses fed into exploitation round

**Example**: Every 2 weeks, review the last 500 tennis predictions. Are we systematically losing on clay courts? Adjust clay-court logic.

### Slow Loop (Walk-Forward on Historical Data)

**Cadence**: Monthly or quarterly

**Scope**:
- Entire historical dataset (all 2000+ predictions, multiple years)
- Use walk-forward validation splits (see [[walk-forward-validation]]) to avoid overfitting the diagnostic
- Comprehensive feature analysis (steps 1-6 in full depth)
- Step 4 (loss autopsy) can be thorough, even manual review of ~50 worst losses

**Output**: 3-5 medium- to low-confidence hypotheses. Some feed exploration budget; others feed data engineering roadmap

**Example**: Every quarter, review the past 3 years of tennis data across 10 walk-forward folds. Identify persistent patterns. "Serve-speed feature never improved accuracy across any fold → remove it."

## Three-Gate Validation (Before Incorporating Results)

Not every finding from results diagnostic should immediately influence strategy. Before incorporating a finding, pass it through three gates:

### Gate 1: Persistence

**Question**: Does this finding hold in multiple time periods / cross-validation folds?

**Check**:
- Fast loop finding: Confirm it appears in both recent data and historical walk-forward folds
- Slow loop finding: Confirm it appears in majority of walk-forward folds (5/7 minimum)
- One-off finding with n<30: Insufficient evidence, label as "watch" not "incorporate"

**Example (Tennis)**: "Clay-court losses" is real only if it appears in every walk-forward fold. If it's only in fold 3, it might be random.

### Gate 2: Historical Validation

**Question**: Could this finding have been obvious from historical data? If so, why didn't earlier versions of the strategy catch it?

**Check**:
- If finding is obvious in history, strategy should have adapted already (something is broken)
- If finding is new (e.g., "recent form matters more than H2H since 2024"), mark as regime change
- If finding is hidden (e.g., "clay court effect only visible in last 50 matches"), mark as emerging (monitor)

**Example (Tennis)**: "Serve speed is useless" should be obvious from 5 years of data. If strategy still weighs it heavily, gate fails. Revert strategy to version before serve speed was added.

### Gate 3: Causal Mechanism

**Question**: Do you understand WHY this finding is true? Can you describe the causal mechanism?

**Check**:
- Hypothesis: "Serve speed is useless because match outcomes depend on rallies, not serves" — plausible mechanism
- Counter-example: "Home crowd matters more on Tuesdays" — no plausible mechanism (likely noise)
- Mechanism doesn't require deep domain expertise, but it should be testable or logical

**Example (EFL Championship)**: "Home crowd effect strongest in smaller stadiums" has a mechanism (fewer away fans can travel, less opposing noise). This passes gate 3. "Home crowd effect strongest on Tuesdays" has no clear mechanism; likely noise.

**Decision Rule**: Only incorporate findings that pass all three gates. Findings that fail any gate are either watched (if promising) or discarded.

## Implementation Checklist

- [ ] Define result types for your domain (win/loss, profit/loss, etc.)
- [ ] Automate split and profile (step 1)
- [ ] Set up enrichment pipeline (step 2): add context features, external data
- [ ] Implement feature comparison (step 3): t-tests, chi-squared where applicable
- [ ] Manual loss autopsy process (step 4) or LLM-assisted categorisation
- [ ] Win validation checklist (step 5)
- [ ] Hypothesis generation template (step 6)
- [ ] Fast loop trigger (fortnightly or weekly)
- [ ] Slow loop trigger (monthly or quarterly)
- [ ] Three-gate validation process before incorporating findings
- [ ] Logging: record each finding, which gate it passed, decision to incorporate/watch/discard

## Known Findings (Examples)

**Confirmed findings across domains** (these passed three-gate validation and are now integrated into strategy):

1. **NBA**: "Streak-dampening rule removes weak signal." Removing artificial streak-dampening from older versions improved holdout by +0.7% and validation by +0.8% (see [[nba]])

2. **Tennis**: "Majority-class trap on H2H." Model overweighted historical H2H and underweighted recent form on underdogs. Fixed in v4.2.

3. **EFL Championship**: "Home-court effect nonlinear with stadium capacity." Separate logic for stadiums <10K and >10K improved edge by +0.3%.

## Links

- [[autostrategy]] — Framework that feeds results diagnostic into iteration loop
- [[compound-evaluation]] — Metrics that results diagnostic interprets
- [[walk-forward-validation]] — How to apply diagnostic across multiple time periods
- [[nba]], [[tennis-atp]], [[efl-championship]], [[crypto]] — Domains where diagnostic found confirmed findings

## Sources

- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/AutoStrategy_SKILL_v3.md
