# Wiki Agent Report -- 2026-04-15

> Scheduled run. Slack #ttai-employees connector unavailable, filing report in-repo per error-handling rule.

## Sources Scanned
- Wiki inbox/ (1 file, already-processed, moved to inbox/processed/)
- operations/fred-reports/ (last report: 2026-04-13 Betfair exploration)
- Strategy pages, predicted-loser rule cluster, NBA/tennis domain pages
- Slack #ttai-employees: not reachable via connector

## Updates
- **betting-rules/predicted-loser-rule.md** -- Aligned record with NBA page: 0/9 -> 0/18 (NBA 8/8, Tennis 10/10). Fred's 2026-04-14 formalisation recommendation noted; decision flagged for Andy, not taken here.
- **betting-rules/never-back-predicted-loser.md** -- Same update. Progress is now 18/20 bets.
- **betting-rules/active-rules.md** -- Summary + status columns updated to match 18/18 reality.
- **index.md** -- Predicted-loser summary lines refreshed; date bumped.
- **inbox/** -- Moved 2026-04-12-agent-browser-prompt-caching-and-optimisation-research.md to inbox/processed/ (content was ingested in the 2026-04-12 log entries but the file itself had never been moved).

No new pages created. No new content in inbox to process.

## Patterns

1. **Predicted-loser evidence has overtaken the procedural threshold.** At 18/18 with 0% win rate, the statistical confidence on a 0-or-near-0 win rate is already past anything the marginal 19th and 20th bets could add. The 20-bet threshold exists to prevent small-sample over-reaction; at this sample size and tail probability, the question is procedural (does Andy want to honour the rule-of-20) not evidential. Fred has recommended early formalisation. Worth resolving on next reply -- waiting costs nothing but also gains nothing.

2. **Revenue de-concentration is happening through a different channel than planned.** The Q2 plan counted on Mercia go-live (15 April) to be the first big step down from the 73% KW Bell dependency. Mercia has slipped (Outlook/Entra still blocked) -- yet de-concentration is happening anyway, via JDW inbound (£500 + £200/mo) and Tonic friend-referral (£1,750). The inbound/referral loop is out-performing the planned channel. Worth examining whether Mercia's importance has been overstated, and whether Mark-Lite inbound + warm referral should get more of Andy's time than Mercia unblocking work.

3. **Agent-browser's atomic-actions pivot is an instance of the removal principle.** Per the 2026-04-14 log, agent-browser is moving from scripted workflows toward atomic actions. This is structurally "removing the workflow layer" -- the same shape as removing streak dampening from the NBA model (2026-04-08) and removing features in compound-evaluation work. The candidate principle "capabilities before workflows" and the existing [[removal-as-valuable-as-addition]] principle point at the same thing. Worth considering whether they collapse into one.

4. **Fred's last report is 2 days old at a non-trivial moment (regular-season close, predicted-loser threshold crossing).** Either Fred is intentionally quiet during the play-in transition, or the daily report cadence has slipped. Wiki cannot tell which without Slack access. Flagging for Andy.

## Questions for Andy

- Formalise predicted-loser rule now at 18/18, or wait for 20? Fred has recommended early formalisation; wiki has not changed rule status pending your call.
- Mercia go-live -- 15 April (today) has passed with the Outlook/Entra blocker unresolved. The overview.md "Must-Hit" bullet still lists that date. Want it rewritten now, or wait for a fresh go-live date from Solaas IT?
- Has Fred posted anything since 2026-04-13? If so, is the report going somewhere other than operations/fred-reports/?
- Is the Slack connector meant to be live for Wiki yet? Today's scan fell back to in-repo reporting.

---
Wiki updated: predicted-loser-rule.md, never-back-predicted-loser.md, active-rules.md, index.md, log.md, inbox/processed/ (one file moved).
