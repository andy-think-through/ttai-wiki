# Cowork Pipeline
> Daily betting operations orchestration and current implementation.
> Last updated: 2026-04-08

## Architecture
```
Cowork (orchestrator)
  ↓
Claude Code Sonnet (model runner)
  ↓
Computer Use / Min browser (Betfair UI interaction)
  ↓
Manual bet placement (Andy reviews → places bets)
```

## Daily Sequence
1. **Fetch results** — Get yesterday's match results and scores
2. **Update tracker** — Log results in betting tracker spreadsheet (.xlsx, openpyxl)
3. **Run models** — Claude Code Sonnet runs predictive models for each sport
4. **Fetch odds** — Query or screenshot Betfair for current market odds
5. **Generate briefing** — Cowork creates summary of high-edge opportunities
6. **Andy reviews** — Manual ~15 min review of briefing (decision gates)
7. **Place bets manually** — Andy confirms and places bets directly on Betfair

**Timing:** Most of this can run at 7–8am. The review step is manual and blocks bet placement until Andy reviews and approves.

## Sports Coverage

| Sport | Type | Volume | Status |
|-------|------|--------|--------|
| **NBA** | Full live + pregame | 10+ matches/week | Active |
| **Tennis ATP** | Full live + pregame | 2–5 matches/day | Active (calibration required) |
| **Snooker** | Live + event betting | 3–8 matches/week | Active |
| **Darts** | Note-only | PDC tournaments | Note tracking only, no live betting |
| **Crypto** | VPS monitoring | 24/7 | Telegram/Google Sheets updates |

## Known Issues & Workarounds

### Issue 1: Computer Use Timeout When User Not Present
**Problem:** Computer Use calls timeout after 30s if the user is not at the keyboard to approve browser access.

**Current Workaround:** Keep a logged-in Betfair browser session open; use screenshot-based odds fetching only when needed.

**Permanent Fix:** Migrate to Betfair API (requires obtaining API credentials and IP whitelisting). This eliminates all Computer Use dependency.

### Issue 2: Tennis Matchup Data Requires Manual JSON Input
**Problem:** Tennis matches are sourced from ATP website, but matchup data (seeding, head-to-head history) must be manually collated and fed to the model as JSON.

**Current Workaround:** Curate matchups manually each day from ATP site.

**Permanent Fix:** Build an ATP scraper or use a third-party tennis data API (ATP has limited public APIs; consider investing in a data provider license).

### Issue 3: Betfair Odds Lag During Live Betting
**Problem:** Screenshot-based odds are stale by 5–10s during live events; fast-moving markets can execute at worse odds than displayed.

**Workaround:** Accept odds slippage; manually adjust if screenshotted odds differ significantly from placement confirmation.

**Fix:** Betfair API provides real-time odds (faster than UI).

## Key Rules Enforced

- **80% injury veto** — If a key player is 80%+ likely to be injured, veto the bet (sports injuries have option value; rarely worth forcing a bet)
- **Away-team 20% rule** — Home teams have a ~4–5% win rate advantage; only bet away teams if the model edge exceeds 20% after odds
- **Never back predicted loser** — If the model predicts Team A will win, never bet against them (exploits low-probability events)
- **Tennis calibration** — Apply isotonic regression to raw tennis predictions (see [[probability-calibration]]) before comparing to odds
- **Flat £5 staking** — All bets are £5 fixed stake; no Kelly or proportional sizing
- **Grass court veto** (pending) — Grass has high randomness and negative ROI historically; consider disabling entirely
- **Manual bet placement always** — Andy must manually confirm each bet; no automated posting to Betfair

## Key Metrics Tracked

- **Win rate (%)** — % of bets that won
- **ROI (%)** — (Profit / Total Stake) × 100
- **Edge hold** — Did the model edge translate to actual edge in practice?
- **Pressure ratio** — Live vs pregame ROI (if live is much worse, odds fetching is stale)

## Dependencies

- **Betfair account** — logged in and accessible
- **Betting tracker** — .xlsx file with historical bets, results, ROI
- **Model artifacts** — pre-trained models for each sport in Claude Code environment
- **ATP/NBA/Snooker data sources** — live feeds or screenshottable sites
- **Cowork** — orchestrator skill that runs daily
- **Google Sheets** (optional) — for crypto monitoring via Telegram integration

## Maintenance

- **Daily:** Review briefing, place bets, update tracker with results
- **Weekly:** Audit ROI by sport, check for systematic issues (e.g., model drift)
- **Monthly:** Revalidate calibration; consider re-tuning edge thresholds
- **As-needed:** Add new sports, disable underperforming markets, patch data sources

## Sources
- raw/autostrategy/daily-skill-lessons-learned.md
- raw/autostrategy/autostrategy_STATUS.md
- raw/autostrategy/AutoStrategy_Paper_v6.md

## Links
- [[autostrategy]] — Strategy optimization framework
- [[betting-portfolio]] — Portfolio container
- [[scheduled-tasks-need-zero-intervention]] — Operational principle
- [[tool-routing]] — Tool selection guide
- [[known-failure-modes]] — Failure mode mitigation
- [[compound-evaluation]] — Evaluation framework (metrics tracked)
- [[probability-calibration]] — Applied to tennis predictions
- [[nba]], [[tennis-atp]], [[snooker]], [[darts]], [[crypto]] — Domains managed
