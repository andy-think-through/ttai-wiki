# T20 Cricket (IPL)

> Queued domain with excellent market structure. Toss-window edge thesis needs urgent testing -- IPL season running now. First AutoStrategy pass (14 Apr) ran as pre-scripted strategy search rather than genuine agent-in-the-loop; 47.9% OOS accuracy confirms IPL is hard to predict at match-winner level.
> Last updated: 2026-04-20

## Model
Not yet built. Thesis: toss creates a structural 5-10% shift in win probability (batting first vs chasing). If the pre-toss market hasn't fully adjusted within 2-3 minutes of the toss, there's a brief window of mispricing.

Data source: Cricsheet (open source ball-by-ball data).

## Status
Queued -- feasibility study in progress. First AutoStrategy pass complete (14 Apr) but needs redoing with a genuine autoresearch loop (see Decision Log).

## Market Structure (Fred Betfair exploration, 2026-04-13)

IPL has the best market structure of any sport Fred examined:

| Timeframe | Matched | Fav Spread | Dog Spread |
|---|---|---|---|
| Next day | £67,792 | 0.5% | 0.9% |
| 2 days out | £2,391 | 2.7% | 3.8% |
| 3 days out | £91 | 8.6% | 13.9% |
| 4 days out | £26 | 9.9% | 10.9% |

**Key finding:** Next-day IPL spreads (0.5% fav, 0.9% dog) are tighter than ANY other sport Fred examined, including NBA. But liquidity drops off a cliff beyond 1 day out. Any IPL betting must be same-day or day-before.

Pakistan Super League also showed decent liquidity: £33K matched for next-day match.

## Edge Thesis: Toss-Window Mispricing

The toss in T20 cricket happens ~30 minutes before the match starts and determines which team bats first vs chases. Batting first vs chasing is worth an estimated 5-10% in win probability depending on conditions (pitch, weather, venue).

**Hypothesis:** If the pre-toss market hasn't fully adjusted within 2-3 minutes of the toss result, there's a brief window where a bettor who sees the toss can back the advantaged side before the market catches up.

**Why it might work:** The market is very efficient pre-toss (0.5% spreads = lots of sharp money). But the toss is a discrete information event that shifts probabilities by 5-10%. If automated repricing takes even 60-120 seconds to propagate, there's a window.

**Why it might not work:** The market may reprice instantly (algorithmic traders). Or the toss effect may already be priced into the pre-toss market as an average expectation.

## Feasibility Test (Urgent -- IPL Running Now)

Monitor 5 IPL matches at toss time (~14:30 UK). Record:
1. Odds 1 minute before toss
2. Odds at moment of toss announcement
3. Odds at 1, 2, 5 minutes after toss
4. Final pre-match odds (at match start)

If the market takes >2 minutes to fully adjust (>2% of the toss effect still unpriced), the edge exists and is worth building a model around.

## Active Rules
- None at this time (domain not yet active)

## Findings from First AutoStrategy Pass (2026-04-14)

An AutoStrategy run was executed in Claude Code against Cricsheet ball-by-ball data to try to predict match winners. Headline results:
- **47.9% OOS accuracy** — below coin-flip on a binary outcome
- **Massive compound-score lift vs baseline (+62%)**, driven mostly by L4 coherence
- Model families evaluated: raw win rates, Elo, Bayesian Beta(α,β), venue-weighted form, H2H, various ensembles

### Transferable findings (robust)
- **Bayesian Beta beats raw win rates for sparse-data / new-team cases.** Beta(α,β) priors absorb small-sample noise cleanly — cheap to implement, wide transfer to other low-sample sports (new football season, first-round darts, early-season NBA). Feeds into the [[autostrategy]] toolkit for any sparse-prior problem.
- **H2H record hurts in IPL.** Team compositions change too much year-to-year; H2H memory is noise, not signal. A reminder that "classic" features can be outright harmful in fast-rotating squads.
- **Three-way ensemble (Bayesian prior + Elo + venue-weighted form) edges any single component,** because each captures orthogonal signal.
- **Toss × venue interaction contributes 3–6% probability shift** when the toss-winner makes the optimal decision for that venue — consistent with the [[toss-window]] edge thesis below.

### Methodological caveat (to fix next pass)
An audit after the run (see [[autostrategy]]) found that the IPL "autoresearch" was closer to a **pre-scripted strategy search** than genuine autoresearch — ~20 strategies were pre-written and tested against the 5-level harness, rather than Claude-in-the-loop proposing each next strategy. The 47.9% OOS is still honest and the transferable findings above hold, but the "31 experiments" headline overstates how much search was actually performed. For future AutoStrategy runs, TASK.md must explicitly require Claude API / tool use to propose each strategy change.

## Decision Log
- 2026-04-14: First AutoStrategy pass completed. 47.9% OOS accuracy on match-winner prediction confirms T20 is genuinely hard to predict at binary level. Bayesian Beta + three-way ensemble findings promoted to [[autostrategy]] as transferable. Audit identified the loop itself was pre-scripted — adopt Claude-in-loop requirement for next pass.
- 2026-04-13: IPL market structure confirmed as excellent (£68K, 0.5% spreads). Toss-window feasibility test designed. Urgent -- IPL season is live.

## Links
- [[autostrategy]] -- Strategy optimization methodology
- [[betting-portfolio]] -- Portfolio container
- [[execution-cost-varies-by-selection]] -- IPL has the tightest spreads of any sport examined
- [[selectivity-is-everything]] -- Even with good market structure, only bet where there's genuine edge
- [[market-efficiency-varies-within-domain]] -- Efficient pre-toss market may become inefficient for 2-3 minutes post-toss

## Sources
- Fred Betfair exploration report (2026-04-13)
- Cricsheet (planned data source for model building)
