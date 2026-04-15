# Autoresearch

> Karpathy's open-sourced parameter-tuning pattern applied to strategy optimisation. Read, hypothesise, modify, evaluate, keep/revert, repeat.
> Last updated: 2026-04-08

## Karpathy's Original Pattern

In early March 2026, Andrej Karpathy open-sourced a 630-line Python script that implements a general pattern for automated optimisation of any system describable as:
- A mutable file (parameters, configuration, or code)
- An evaluation metric
- A test loop

The repository reached 32,000+ GitHub stars within weeks, validating that this pattern addresses a common need: how do you iterate when manual tuning is too slow and the problem space is too large for grid search?

### The Core Loop

1. **Read**: Load the mutable file (current best configuration)
2. **Hypothesise**: Generate a change (educated guess or random perturbation)
3. **Modify**: Apply the change to the mutable file
4. **Evaluate**: Run the system, compute the metric
5. **Keep/Revert**: If metric improved, keep; otherwise revert
6. **Repeat**: Go to step 1

The loop is deterministic, auditable, and can run unattended. Each iteration produces a git-like diff showing exactly what changed.

### Architecture

Three required components:
1. **Mutable file**: Plain text (JSON, YAML, Python, or prose) that the system reads
2. **Program file**: Stateless code that reads the mutable file and produces output
3. **Eval metric**: A single number (higher or lower is better; must be consistent)

The mutable file and program are completely decoupled. Change the strategy, re-run the program, get a new metric. This decoupling is critical: it means you can iterate on the strategy without touching the evaluation logic.

## Andy's First Application: Mark-Lite v3→v4

In March 2026, Andy applied autoresearch to optimise Mark-Lite's outreach skills:

**Lead-Finding Skill**
- v3 baseline: 6.6/10 (evaluated on lead quality and relevance)
- v4 with autoresearch: 10.0/10
- Key change: Reordered decision logic to prioritise size + trade match before geography

**Outreach Skill**
- v3 baseline: 9.0/10
- v4 with autoresearch: 10.0/10
- Key change: Refined email template selection logic and timings

Both skills converged in 3–4 weeks of nightly iteration cycles (5–10 changes per skill per week). The improvements were modest in scope (rewording, reordering, tweaking thresholds) but cumulative.

## Two Key Constraints

### 1. Speed (Tight Feedback Loop Required)

Autoresearch only works if each iteration is fast enough to run nightly or more frequently.
- If evaluation takes 2 weeks, you can only do ~26 iterations per year: too slow to converge
- If evaluation takes 30 minutes, you can do 40+ iterations per night: enough to explore
- Implication: You need a fast proxy metric, not the ground-truth metric

Example (Mark-Lite):
- Ground truth: "How many leads actually convert?" (requires weeks to month)
- Fast proxy: "How well does this match our quality rubric?" (minutes)
- Autoresearch optimises the proxy; verify convergence on ground truth later

### 2. Depth (Constrained Structural Optimisation)

Autoresearch optimises within a fixed structure. It can't redesign the program from scratch.
- Example: Mark's outreach is built on "identify lead → check for contact → draft email → send"
- Autoresearch can optimise each step (better filtering, better templates)
- But autoresearch alone won't discover "actually, we should call instead of email" (structural redesign)

This is where AutoStrategy extends autoresearch: by making the strategy itself mutable (including structural choices), you can explore broader design spaces.

## Connection to AutoStrategy

AutoStrategy treats autoresearch as the inner loop and adds:
1. **Multi-level evaluation** (L1–L5) instead of a single metric, catching more failure modes
2. **Exploration mode** (25% budget) to escape local optima and explore structural changes
3. **Compound score** that balances accuracy, generalisation, edge cases, and interpretability
4. **Data path handling** (clean, action-entangled, no data) with appropriate calibration

In other words: autoresearch is the engine; AutoStrategy is the transmission and navigation system.

## Practical Lessons

- **Start with a clear metric**: If you can't define what "better" means in 5 seconds, autoresearch will fail
- **Instrument heavily**: You need logs, diagnostics, and post-hoc analysis to understand what changed and why
- **Manual spot-checks**: Run the system manually after every 10 iterations to catch subtle breakages (the metric might not catch them)
- **Version everything**: Every mutable file version should be tagged with date, metric value, and key change summary
- **Hybrid human-AI**: The hypothesise step can be done by LLM (e.g., Claude suggesting next tweak based on recent results), but humans should review every few iterations

## Implementation Checklist

- [ ] Mutable file written (strategy, parameters, or configuration)
- [ ] Program file decoupled from mutable file
- [ ] Eval metric defined (fast enough for nightly runs)
- [ ] Test loop automated
- [ ] Keep/revert logic implemented
- [ ] Logging/diagnostics in place
- [ ] Manual spot-checks scheduled (e.g., weekly)
- [ ] Version tagging system set up
- [ ] LLM-assisted hypothesis generation (optional, but useful)

## Links

- [[autostrategy]] — AutoStrategy extends autoresearch to strategy design
- [[compound-evaluation]] — Multi-level metrics for richer feedback
- [[results-diagnostic]] — Post-hoc analysis to understand what changed
- [[agent-browser]] — Parameter optimization for workflow refinement
- [[mark-lite]] — Applied to lead-finding and outreach skill optimization

## Sources

- Karpathy's autoresearch GitHub repository (open-sourced March 2026)
- raw/autostrategy/AutoStrategy_Paper_v6.md
- raw/autostrategy/AutoStrategy_SKILL_v3.md
