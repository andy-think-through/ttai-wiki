# Wiki Agent Report -- 2026-04-16 (follow-up scan)

## Context

Previous run today (authoritative recovery) processed Routines migration ingest, created 5 pages, updated 9. That work was committed to `claude/magical-goldberg-tSVR5`. This run merged that work and performed a data integrity pass.

## UPDATES

- **NBA P&L corrected**: overview.md and index.md both had +£38.90 (stale). Authoritative figure from nba.md is +£28.90 -- regular season closed April 13 after CHI @ DAL -£10 loss. Total betting YTD corrected from £49.86 to £39.86.
- **Tennis P&L corrected** in index.md: was +£5.53 (April 8), now +£7.96 (per tennis-atp.md April 10).
- **Duplicate pipeline row fixed** in overview.md: MJM-Consulting and Carmen-MacDougall were listed twice.
- **Holmes-Workholding added** to pipeline table -- was missing since overview was last restructured. Status: Prospect (stale since April 8).
- **Opportunities priority matrix** updated: items 1 and 3 flagged as 8 days unacted. CI tier (item 9) noted as in motion. Pattern 2 revenue figures updated to reflect de-concentration.

## PATTERNS

- **P&L propagation is a recurring failure mode.** Domain pages (nba.md, tennis-atp.md) get updated by Fred or the daily scan, but the figures don't propagate to overview.md or index.md. This is the third time a P&L drift has been caught. Consider making domain pages the single source of truth and generating overview figures from them rather than maintaining copies.
- **Unacted priority items decay silently.** Items 1 (pipeline selectivity scoring) and 3 (darts/crypto removal review) from April 8 have sat for 8 days without progress. They're not blocked -- they're just not triggered. The priority matrix needs a review cadence or it becomes a wish list. The crypto review on April 24 is the natural forcing function for item 3.
- **Holmes-Workholding is approaching phantom value territory.** 8 days with no interaction update. Pattern 5 in opportunities.md already flagged it as a potential structural loser (long-term upside masking short-term non-conversion). If no movement by end of April, it's worth parking.

## QUESTIONS FOR ANDY (carried forward + new)

1. **Branch strategy** (from previous run, still open): Should Wiki push to `main` directly? Personal wiki repo -- branching creates orphaned work.
2. **Predicted-loser rule** (from previous run): Formalise at 18/18 or wait for 20?
3. **Mercia** (from previous run): Gmail send-as workaround or keep waiting on Solaas IT?
4. **Fred status** (from previous run): Last reported 04-13. NBA playoffs live. Is he running?
5. **Holmes-Workholding** (new): Any update since April 8? If not, flag for parking review.
6. **Priority matrix review**: Items 1 and 3 are 8 days unacted. Still priorities, or overtaken by events?
