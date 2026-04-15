# Planning Data Serves Site Trades, Not Supply-Chain Trades

> Planning portal leads have high value for trades that win work directly from developers and low value for trades subcontracted through supply chains.
> Last updated: 2026-04-12

## The Principle

Construction leads sourced from planning applications (PlanIt API, council portals) are relevant to **site-based trades** — firms that win work by approaching developers, architects, and site managers directly. They are not relevant to **supply-chain trades** — firms that win work through main contractor subcontracting, tender processes, or supply chain relationships.

## Where It Was Discovered

Mark-Lite campaign analysis, April 2026. Compound evaluation L3 (trade segment split) across 65 firms in Warwickshire and Northamptonshire:

| Trade Classification | Firms | Warm Replies | Rate | Opt-Outs |
|---|---|---|---|---|
| **Site-based** (Groundworks, Brickwork, Scaffolding) | 19 | 4 | 21.1% | 0 |
| **Office-managed** (Electrical, HVAC, Roofing, Drainage) | 34 | 0 | 0% | 2 |

The overall 6.2% warm reply rate masked this split entirely — a textbook [[majority-class-trap]].

Three structural reasons for the gap:
1. **Lead relevance:** Electrical, HVAC, and Roofing rarely appear explicitly in planning applications. Leads sent to these trades feel irrelevant.
2. **Firm structure:** Site trade directors read their own email. Office-managed trade firms have admin filtering.
3. **Business development pattern:** Site trades win work from developers directly. Supply-chain trades win through main contractors — planning data doesn't map to how they actually get jobs.

## Where Else It Applies

- **[[mark]]** — Client variant selection. New Mark clients in site-based trades (Groundworks, Brickwork, Scaffolding, Civil Engineering) will get better results from planning-sourced leads than supply-chain trades.
- **[[mark-lite]]** — Campaign segmentation. Future campaigns should separate site trades from office-managed trades and use different lead sources for each.
- **Construction Intelligence opportunity** (see [[opportunities]] Pattern 3) — A standalone data subscription would primarily serve site-based trades. Supply-chain trades would need tender portal data instead.
- **[[planit-api]]** — The PlanIt data is structurally more valuable to some trades than others. This should inform which clients are pitched the planning monitoring product.

## Boundary Conditions

- **Civil Engineering** had 0 warm replies but only 5 firms — insufficient data. Civil engineering straddles both classifications (some firms bid directly, some subcontract). Needs more data before classifying.
- **Scaffolding** had only 2.8 leads per firm (lowest supply) but still generated a warm reply — suggesting even modest lead flow works for the right trade.
- **Tender portal data** may solve the supply-chain trade problem. Electrical, HVAC, and Roofing firms win through Find-a-Tender, Construction Enquirer, and contractor supply chains — these are the appropriate lead sources, not planning applications.

## Related Principles

- [[market-efficiency-varies-within-domain]] — The lead source must match the trade's business development pattern
- [[majority-class-trap]] — Overall campaign metrics mask the site-vs-office split
- [[strict-trade-matching]] — Necessary but insufficient; the lead SOURCE must also match the trade type
- [[selectivity-is-everything]] — Better to focus on 19 site-trade firms at 21% than 65 mixed firms at 6%

## Links

- [[mark-lite]] — Where the data was collected
- [[mark]] — Product implications for client selection
- [[planit-api]] — The data source this principle constrains
- [[compound-evaluation]] — The framework that surfaced this finding (L3 edge case analysis)

## Sources

- Mark-Lite Warwickshire Outreach Tracker + Mark-Lite Northants Outreach Tracker (April 2026 analysis)
- Mark-Lite Campaign Analysis April 2026.docx
