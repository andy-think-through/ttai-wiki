# PlanIt API

> Planning application data source for [[mark]] and [[mark-lite]] lead finding. Real-time UK planning applications indexed and searchable. Rate limit 1 req/min; OR operator support; region IDs; JSON vs. GeoRSS trade-offs.
> Last updated: 2026-04-08

## Overview

**PlanIt** (planit.org.uk) aggregates planning applications from UK local authorities in real-time. It is the primary data source for Mark lead discovery across all clients.

### What PlanIt Provides

- **Live planning applications** — Updated daily, typically 24-48 hours after local authority publishing
- **Searchable by keyword** — "loft conversion", "demolition", "warehouse", etc.
- **Searchable by region** — England divided into regional IDs; can combine multiple
- **Full descriptions** — JSON endpoint returns complete application text (GeoRSS truncates)
- **Agent/contact data** — `agent_company` field identifies architect, planning consultant, etc.
- **Web interface + API** — Both available; API preferred for automation

### Gotchas

1. **Rate limit: 1 request per minute** — Strict. Exceed it and you get HTTP 429 with lockout up to 380 seconds
2. **Database timeout: 45 seconds** — Large queries timeout; must split or simplify
3. **Circle searches time out** — Geographic boundary/radius searches don't work; use region IDs instead
4. **GeoRSS truncates descriptions** — Use JSON endpoint for full text matching

## API Endpoints

### GeoRSS Format (Geo-RSS Atom Feed)
```
https://www.planit.org.uk/api/applics/georss?auth=[region]&recent=[days]&sort=-start_date&pg_sz=[pagesize]
```

**Output:** XML feed with `<title>` (address), `<summary>` (description), `<published>` (date), `<link>` (portal URL)

**When to use:** Loading in browser (no 429 rate limiting); reading programmatically with XML parser

**Example:**
```
https://www.planit.org.uk/api/applics/georss?auth=Warwickshire&recent=21&sort=-start_date&pg_sz=50
```

### JSON Format (Structured Data)
```
https://www.planit.org.uk/api/applics/json?auth=[region]&recent=[days]&search=[keywords]&pg_sz=[pagesize]&select=[fields]
```

**Output:** JSON array of application objects with full descriptions, agent company, application type, etc.

**When to use:** Keyword filtering (server-side), field selection (faster), extracting structured data

**Important:** Direct `curl`/`requests` calls to JSON endpoint trigger 429 rate limiting. Use browser-based loading instead (or fallback to SMTP validation if needed).

**Example:**
```
https://www.planit.org.uk/api/applics/json?auth=469,468&recent=7&search=loft+conversion+or+barn+conversion&pg_sz=500&select=uid,description,address,start_date,area_name,url,app_type,agent_company
```

## Region IDs

PlanIt uses alphanumeric region identifiers OR numeric auth codes:

### Warwickshire (for Hawks)
- `auth=Warwickshire` (name)
- Single request covers entire region

### West Midlands (Bat Surveys)
- `auth=469` (numeric ID)
- Covers 32 planning authorities: Birmingham, Coventry, Solihull, Warwick, Dudley, Sandwell, Walsall, Wolverhampton, etc.

### East Midlands (Bat Surveys)
- `auth=468` (numeric ID)
- Covers 40 planning authorities: Derby, Leicester, Nottingham, Northampton, Lincoln, Rutland, etc.

### Northamptonshire (Mark-Lite)
- New unitary structure (2021 merger split into North/West Northamptonshire + updated Northampton)
- Primary: `auth=North+Northamptonshire`, `auth=West+Northamptonshire`
- Secondary (legacy, still works): `auth=Northampton`, `auth=Kettering`, `auth=Corby`, `auth=Wellingborough`, `auth=Daventry`
- Can combine: `https://...?auth=North+Northamptonshire,West+Northamptonshire&...`

### Combined Queries (Multi-Region)
```
https://www.planit.org.uk/api/applics/json?auth=469,468&...
```

Covers West + East Midlands in single call (no wait needed between regions in same query).

## Keyword Searching

### OR Operator
PlanIt supports OR for multiple keywords in single query:

```
search=loft+conversion+or+barn+conversion+or+demolition+or+roof+extension+or+re-roofing+or+listed+building+or+outbuilding
```

URL-encoded: Spaces = `+`, OR = `+or+`

### Application Filtering
Filter by application type using `app_type` field:

```
app_type=HFUL,Full,Heritage,LBC,CLP
```

(Server-side filtering in JSON endpoint)

### Keyword Strategy

**For Bat Surveys (Midlands):**
```
search=loft+conversion+or+barn+conversion+or+demolition+or+roof+extension+or+re-roofing+or+listed+building+or+outbuilding
```
Expected ~40-60 results per week for both regions combined.

**For Mark-Lite Warwickshire:**
```
search=commercial+or+industrial+or+warehouse+or+retail+or+school+or+office+or+residential+development+or+mixed+use+or+extension+or+erection+or+demolition
```

## Pagination & Overflow Handling

### Page Size
```
pg_sz=500
```
Returns up to 500 results per page (max allowed).

### Overflow Detection
If query returns exactly 500 results, there may be more pages:

```
page=2
```

Add `&page=2` to second call. Wait 60+ seconds between calls.

### Fallback: Split Query
If a combined query times out (45-second database timeout), split into parts:

**Option 1: By region (2 calls)**
```
Query 1: auth=469&...
[WAIT 60+ seconds]
Query 2: auth=468&...
```

**Option 2: By keyword (up to 14 calls)**
```
Query 1: search=loft+conversion&...
[WAIT 60+ seconds]
Query 2: search=barn+conversion&...
[etc.]
```

**Option 3: Reduce scope**
- Narrow `recent=` to 7 days instead of 21
- Reduce `pg_sz=` to 250
- Narrow keywords to highest-priority terms

## Field Selection

```
select=uid,description,address,start_date,area_name,url,app_type,agent_company
```

Only request fields you need. Reduces response size and API load.

### Commonly Used Fields

| Field | Format | Use |
|---|---|---|
| uid | String | Application unique ID / reference number |
| description | Text | Full planning description (search-matched against keyword) |
| address | String | Property address |
| start_date | ISO 8601 | Application submission date |
| area_name | String | Local authority name |
| url | URL | Link to planning portal |
| app_type | Code | Application type (HFUL, Full, Heritage, etc.) |
| agent_company | String | Architect/planning consultant firm name (nullable) |

### Special Field Syntax for Agent Data
```
select=uid,description,address,...,ac:other_fields->agent_company
```

Use `ac:` prefix to access nested `other_fields` object. Returns contact company name if available (may be null).

## Rate Limiting

### Hard Limit
- **1 request per minute** — Strictly enforced
- Wait at least 60 seconds between API calls to different regions/queries

### Lockout
- Exceed 1/min: HTTP 429 "Too Many Requests"
- Lockout period: Up to 380 seconds
- Recovery: Wait the specified time; cannot make new requests until lockout expires

### Browser vs. Direct API
- **Browser-based (GeoRSS):** Does NOT trigger 429 (PlanIt treats browser traffic differently)
- **Direct curl/requests (JSON):** Triggers 429 if rate limit exceeded

**Recommendation:** Use browser for all PlanIt API calls (parse XML or fetch JSON via browser DOM).

## Application Type Codes

### Include
- **HFUL** — Householder Full Planning
- **Full** — Full Planning Permission
- **Heritage** / **LBC** — Listed Building Consent
- **CLP** / **CLPD** — Certificate of Lawfulness
- **Amendment** — Planning amendment (if relevant)

### Exclude
- **TCA** / **TPO** / **TDD** — Tree works
- **AOC** / **Conditions** / **DOC** / **DIS** / **Discharge** — **CRITICAL: These are dead leads** (ecology requirements already discharged in original permission)
- **SCR** — Screening opinion (pre-application, too early)
- **ADV** — Advertisement consent
- **TEL** — Telecoms
- **AGR** — Agricultural notification

## Data Quality Notes

### Common Issues

1. **Missing agent_company** — 65% of domestic applications have no agent (self-submitted)
2. **Incomplete descriptions** — Some councils provide minimal text; requires council portal visit for full details
3. **Stale applications** — Published date may be 1-2 weeks before PlanIt indexes; follow portal URL for true application date
4. **Duplicate applications** — Some projects submit both Full Planning + Listed Building Consent as linked applications; deduplicate by address + description match

### Validation Steps

After pulling from PlanIt:
1. Visit council portal URL to verify application still active (not withdrawn)
2. Cross-check `agent_company` field if null (may need council portal visit or web search)
3. Filter out non-residential (schools, churches, commercial warehouses) unless trade-relevant

## Example Queries

### Bat Surveys (Weekly)
```
https://www.planit.org.uk/api/applics/json?auth=469,468&recent=7&search=loft+conversion+or+barn+conversion+or+demolition+or+roof+extension+or+re-roofing+or+listed+building+or+outbuilding&pg_sz=500&select=uid,description,address,start_date,area_name,url,app_type,agent_company
```

Expected result: 40-60 applications across both regions

### Hawks Scaffolding (Weekly)
```
https://www.planit.org.uk/api/applics/georss?auth=Warwickshire&recent=14&sort=-start_date&pg_sz=50
```

Then filter by keyword (commercial, industrial, warehouse, multi-storey, facade)

### Mercia Flooring (Not Applicable)
Mercia uses DfE GIAS data (schools), not planning applications.

## Integration in Mark Skills

### Weekly Lead Finding Skills
- Load PlanIt via browser tool (avoid 429)
- Parse GeoRSS XML or JSON response
- Filter by application type + keywords
- Match application description to lead type (bat survey, scaffolding, brickwork, etc.)
- Extract address, application type, agent company
- Deduplicate against existing Opportunities tab

### Daily Outreach Skills
- Do NOT query PlanIt (already done weekly)
- Use pre-found leads from Opportunities tab
- Match leads to prospects using trade + size-fit

## Links

- [[mark]] — Lead finding service using PlanIt
- [[mark-lite]] — Direct outreach using PlanIt leads
- [[email-infrastructure]] — Contact enrichment for agent firms found on PlanIt

## Sources

- planit.org.uk API documentation
- /sessions/brave-vigilant-gauss/mnt/Projects--Think Through AI/raw/mark/FULL_PROJECT_CONTEXT.md
- Mark SKILL files (Hawks, Bat Surveys, Mark-Lite Northants weekly lead finding)
