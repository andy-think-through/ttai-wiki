# Probability Calibration

> Isotonic regression for correcting systematic overconfidence in predicted probabilities. Critical for value-betting domains.
> Last updated: 2026-04-08

## The Problem: Overconfident Probabilities

Many machine-learning models produce probability predictions that are **systematically miscalibrated**:
- Model says: "This bet has 67% win probability"
- Reality: In 100 similar situations, it only wins 45% of the time
- Result: Phantom bets (bets the model thinks have positive expected value that don't)

For value-betting strategies, this is catastrophic. You're computing edge as:
```
Edge = Model_Probability - Odds_Implied_Probability
```

If your model probabilities are overconfident, all edges are inflated. You end up taking bets that look profitable but aren't.

## Discovery: EFL Championship (2025)

Andy discovered this during EFL Championship value-betting development:

**Before calibration**:
- Model predicted probability on validation set: average 0.67
- Actual win rate in validation set: 0.45
- Overconfidence: 22 percentage points

**Betting impact** (simulated on validation set):
- Total bets identified (edge > 1%): 345
- Bets that actually had positive edge (tested against holdout odds): 102
- False-positive rate: 70%
- ROI on identified bets: -2.0% (you'd lose money)

**After calibration** (isotonic regression):
- Model predictions now match actual frequencies across buckets
- Bets with calibrated edge > 1%: 102 (down from 345)
- ROI on calibrated bets: +6.9% (profitable)
- Key change: Only bets with true edge survive calibration; phantom bets are eliminated

## How It Works: Isotonic Regression

Isotonic regression is a simple but powerful calibration method. It maps raw model probabilities to actual frequencies.

### The Process (3 steps)

**Step 1: Fit on Training Data**
1. On your training set, collect all predictions and actual outcomes
2. For each prediction, record: (predicted_probability, actual_outcome)
3. Sort by predicted probability (ascending)
4. Isotonic regression fits a monotonically increasing function that maps predictions → actual frequencies
5. Output: A calibration curve (a lookup table or piecewise-linear function)

**Example (Tennis)**:
```
Raw prediction 0.51 → Actual frequency (trained on 200 samples) → 0.48 (slightly overconfident)
Raw prediction 0.60 → Actual frequency (trained on 185 samples) → 0.56
Raw prediction 0.75 → Actual frequency (trained on 150 samples) → 0.70 (overconfident)
Raw prediction 0.90 → Actual frequency (trained on 80 samples)  → 0.84 (very overconfident)
```

The isotonic regression learns this mapping and generalises to new predictions.

**Step 2: Freeze the Calibration Curve**
- Lock the isotonic regression function (do not retrain)
- The curve is now your calibration transformation
- Apply it to all holdout and out-of-sample predictions

**Step 3: Apply to New Predictions**
- For each new prediction: calibrated_prob = isotonic_function(raw_prob)
- Compute edges with calibrated probabilities: Edge = calibrated_prob - odds_implied_prob
- Only take bets where calibrated edge > threshold

### Why Isotonic Regression?

Isotonic regression is:
- **Monotonic**: Output always increases with input (doesn't reverse probability ordering)
- **Simple**: No hyperparameters to tune (unlike polynomial fitting or Platt scaling)
- **Non-parametric**: Doesn't assume any particular functional form
- **Empirically validated**: Works well in practice for probability calibration

Alternative methods (Platt scaling, histogram binning) are more parameterised; isotonic regression is the gold standard.

## When to Use Probability Calibration

### MANDATORY: Value-Betting Domains

If your strategy computes expected value as `Edge = Model_Prob - Odds_Prob`, you **must** calibrate.

**Domains**:
- Sports betting (tennis, football, NBA, horse racing, etc.)
- EFL Championship
- General betting/gambling where odds are available

Without calibration, your edge estimates are fiction. You'll take bets that look profitable but lose money.

### OPTIONAL: Ranking / Prediction Tasks

If you're computing accuracy, log-loss, or AUC, calibration may help but is not mandatory:
- **Accuracy**: Calibration doesn't change classification (just probability attached to it)
- **Log-loss**: Calibration improves directly (lower log-loss on holdout)
- **AUC**: Calibration doesn't change ranking order (only smooths probabilities)

Use calibration if:
- You're publishing probabilities to end users (they should match reality)
- You're using probabilities downstream (e.g., confidence thresholds)

### SKIP: Pure Signals (Buy/Sell Decisions)

If your strategy outputs binary signals (buy/sell, act/no-act), you don't need probabilities at all. Calibration is irrelevant.

**Example**: A trend-following bot that outputs "buy" or "sell" without probabilities needs no calibration.

## Implementation Details

### Training the Calibration Function

```python
from sklearn.isotonic import IsotonicRegression

# On training set
calibrator = IsotonicRegression(out_of_bounds='clip')
calibrator.fit(train_predictions, train_actuals)

# Freeze (pickle or save coefficients)
# Do not retrain on holdout or future data
```

**Critical**: Train on training set only. Do not use holdout data to fit the isotonic regressor (that would be overfitting the calibration itself).

### Applying to New Data

```python
# On holdout or future predictions
calibrated_probs = calibrator.predict(new_predictions)

# Compute edge with calibrated probabilities
edges = calibrated_probs - odds_implied_probs
take_bet = edges > threshold
```

### Verification: Calibration Check

After applying calibration, verify it worked:
1. Bucket the calibrated predictions into bins (0.1-0.2, 0.2-0.3, etc.)
2. For each bin, compute actual frequency of positive outcomes
3. Check that predicted probability ≈ actual frequency within each bin (within ±3 percentage points)

**Example verification**:
```
Predicted 0.55 ± 0.05: Actual frequency 0.54 ✓
Predicted 0.65 ± 0.05: Actual frequency 0.66 ✓
Predicted 0.75 ± 0.05: Actual frequency 0.73 ✓
All buckets pass: Calibration successful
```

If buckets don't match, calibration failed (possible causes: overfitting during calibration fit, or data distribution shift between training and holdout).

## Tennis ATP Application (Recent)

Integrated into tennis pipeline (v4.3+):

**Before**: Model predicted H2H head-to-head accuracy
- Raw model probability: avg 0.62 on holdout
- Actual frequency: 0.58 (underconfident, actually good)
- Edge estimates: Conservative but reliable

**Calibration fit**: Isotonic regression on training set
- Discovered slight underconfidence (model slightly too pessimistic)
- Mapping: 0.62 → 0.59

**After calibration**: Applied to all holdout value-bets
- Edge estimates now match actual observed frequencies
- Probability of bet winning: predicted 0.58 → actual 0.57 ✓
- ROI improved by +0.3% (small but consistent gain)

**Why modest improvement?** Because the model was already well-calibrated. Calibration usually has largest impact on models with severe overconfidence (like the EFL example, +6.9%).

## EFL Championship Discovery (Full Example)

Complete walk-through of the discovery and fix:

**Problem identification**:
1. Model predicts 67% for a bet
2. Over 100 similar bets, only 45 hit
3. Question: Why is there a 22pp gap?

**Root cause**: Training set had different outcome distribution than test set
- Training: High-accuracy games (good teams, neutral venues)
- Holdout: More competitive games (underdog venues)
- Model learned to be overconfident on the "easy" training examples
- Transferred overconfidence to harder holdout examples

**Solution**: Isotonic regression
- Fit on training set: maps 0.67 → 0.45 (the discovered mapping)
- Apply to holdout: all 67% predictions become 45% predictions
- Now: calibrated edge = 0.45 - 0.40 (odds) = 0.05 (5% edge, real)
- Old uncalibrated edge: 0.67 - 0.40 = 0.27 (phantom 27% edge, not real)

**Results**:
- Phantom bets eliminated: 345 → 102 (70% false-positive rate eliminated)
- ROI: -2.0% → +6.9% (swing of 8.9 percentage points)

## Implementation Checklist

- [ ] Collect training predictions and outcomes
- [ ] Fit isotonic regression on training set
- [ ] Freeze calibrator (do not retrain)
- [ ] Apply to all holdout predictions
- [ ] Apply to all out-of-sample predictions
- [ ] Verify calibration (bucket check)
- [ ] Compute edges with calibrated probabilities
- [ ] Re-evaluate strategy metrics on calibrated predictions
- [ ] For value-betting: simulate ROI before/after calibration
- [ ] Document calibration function (save coefficients or model pickle)
- [ ] Refit calibrator quarterly or if data distribution shifts
- [ ] Caution: Do not refit on holdout or live data (overfitting)

## When to Refit

Refit the isotonic regressor when:
- **Quarterly or annually**: Refresh calibration on newly accumulated data (if available)
- **After major model change**: If you significantly retrain the underlying model, refit calibration on new training set
- **If performance degrades**: If verified ROI on new bets drops unexpectedly, check calibration (may have shifted)

**Do not refit**:
- On holdout data (overfitting)
- On live betting results (contamination with selection bias)
- Every week (data not stationary enough for weekly calibration)

## Links

- [[autostrategy]] — Value-betting strategies use probability calibration
- [[compound-evaluation]] — L1–L5 evaluation of calibrated predictions
- [[tennis-atp]] — Current application
- [[efl-championship]] — Discovery and original application

## Sources

- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/AutoStrategy_SKILL_v3.md
- Andy Allen's EFL Championship value-betting development (2025)
