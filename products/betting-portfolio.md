# Betting Portfolio

> AutoStrategy value betting across sports. Current P&L: +£49.86 total (+£38.90 NBA, +£7.96 tennis, +£3.00 snooker). Mix of live, paper, and parked positions. Income stream diversification outside Mark/Hike/Consulting.
> Last updated: 2026-04-10

## Portfolio Overview

Andy runs **AutoStrategy**, a systematic value betting approach across multiple sports domains. This is a side income stream (not a core business focus like Mark or Hike SEO) but generates positive ROI and provides operational learning.

### Current Composition

| Domain | Status | P&L | Notes |
|---|---|---|---|
| [[NBA]] | Live | +£38.90 | Primary domain; most developed methodology |
| [[Tennis]] | Live | +£7.96 | Secondary domain; Monte Carlo clay swing active |
| [[Snooker]] | Live | +£3.00 | Tertiary domain; smallest volume |
| Darts | Paper | N/A | Methodology developed; not actively betting |
| Horse Racing | Parked | N/A | Research phase; awaiting market conditions |
| Crypto | **Parked indefinitely** | -16.8% | Multi-pair stop-loss exits below backtest. VPS deleted 29 Apr. |

**Total Portfolio P&L: +£49.86** (actual cash, not theoretical). Previously +£47.43 as of Apr 8. Betfair balance: £31.53 (as of Apr 6).

## Methodology

### Core Principle: Value Betting

- Identify **discrepancies** between market-implied probability and true probability
- Bet only on **positive expected value** outcomes (where odds > calculated true odds)
- Repeat at scale across sports and seasons
- Rely on systematic rules, not emotion or prediction

### Risk Management

- **Unit stakes:** Consistent per-bet sizing (typically 1-2% of bankroll)
- **Kelly criterion:** Adjust stake based on confidence and edge size
- **Bet limits:** Max exposure per match, per round, per day
- **Loss controls:** Cut underperforming strategies quickly

### Seasonal Patterns

- **NBA (Oct-Jun):** Regular season + playoffs; high volume; tight market efficiency = smaller edges
- **Tennis (Year-round):** Grand Slams (4), Masters (9), smaller tournaments; variable liquidity
- **Snooker (Sep-May):** Main season; World Championship (Apr) highest volume
- **Darts (Oct-Jun):** PDC season; high volume in World Championship (Dec-Jan)
- **Horse Racing:** Flat (Mar-Nov), Jump (Aug-Apr); two distinct seasons
- **Crypto:** 24/7 market; thesis-driven rather than seasonal

## Domain Detail

### NBA ([[NBA]])

**Status:** Live, +£38.90

- **Edge Source:** Player prop markets (o/u points, assists, rebounds); line movement arbitrage
- **Data:** Real-time stats + player news + injury reports + Vegas lines
- **Rules:** [[Active Rules]], [[Never Back Predicted Loser]], [[Away Team Threshold]], [[Grass Veto]] (not applicable to indoor), etc.
- **Volume:** ~20-40 bets per season
- **Typical Bet:** +120 to -110 lines; ROI ~55-60% if edge identified correctly

### Tennis ([[Tennis]])

**Status:** Live, +£5.53

- **Edge Source:** Serve dominance + surface preference + grass court specialist lines
- **Tournaments:** Grand Slams + Masters + smaller events; liquidity varies widely
- **Rules:** Applied similar [[Active Rules]] framework; less developed than NBA
- **Volume:** ~5-10 bets per season (lower opportunity density)
- **Typical Bet:** Grass court specialists overpriced on clay; win %s moving against true probability

### Snooker ([[Snooker]])

**Status:** Live, +£3.00

- **Edge Source:** Frame score accumulator bets; world championship playoff structure exploits
- **Tournaments:** World Championship (April) highest volume; smaller events year-round
- **Rules:** Early methodology; still refining
- **Volume:** ~3-5 bets per season (emerging domain)
- **Typical Bet:** Underpriced match odds due to low market efficiency in non-major events

### Darts ([[Darts]])

**Status:** Paper (not actively betting)

- **Edge Source:** PDC World Championship structure; inconsistent player form; home advantage
- **Methodology:** Developed but not live
- **Why Parked:** Market is efficient during main season; edges smaller than expected. Waiting for off-season patterns or tournament restructures.

### Horse Racing ([[Horse Racing]])

**Status:** Parked (research phase)

- **Edge Source:** Form analysis + going conditions + jockey-trainer partnerships
- **Data Needs:** Extensive historical data (5+ seasons per horse + jockey combos)
- **Why Parked:** Requires bespoke research infra; not yet built. Viable but lower priority than sports with larger edge opportunities.

### Crypto ([[Crypto]])

**Status:** Parked indefinitely (2026-04-29)

- **Edge Source:** Market inefficiency in alts; technical analysis + fundamental disparities
- **Result:** -16.8% multi-pair paper trading. Stop-loss exits systematically below backtest.
- **Why Parked:** Paper trading disproved the backtest edge. VPS (DigitalOcean 159.65.18.20) deleted 29 Apr. Logs saved.
- **Principle validated:** [[phantom-value]] -- apparent edge was structural illusion, not real mispricing

## Portfolio Management

### Performance Tracking

All bets logged in spreadsheet with:
- Date, sport, market, bet type (match, prop, accumulator)
- Odds, stake, expected value (calculated vs. actual)
- Result (W/L/Void), actual odds at push time
- Comments (why was this bet positioned? what learned?)

### Seasonality & Rebalancing

- **Q4 (Oct-Dec):** NBA ramping + Darts + Tennis season starts → high volume
- **Q1 (Jan-Mar):** NBA mid-season + Tennis + Horse racing (flat)
- **Q2 (Apr-Jun):** NBA playoffs + Tennis Grand Slams + Snooker Worlds → peak volume
- **Q3 (Jul-Sep):** Low volume (off-season); data analysis, rule refinement, archival

### Capital Deployment

- Starting bankroll: [Amount not disclosed in context]
- Current portfolio P&L: +£47.43 (reinvested)
- Allocation: NBA 75% → Tennis 15% → Snooker 10%
- New domains (Darts, Horse, Crypto) will receive incremental allocation once live

## Betting Rules & Methodology

### Active Rules

- [[Active Rules]] — Core systematic rules applied across domains
- [[Never Back Predicted Loser]] — Avoid betting on teams/players market prices as likely losers
- [[Away Team Threshold]] — Away teams require additional edge due to home advantage cost
- [[Grass Veto]] — Don't bet on clay court specialists playing grass

### Rule Evolution

Rules are data-driven:
1. Hypothesis (e.g., "Away team bias + travel fatigue = +3 point spread")
2. Backtest against 2+ seasons of data
3. Live test with small stakes
4. Refine or discard based on ROI

## Income Stream Role

This is **not** a primary business; it serves three purposes:

1. **Diversification** — If Mark or Hike SEO experience downturns, betting provides buffer income
2. **Operational Learning** — Systematic process + data analysis + rules refinement → transferable to Mark/Hike
3. **Tax Efficiency** — Gambling losses offset business income (UK tax law)

### Time Investment

- **Live season:** 5-10 hours/week (data review, line shopping, bet placement)
- **Off-season:** 2-5 hours/week (data analysis, rule refinement, backtest new strategies)

Not a full-time focus; Mark and Hike SEO are priorities.

## Risk Acknowledgments

- **Market risk:** Lines move against bets; unexpected injuries/news shifts odds
- **Model risk:** Historical patterns may not predict future; market efficiency improves over time
- **Behavioral risk:** Emotional decision-making can override systematic rules (mitigated by strict rules + logs)
- **Liquidity risk:** Smaller markets (snooker, niche props) may have limited volume; bets size constrained

## Future Expansion Candidates

- **Formula 1:** Constructor/driver odds; pre-season vs. actual season performance
- **MMA/UFC:** Underpriced underdog props; fighter form cycles
- **Rugby (Union + League):** Weather effects on odds; team cohesion vs. bookmaker models
- **Esports:** Emerging market with information asymmetry vs. mainstream sports

Each requires 6-12 months of research + backtest before going live.

## Links

- [[NBA]] — Primary domain detail
- [[tennis-atp]] — Secondary domain detail
- [[snooker]] — Tertiary domain detail
- [[darts]] — Parked domain (paper bets)
- [[horse-racing]] — Parked domain (research)
- [[crypto]] — Parked domain (awaiting strategy)
- [[active-rules]] — Core systematic rules
- [[never-back-predicted-loser]] — Specific rule detail
- [[away-team-threshold]] — Specific rule detail
- [[grass-veto]] — Specific rule detail
- [[autostrategy]] — Strategy optimization methodology
- [[compound-evaluation]] — Multi-level evaluation framework
- [[walk-forward-validation]] — Rolling-fold testing for regime robustness

## Sources

- Andy's private betting logs (not in repo; referenced for context)
- Historical test data stored in private analysis sheets
- /sessions/brave-vigilant-gauss/mnt/Projects--Think Through AI/raw/mark/FULL_PROJECT_CONTEXT.md (mentions P&L figures)
