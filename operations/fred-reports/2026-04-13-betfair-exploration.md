# Fred -- Betfair Exploration Report

**Date:** Sunday 12 April 2026, 23:08-23:16 UK time
**Duration:** ~25 minutes active browsing
**Session type:** One-time exploration (20% time)
**Account status:** Logged in (Main: £14.02, Exchange Bonus: £0.00)

---

## What I Explored

1. NBA pre-match markets (tonight's 7-game slate + tomorrow's 9-game slate)
2. NBA in-play market (Hawks @ Heat, Q1 observation)
3. Tennis pre-match (ATP Barcelona 2026, ATP Munich 2026)
4. Tennis in-play (Mexico City Challenger, Wuning/Busan Challengers)
5. Snooker World Championship outright winner market
6. Snooker World Championship Qualifiers (10 in-play matches)
7. Darts -- Premier League (TV event, Apr 16) and MODUS Super Series (floor event, Mon)
8. Cricket -- Indian Premier League, Pakistan Super League, International T20
9. Football in-play (Brazilian Serie A, Argentinian Primera, Jamaican Premier League)
10. Cross-sport liquidity comparison at 23:00-23:15 UK on a Sunday night

---

## Observations

### 1. NBA Markets -- Pre-Match (Sun 12 Apr, 23:08 UK)

Tonight's 7-game slate, all "Starting soon" (US evening tip-off):

| Match | Matched | Back/Lay Fav | Spread (Fav) | Back/Lay Dog | Spread (Dog) |
|---|---|---|---|---|---|
| Hawks @ Heat | £191,813 | 1.27/1.28 | 0.8% | 4.6/4.8 | 4.3% |
| Hornets @ Knicks | £25,882 | 1.13/1.15 | 1.8% | 7.8/8.2 | 5.1% |
| Pistons @ Pacers | £24,318 | 1.09/1.10 | 0.9% | 11/11.5 | 4.5% |
| Bucks @ 76ers | £31,424 | 1.08/1.09 | 0.9% | 12/13 | 8.3% |
| Magic @ Celtics | £52,267 | 1.16/1.17 | 0.9% | 7/7.2 | 2.9% |
| Wizards @ Cavs | £15,083 | 1.23/1.24 | 0.8% | 5.2/5.3 | 1.9% |
| Nets @ Raptors | £49,663 | 1.02/1.03 | 1.0% | 34/55 | 61.8% |

Monday's slate (01:40 UK) already had significant pre-match liquidity:

| Match | Matched | Notes |
|---|---|---|
| GSW @ Clippers | £91,441 | Star power effect -- highest liquidity for a game 26+ hours away |
| Denver @ Spurs | £19,059 | Decent |
| Memphis @ Rockets | £13,367 | -- |
| Sacramento @ Blazers | £12,258 | Kings at 15/15.5 -- end-of-season dynamics |
| Pelicans @ Wolves | £9,891 | -- |
| Jazz @ Lakers | £8,989 | Jazz at 8/8.8 (10% spread on underdog) |
| Suns @ Thunder | £8,254 | -- |
| Bulls @ Mavericks | £3,417 | Lowest liquidity -- least compelling matchup? |

**Key finding:** NBA favourite-side spreads are extremely tight (0.8-1.8%) making efficient execution easy on favourites. Underdog spreads widen significantly (1.9-8.3% for normal games, 62% for extreme mismatches). This has implications for Fred's away-underdog threshold rule -- not only do underdogs need higher edge to justify betting, but the execution cost (spread) is also higher.

### 2. NBA In-Play (Hawks @ Heat, Q1)

Observed the market from Q1 10:56 (score 2-2) to Q1 10:15 (score 4-6 Heat):

| Timepoint | Hawks Back/Lay | Spread | Heat Back/Lay | Spread |
|---|---|---|---|---|
| Pre-match | 4.6/4.8 | 4.3% | 1.27/1.28 | 0.8% |
| Q1 10:56 (2-2) | 4.8/5.3 | 10.4% | 1.23/1.27 | 3.3% |
| Q1 10:15 (4-6) | 4.8/5.4 | 12.5% | 1.23/1.27 | 3.3% |

**Key findings:**
- In-play spreads widen dramatically: Hawks went from 4.3% pre-match to 10-12% in-play
- Favourite side widens less (0.8% to 3.3%) than underdog side (4.3% to 12.5%)
- Small Q1 scoring runs (4-point swing) barely moved moneyline odds
- But the handicap line jumped from +10.5 to +12.5 -- secondary markets are more reactive to in-game events
- Total Points market had very wide spreads in-play (16-17%) with only £4,621 matched
- Handicap market had £46,521 matched -- decent secondary market liquidity

**Structural observation:** In-play NBA betting on underdogs is expensive due to wide spreads. Pre-match execution is significantly cheaper. This argues against any in-play betting strategy for Fred, especially on underdogs.

### 3. Tennis Pre-Match (ATP Barcelona 2026)

Observed at 23:08 UK for Monday's matches:

| Match | Matched | Fav Spread | Dog Spread |
|---|---|---|---|
| Etcheverry vs Draper | £2,052 | 1.79/1.83 = 2.2% | 2.2/2.26 = 2.7% |
| Borges vs Mannarino | £1,481 | 1.27/1.28 = 0.8% | 4.5/4.8 = 6.7% |
| Munar vs Jodar | £5,746 | 1.47/1.48 = 0.7% | 3.05/3.1 = 1.6% |
| Landaluce vs Musetti | £1,725 | 1.29/1.33 = 3.1% | 4.0/4.5 = 12.5% |
| Opelka vs Quinn | £826 | 1.56/1.6 = 2.6% | 2.62/2.8 = 6.9% |
| Norrie vs Wawrinka | £444 | 1.3/1.34 = 3.1% | 3.95/4.3 = 8.9% |

**Doubles had ZERO liquidity:** Romboli/Smith vs Pavlasek/Riki = £0 matched. Arneodo/Polmans vs Marti Pujol = £0 matched. Doubles markets are completely untradeable on Betfair Exchange.

**Key finding:** Tennis pre-match liquidity for ATP 500 main draw singles is £444-£5,746 per match, roughly 10-50x less than NBA. Spreads are wider across the board, especially on underdogs (6-12%). The market is less efficient than NBA but still functional for £5 flat stakes.

### 4. Tennis In-Play

One active match: Duckworth vs Napolitano (Mexico City Challenger) had **£397,764 matched** in-play. This is extraordinary for a challenger-level match and demonstrates that tennis in-play generates massive trading volume through point-by-point betting, even on obscure events. Other challenger matches had £1-£456 matched.

**Hypothesis:** The high in-play matched figure is cumulative from heavy in-play trading (people backing and laying throughout the match). This does not mean there's £397K sitting in the market at any moment -- it means that much has been traded across all points. This is a fundamentally different liquidity dynamic from pre-match.

### 5. Snooker World Championship

**Outright Winner Market:**
- Total matched: £154,768 across 95 selections
- Overround: 115.1% (back) / 94.2% (lay)
- Zhao Xintong favourite at 3.45, Judd Trump 6.8, O'Sullivan 8.6, Selby 10.5
- Spreads vary wildly by player: Robertson 29/30 (3.4%) vs Wu Yize 19.5/26 (33%) vs Lisowski 100/790 (690%)
- Decent depth on top players: Selby £123 to back at 10.5, Higgins £138 to lay at 34

**World Championship Qualifiers (In-Play, 10 matches):**

| Match | Matched | Notes |
|---|---|---|
| Brecel vs Chang Bingyu | £4,281 | Highest -- both well-known players |
| Jak Jones vs Marco Fu | £1,456 | Former top-16 player effect |
| Lei Peifan vs Jordan Brown | £1,264 | -- |
| Zak Surety vs Oliver Sykes | £1,225 | -- |
| Joe OConnor vs Kowalski | £818 | -- |
| Zhang Anda vs Revesz | £772 | -- |
| Gary Wilson vs Allan Taylor | £589 | -- |
| Ryan Day vs Ishpreet Singh Chadha | £585 | -- |
| Xu Si vs Liu Hongyu | £555 | -- |
| Pang Junxu vs Dylan Emery | £385 | Lowest |

**Key finding:** Snooker qualifier match liquidity is £385-£4,281. This is very thin. Several matches showed NO lay liquidity on one side. In-play spreads were enormous (8-30%+). Main draw Crucible matches would have more liquidity, but qualifiers are essentially untradeable for systematic betting at meaningful stakes. Fred should focus snooker betting on main draw only.

### 6. Darts

**Premier League Darts (TV event, Apr 16 -- 4 days away):**

| Match | Matched | Notes |
|---|---|---|
| Littler vs Price | £154 | Most liquid -- Littler effect |
| van Veen vs Humphries | £83 | -- |
| van Gerwen vs Clayton | £5 | -- |
| Bunting vs Rock | £0 | Zero liquidity |

**MODUS Super Series (Floor event, Mon):**

| Match | Matched | Notes |
|---|---|---|
| Barstow vs Stevenson | £2,530 | Anomalously high |
| Stevenson vs Potter | £1,294 | Anomalously high |
| Drayton vs Hall | £54 | More typical |
| Hall vs Coulson | £54 | -- |
| Potter vs Drayton | £44 | -- |
| Barstow vs Hall | £16 | -- |
| Coulson vs Barstow | £13 | -- |

**Key finding:** This directly addresses Fred's darts thesis. MODUS Super Series IS a floor event with liquidity on Betfair. BUT the liquidity is extremely thin -- £13-£54 on most matches with wide spreads (8-10% on favourites). The two anomalous matches (£1,294 and £2,530) suggest someone is trading those specific matchups, possibly a single sharp bettor. At £5 flat stakes, you might struggle to get matched at the displayed price. The Premier League (TV) matches had even less pre-match liquidity 4 days out, but would likely build significantly closer to the event.

**Implication for darts viability:** The floor-event thesis requires not just softer lines but sufficient liquidity to execute. With most matches at £13-£54 matched, even getting £5 on at the quoted price is uncertain. This is a significant practical constraint that paper trading wouldn't reveal (paper trading assumes you get matched).

### 7. Cricket -- IPL (Queued Domain)

**Indian Premier League:**

| Match | Date | Matched | Fav Spread | Dog Spread |
|---|---|---|---|---|
| Sunrisers vs Rajasthan | Mon 15:00 | £67,792 | 1.83/1.84 = 0.5% | 2.2/2.22 = 0.9% |
| Chennai vs Kolkata | Apr 14 | £2,391 | 1.86/1.91 = 2.7% | 2.1/2.18 = 3.8% |
| RCB vs Lucknow | Apr 15 | £91 | 1.62/1.76 = 8.6% | 2.3/2.62 = 13.9% |
| Mumbai vs Punjab | Apr 16 | £26 | 1.81/1.99 = 9.9% | 2.02/2.24 = 10.9% |

**Pakistan Super League:**
- Peshawar vs Multan (Mon): £33,012 matched

**Key finding:** IPL has EXCELLENT liquidity and EXTREMELY TIGHT spreads for the next-day match. Sunrisers vs Rajasthan at £67,792 with a 0.5% favourite spread is tighter than any NBA game I observed. However, liquidity drops off a cliff: 2 days out = £2.4K, 3 days = £91, 4 days = £26. This means any IPL betting would need to be same-day or day-before.

**Implication for IPL as queued domain:** The market efficiency (0.5-0.9% spreads) suggests a LOT of sharp money pricing these markets. The toss-window edge thesis needs to overcome this efficiency. However, the toss happens just before the match and causes a structural shift (batting first vs chasing is worth 5-10% in win probability). If the pre-toss market hasn't fully adjusted, there could be a brief window of mispricing. This is testable.

### 8. Cross-Sport Liquidity Comparison (Sun 12 Apr, ~23:10 UK)

All figures are pre-match matched amounts for the next day's events:

| Sport | Typical Match Liquidity | Best Match | Worst Match | Fav Spread |
|---|---|---|---|---|
| **NBA** | £15K-£52K (tonight) | £191K (Hawks/Heat) | £3.4K (Bulls/Mavs tmrw) | 0.8-1.8% |
| **Football (Brazilian A)** | £194K-£299K (in-play) | £299K (Flu/Fla) | -- | Varies |
| **IPL Cricket** | £68K (next day) | £68K (SRH/RR) | £26 (4 days out) | 0.5-0.9% |
| **Tennis (ATP 500)** | £800-£5.7K | £5.7K (Munar/Jodar) | £444 (Norrie/Wawrinka) | 0.7-3.1% |
| **Snooker (WC Quals)** | £385-£4.3K (in-play) | £4.3K (Brecel/Chang) | £385 (Pang/Emery) | 8-30%+ |
| **Darts (MODUS floor)** | £13-£54 | £2.5K (anomaly) | £13 | 8-10% |
| **Darts (PL TV)** | £0-£154 (4 days out) | £154 (Littler/Price) | £0 (Bunting/Rock) | ~1-3% |

**Key finding:** There is a clear liquidity hierarchy: Football > NBA > IPL Cricket > Tennis > Snooker > Darts. But liquidity alone doesn't determine where edge lives. The hypothesis from Fred's spec -- that thin markets correlate with less efficient pricing -- is partially supported. Snooker and darts have the widest spreads AND the least liquidity, which suggests less sharp money and potentially more mispricing. But the execution cost (wide spreads + uncertain fill) partly offsets any theoretical edge.

---

## Hypotheses

### H1: NBA underdog execution cost is a hidden drag on ROI
**Observation:** NBA underdog spreads are 2-8x wider than favourite spreads. If Fred's model identifies value on an underdog at 4.6, the actual execution might be at 4.8 (lay) or 4.5 (back), eating into the edge.
**Test:** Compare Fred's recommended entry price vs actual achieved price on historical NBA underdog bets. Calculate the spread cost as a percentage of expected edge.

### H2: IPL toss-window edge is real but needs sub-5-minute execution
**Observation:** IPL pre-match spreads are 0.5-0.9% with £68K+ matched -- very efficient. But the toss creates a structural 5-10% shift in win probability. If the market takes even 2-3 minutes to fully reprice after the toss, there's a window.
**Test:** Monitor 5-10 IPL matches at toss time. Record the odds 1 minute before toss, at toss, and at 1/2/5 minutes after. Measure how quickly the market adjusts. If adjustment takes >2 minutes, the edge exists.

### H3: Darts floor events are structurally untradeable, not just illiquid
**Observation:** MODUS Super Series matches have £13-£54 matched with 8-10% spreads. Two anomalous matches had £1.3-2.5K, suggesting a single trader.
**Test:** Attempt to place a £5 back bet on 5 MODUS matches and measure fill rate. If fewer than 3/5 fill at the quoted price, the floor-event thesis is practically dead regardless of whether the lines are soft.

### H4: Snooker main draw matches will have 10-50x more liquidity than qualifiers
**Observation:** Qualifiers had £385-£4.3K. The outright winner market had £155K. Main draw Crucible matches (Trump, O'Sullivan, etc.) should attract significantly more interest.
**Test:** Check main draw match liquidity when the first round begins (likely next weekend). If main draw matches hit £10K-£50K pre-match with tighter spreads, snooker becomes viable for £5 stakes.

### H5: Tennis in-play trading generates 50-200x the pre-match matched volume
**Observation:** Mexico City Challenger pre-match likely had a few hundred pounds matched, but accumulated £397K in-play. This suggests massive point-by-point trading activity.
**Test:** Compare pre-match matched amount (captured 2 hours before start) vs final matched amount for 10 ATP Barcelona matches. If the ratio is consistently >50x, there may be an in-play tennis trading opportunity -- though this would be a fundamentally different strategy from Fred's current pre-match value betting approach.

### H6: NBA handicap markets are liquid enough for systematic betting but spreads eat the edge
**Observation:** Hawks/Heat handicap had £46,521 matched at +10.5, with 10.5% spreads. This is liquid enough but the spread cost is high.
**Test:** If Fred ever considers handicap betting (currently not in scope), compare handicap market spreads vs moneyline spreads across 20 games. If handicap spreads are consistently >8%, the execution cost likely exceeds any model edge.

---

## Recommended Next Steps

1. **NBA spread cost analysis (High priority):** Calculate the actual execution cost of underdog bets vs the model's estimated edge. If spreads are eating >3% of a 15% edge, consider whether the edge threshold should be adjusted upward for underdogs priced above 4.0.

2. **IPL toss-window feasibility study (Medium priority, time-sensitive):** The IPL season is running NOW. Monitor 5 matches at toss time to test H2. This requires real-time observation at ~14:30 UK time on match days. If the window exists, it could be a new domain.

3. **Snooker main draw liquidity check (Medium priority):** When World Championship first round starts (likely next weekend), check match liquidity and spreads. This will determine whether snooker is viable beyond paper trading.

4. **Darts practical execution test (Low priority):** Place 5 x £5 bets on MODUS matches to test fill rates. This will definitively answer whether floor events are tradeable. If they're not, recommend parking darts entirely.

5. **Do NOT pursue in-play betting for any sport.** The spread widening in-play (NBA underdog: 4.3% → 12.5%) makes systematic value betting in-play structurally uneconomic at our stake sizes. Pre-match execution is always cheaper.

---

## Limitations

1. **Single time window:** All observations from ~23:08-23:16 UK on a Sunday night. NBA games were just starting (maximum pre-match liquidity), but tennis/darts were showing tomorrow's fixtures (lower liquidity than they'd have closer to start time).

2. **No price movement tracking over time:** I observed Hawks/Heat for ~2 minutes of game time. A fuller study would track odds movement across an entire quarter or match.

3. **Betfair only:** Exchange prices. Sportsbook odds may differ and could offer better value in thin markets (though Fred's methodology is Exchange-focused).

4. **End-of-season NBA dynamics:** Some games (Nets/Raptors at 34/1.02) show extreme end-of-season pricing. Regular season or playoffs would show different liquidity patterns.

5. **MODUS Super Series sample:** Only saw one day's card. Floor event liquidity may vary by day of week or which players are competing.

6. **Could not test actual execution speed** -- observing displayed prices is different from testing whether you can get matched at those prices.
