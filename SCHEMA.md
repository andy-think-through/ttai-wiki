# Andy Allen — Unified Knowledge Base

> Schema for an LLM-maintained wiki across all of Andy Allen's business activities.
> This file tells Claude Code how the wiki is structured, what the conventions are,
> and what workflows to follow when ingesting sources, answering questions, or maintaining the wiki.
>
> Based on Karpathy's LLM Wiki pattern (April 2026).

---

## Purpose

Andy runs multiple interconnected projects — AI consultancy, productised sales agents, browser automation, SEO strategy work, and a value-betting portfolio. These currently live in four separate Claude project folders with no cross-pollination. Knowledge discovered in one area (e.g. "removal can be as valuable as addition" from betting) applies elsewhere (e.g. Mark's email templates) but never reaches it.

This wiki is the synthesised layer that sits above the raw project folders. It is where:
- Cross-cutting principles live (discovered anywhere, applicable everywhere)
- The business strategy is explicit and linked to each income stream
- Client/prospect knowledge compounds rather than being re-derived each chat
- Operational knowledge is navigable, not buried in lessons-learned docs
- Methodologies are documented as reusable tools, not domain-specific artefacts

The wiki answers: **"Given everything I know across all my projects, what should I be doing and why?"**

---

## Architecture

```
wiki/                              ← LLM-maintained. Claude owns this entirely.
├── index.md                       ← Master catalog: every page, one-line summary, category
├── log.md                         ← Append-only chronological record of all wiki operations
│
├── strategy/                      ← Business direction, goals, revenue tracking
│   ├── overview.md                ← The 100×100 model, current revenue, what's working
│   ├── time-allocation.md         ← Where Andy's time goes and where it should go
│   └── quarterly-priorities.md    ← Current quarter's focus areas and decision log
│
├── methodologies/                 ← Reusable approaches that apply across domains
│   ├── autostrategy.md            ← The full AutoStrategy methodology
│   ├── autoresearch.md            ← Karpathy's original pattern + Andy's adaptations
│   ├── compound-evaluation.md     ← L1-L5 framework (usable beyond betting)
│   ├── results-diagnostic.md      ← Post-hoc analysis + three-gate validation
│   ├── walk-forward-validation.md ← Rolling-fold evaluation for regime-dependent domains
│   └── probability-calibration.md ← Isotonic regression for any domain comparing model vs market
│
├── products/                      ← Things that earn or could earn money
│   ├── consulting.md              ← TTAI consulting (audit → design → implement model)
│   ├── mark.md                    ← Mark AI sales agent (product definition, pricing, architecture)
│   ├── mark-lite.md               ← Andy selling Mark's output directly to tradespeople
│   ├── agent-browser.md           ← Browser agent product (Hike internal + external commercial)
│   ├── hike-ses.md                ← Search Everywhere Strategy docs for Hike clients
│   ├── knowledge-assistant.md     ← RAG chatbot product (AnythingLLM/Onyx, exploring)
│   ├── betting-portfolio.md       ← AutoStrategy value betting as income stream
│   └── tonic-creative-agent.md    ← Ad creative intelligence agent (new archetype)
│
├── clients/                       ← One page per client/prospect. Living status + history.
│   ├── kw-bell.md                 ← Bell Contracting: audit done, solution design next
│   ├── accxel.md                  ← KW Bell subsidiary: discovery day 28 Apr
│   ├── mercia-flooring.md         ← Mark agent client: school outreach, go-live 15 Apr
│   ├── hawks-scaffolding.md       ← Mark agent client: first live customer
│   ├── midlands-bat-surveys.md    ← Mark agent client: planning portal monitoring
│   ├── holmes-workholding.md      ← Mark prospect: reviewing proposal
│   ├── mjm-consulting.md          ← Marketing strategy prospect: competing vs YER
│   ├── ih-group.md                ← Consultancy prospect: via Malcolm, follow-up drafted
│   ├── tonic-health.md            ← Creative agent prospect: proposal sent £1,750
│   ├── carmen-macdougall.md       ← Workshop/collaboration: skill swap dates offered
│   ├── jdw-brickwork.md           ← Mark-Lite inbound lead: meeting 14 Apr
│   └── _template.md               ← Template for new client pages
│
├── people/                        ← Key individuals in Andy's network
│   ├── malcolm-freeman.md         ← Oxygen Elements, BNI Master Connector
│   ├── gareth-hunt.md             ← KW Bell FD, referral source
│   ├── sunna-van-kampen.md        ← Tonic Health CEO, friend
│   ├── bryn.md                    ← Hike SEO MD
│   └── kieran.md                  ← Hike technical colleague
│
├── principles/                    ← Hard-won lessons. Discovered anywhere, applicable everywhere.
│   ├── _index.md                  ← All principles with origin, domain applicability, exceptions
│   ├── raw-probabilities-lie.md
│   ├── removal-as-valuable-as-addition.md
│   ├── trust-the-model-over-punditry.md
│   ├── scheduled-tasks-need-zero-intervention.md
│   ├── phantom-value.md
│   ├── derivative-markets-harder-than-primary.md
│   ├── data-leakage-silent-killer.md
│   ├── selectivity-is-everything.md
│   ├── majority-class-trap.md
│   ├── market-efficiency-varies-within-domain.md
│   ├── dont-reveal-methodology-before-paid.md
│   ├── position-next-stage-not-bigger-commitment.md
│   ├── let-clients-surface-pain-points.md
│   ├── email-quality-over-volume.md
│   ├── strict-trade-matching.md
│   └── ...                        ← New principles added as discovered
│
├── operations/                    ← How things actually work day-to-day
│   ├── cowork-pipeline.md         ← Daily betting ops orchestration
│   ├── tool-routing.md            ← Which tool for which task (Cowork, Claude Code, Chrome MCP, etc.)
│   ├── betfair-integration.md     ← Exchange access, API plans, Computer Use workaround
│   ├── planit-api.md              ← Rate limits, region IDs, JSON vs GeoRSS, OR operator
│   ├── google-sheets-patterns.md  ← openpyxl, max_row trap, formatting preservation
│   ├── email-infrastructure.md    ← Lemwarm, Hunter.io, verification patterns
│   ├── manus-platform.md          ← Skills packaging, Gmail/Outlook MCP, rclone
│   ├── vps-crypto.md              ← DigitalOcean setup, systemd, Telegram alerts
│   ├── browser-agent-arch.md      ← Agent loop, cost controls, viewport constraints
│   └── known-failure-modes.md     ← Computer Use timeouts, sandbox network restrictions, etc.
│
├── domains/                       ← Specific application areas for AutoStrategy betting
│   ├── nba.md                     ← Model, rules, results, diagnostics
│   ├── tennis-atp.md              ← Model, surface stratification, calibration
│   ├── snooker.md                 ← Model, bugs caught, WC qualifiers gap
│   ├── darts.md                   ← Model, floor event problem, viable markets
│   ├── efl-championship.md        ← Parked: calibration discovery, awaiting OOS data
│   ├── crypto.md                  ← Paper trading, BTC + multi-pair, review due Apr 24
│   ├── horse-racing.md            ← Concluded: no edge, data leakage lesson
│   └── football-corners.md        ← Parked: domain-level ceiling
│
└── betting-rules/                 ← Active rules governing bet placement
    ├── active-rules.md            ← All current rules in one place
    ├── predicted-loser-rule.md    ← 0/6, approaching formalisation at 20
    ├── injury-veto-80pct.md       ← Only skip if player in 80%+ of games
    ├── away-team-threshold.md     ← 20%+ edge required for away underdogs
    ├── grass-veto.md              ← Tennis: no bets on grass (pending implementation)
    └── never-back-predicted-loser.md

raw/                               ← Immutable source documents. NEVER modify.
├── autostrategy/                  ← Papers, SKILLs, STATUS, experiment logs, daily briefings
├── mark/                          ← SKILL files, tracker snapshots, campaign results
├── ttai/                          ← Client docs, audit outputs, invoices, pitch decks
├── agent-browser/                 ← README, code docs, workflow docs, run artifacts
└── chat-exports/                  ← Exported conversation transcripts when available
```

---

## Page Types and Conventions

### Every wiki page must have:

```markdown
# Page Title

> One-sentence summary of what this page covers.
> Last updated: [date]

## Content

[The actual content — keep concise, link liberally]

## Links
- [[related-page-1]] — why it's related
- [[related-page-2]] — why it's related

## Sources
- Which raw source documents informed this page
- Which conversations or chat sessions contributed
```

### Page type conventions:

**Strategy pages** — Written in first person ("We're currently focused on..."). Updated when priorities shift. Always link to the products/clients they reference.

**Methodology pages** — Written as reusable documentation. Someone unfamiliar with Andy's work should be able to understand and apply the methodology from the page alone. Include: what it is, when to use it, how it works, examples, limitations.

**Product pages** — Describe the product, its pricing, its current status, which clients use it, and what methodology/technology powers it. Link to relevant client pages and methodology pages.

**Client pages** — Living status documents. Include: who they are, what we're doing for them, current status, next action, revenue (invoiced and projected), key contacts, communication preferences, and a chronological log of significant interactions. When a client engagement progresses, update the page — don't create a new one.

**People pages** — Brief. Name, role, how Andy knows them, what referrals/connections they've made, communication preferences if known. Only create for people who appear across multiple contexts or are key network nodes.

**Principle pages** — Short and punchy. State the principle, explain where it was discovered (with link to domain/product page), list where else it applies, note any known exceptions. The `_index.md` file lists all principles in a single scannable table.

**Operations pages** — Practical how-to documents. Include: what the tool/system does, how to use it, known gotchas, failure modes, and workarounds. Written so that Andy (or a future team member) can follow them without additional context.

**Domain pages** — AutoStrategy betting domains. Include: model description, data source, current status (live/paper/parked/concluded), key results, active rules that apply, and a decision log of significant changes.

**Betting rule pages** — State the rule, its evidence base (sample size, win/loss record), when it was formalised, which domains it applies to, and any pending validation milestones.

---

## Cross-Referencing Rules

Use `[[page-name]]` wiki-link syntax throughout (compatible with Obsidian).

**Mandatory cross-references:**
- Every client page must link to the product(s) being used and the people involved
- Every product page must link to its methodology and its active clients
- Every principle must link to where it was discovered and where else it applies
- Every domain page must link to its active betting rules and relevant methodology pages
- Every methodology page must link to the products/domains where it's currently applied

**The goal:** You should be able to start on any page and navigate to any related page within 2 clicks. If you find yourself writing something that relates to another page but there's no link, add one.

---

## Operations

### Ingest

When Andy provides new source material (a document, a conversation transcript, a daily briefing, a set of results, or verbal updates in chat):

1. Save the raw source to `raw/[appropriate-subfolder]/` with a descriptive filename and date
2. Read the source and identify what's new or changed
3. For each new piece of information, determine which wiki pages it affects
4. Update each affected page — add new information, revise outdated claims, note contradictions
5. If the information doesn't fit any existing page, create a new one following the appropriate page type convention
6. Update `index.md` with any new pages
7. Append an entry to `log.md`:
   ```
   ## [YYYY-MM-DD] ingest | Source Title
   - Source: [filename or description]
   - Pages created: [list]
   - Pages updated: [list]
   - Key new information: [1-2 sentence summary]
   ```

**Single-source ingests** (one document or briefing): process interactively, discuss key takeaways with Andy.

**Batch ingests** (initial setup or catching up): process systematically, provide a summary of all changes at the end.

### Query

When Andy asks a question, search the wiki first (via `index.md` or keyword search), then drill into relevant pages. If the answer requires synthesising multiple pages, do so — and consider whether the synthesis is valuable enough to file as a new wiki page.

Questions that produce reusable analysis (comparisons, strategic assessments, decision frameworks) should be saved as wiki pages under the appropriate category. The question-and-answer disappears from chat history; the wiki page persists.

### Lint

Periodically (suggest every 2-4 weeks, or when Andy asks), perform a health check:

1. **Staleness** — Are any pages outdated? Client statuses that haven't been updated, domain results that are stale, betting rules with enough new data to revisit?
2. **Contradictions** — Does any page claim something that another page contradicts?
3. **Orphans** — Are there pages with no inbound links? (These are likely stale or misplaced.)
4. **Missing pages** — Are there concepts, clients, or topics referenced frequently in other pages but lacking their own page?
5. **Missing cross-references** — Are there obvious connections between pages that aren't linked?
6. **Gaps** — Based on what the wiki knows, what questions should Andy be investigating? What data is missing?

Output the lint results as a checklist. Append to `log.md`.

---

## Initial Ingest Plan

The wiki starts empty. The initial build should ingest the following raw sources in this order:

### Phase 1: Business foundation
1. `claude.md` (TTAI project) — master business context
2. `TTAI_Project_Context.md` — full client engagement details
3. `PROJECT_INSTRUCTIONS.md` (TTAI) — working patterns and commercial rules

**Creates:** strategy/overview.md, all client pages, all people pages, products/consulting.md, products/mark.md, products/mark-lite.md, products/hike-ses.md, products/knowledge-assistant.md, operations/email-infrastructure.md, operations/planit-api.md

### Phase 2: AutoStrategy & betting
4. `AutoStrategy_Paper_v6.md` — full methodology and domain history
5. `AutoStrategy_SKILL_v3.md` — reusable methodology documentation
6. `STATUS.md` — current state of all betting domains
7. `daily-skill-lessons-learned.md` — operational knowledge

**Creates:** all methodology pages, all domain pages, all betting-rules pages, all principle pages, products/betting-portfolio.md, operations/cowork-pipeline.md, operations/tool-routing.md, operations/vps-crypto.md, operations/google-sheets-patterns.md, operations/known-failure-modes.md

### Phase 3: Agent Browser
8. `README.md` (Agent Browser project) — architecture and workflow docs
9. `project-instructions.txt` (Agent Browser) — project framing

**Creates:** products/agent-browser.md, operations/browser-agent-arch.md, updates to clients/kw-bell.md (linking audit finding to agent browser solution)

### Phase 4: Mark operational detail
10. `FULL_PROJECT_CONTEXT.md` (TTAI) — deep Mark/Mark-Lite build details
11. Mark SKILL files (if available in raw/)

**Updates:** products/mark.md, products/mark-lite.md, all Mark client pages with operational detail, operations/manus-platform.md

### Phase 5: Cross-reference pass
After all sources are ingested, do a full cross-reference audit:
- Link KW Bell audit finding → Agent Browser product → browser-agent-arch operations page
- Link AutoStrategy methodology → Agent Browser autoresearch (parameter optimization)
- Link Mark operational lessons → principles (email quality, strict trade matching, etc.)
- Link consulting discovery patterns → methodology (audit → design → implement as a reusable framework)
- Ensure every product links to its clients and vice versa
- Ensure every principle links to its origin and all applicable domains

### Phase 6: Strategy synthesis
Write `strategy/overview.md` — the 100×100 model page that ties everything together:
- Current revenue by stream (consulting, Mark, Hike, betting)
- Product pipeline (what's live, what's building, what's exploring)
- The flywheel: consulting → uncovers product opportunities → products create recurring revenue → betting adds passive income
- Key network relationships driving growth (Malcolm, Gareth, Sunna)
- Time allocation: where Andy's time currently goes vs where it should go

---

## Naming Conventions

- **Filenames:** lowercase, hyphens, no spaces. `kw-bell.md`, `probability-calibration.md`
- **Wiki links:** Match filename. `[[kw-bell]]`, `[[probability-calibration]]`
- **Dates:** ISO 8601. `2026-04-08`
- **Currency:** GBP (£) unless explicitly USD
- **Client shortnames:** Used in filenames and as quick references. Match the natural way Andy refers to them ("KW Bell", "Mercia", "Hawks", "Tonic").

---

## What NOT to Put in the Wiki

- **Raw data files** (CSVs, XLSX trackers, code) — these stay in `raw/` or in the project folders
- **Full conversation transcripts** — store in `raw/chat-exports/`, extract key information into wiki pages
- **Speculative ideas that haven't been discussed** — the wiki captures what Andy has decided or is actively considering, not the LLM's suggestions
- **Sensitive credentials** — no API keys, passwords, bank details, or client financial data beyond invoice amounts

---

## Maintenance Cadence

- **After every significant chat session:** Update affected wiki pages with new information
- **After every daily betting briefing:** Update relevant domain pages with results
- **After every client interaction:** Update the client page with new status/next actions
- **Weekly:** Quick lint pass — check for staleness, update strategy/overview.md
- **Monthly:** Full lint — orphans, contradictions, missing pages, gap analysis

---

## How This Relates to Existing Project Folders

The four Claude project folders (AutoStrategy, Mark/Mark-Lite, Think Through AI, Agent Browser) continue to exist. They remain the working environments for domain-specific tasks — placing bets, drafting emails, building browser agents.

The wiki sits above them. It is the place where:
- Knowledge that crosses boundaries lives (principles, methodologies, strategy)
- The business-level view is maintained (which clients, which products, what's the priority)
- Operational knowledge is consolidated (tool routing, known failures, platform quirks)

When working in a project folder, Claude should check the wiki for relevant context that might live in a different project's domain. When discoveries are made in any project, they should be ingested into the wiki so they're available everywhere.

The wiki is not a replacement for the project folders. It's the connective tissue between them.
