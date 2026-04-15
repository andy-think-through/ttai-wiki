# Knowledge Assistant

> RAG-based self-hosted chatbot for internal staff knowledge. Exploring commercial viability and product-market fit.
> Last updated: 2026-04-08

## Content

**Knowledge Assistant** is a productised offering under exploration: a self-hosted RAG (Retrieval-Augmented Generation) chatbot that gives staff instant, searchable access to organisational knowledge without lengthy training onboarding.

### Use Case

Small to medium teams (10-50 people) with scattered institutional knowledge across documents, wikis, emails, and people's heads. The chatbot learns from uploaded knowledge base and answers staff questions in natural language.

Example target: [[tonic-health]] (small supplement brand with rapidly growing team), [[poweron-uk]] (larger, document-heavy operations).

### Technical Approach

**Platform selection depends on scale:**

- **AnythingLLM** — Recommended for v1 and small teams. Self-hosted, open-source, lower setup complexity, good for MVP and POC.
- **Onyx** — Better for larger or document-heavy clients that need advanced security, complex permission models, and enterprise integration.

### Commercial Model

- **One-time setup:** £500-£1,000 (covers deployment, knowledge base ingestion, team training)
- **Monthly retainer:** £150-£300 (ongoing maintenance, retraining on new documents, performance tuning)
- **Client cost:** Client pays own API costs directly to LLM provider (OpenAI, Anthropic, etc.)

This separates platform/hosting cost (Andy) from model inference cost (client).

### Status

**Exploring, not yet live.** No production clients, but testing approach with small-team targets. Viability depends on:
- Ease of knowledge base migration and ingestion
- Quality of RAG retrieval on unstructured company documents
- Client willingness to adopt chat interface vs traditional search/wiki
- Ability to maintain and tune RAG performance over time

## Links

- [[consulting]] — primary service
- [[mark]] — productised sales agent
- [[hike-ses]] — strategy documents
- [[tonic-health]] — prospect with ideal use case (growing team)

## Sources

- raw/ttai/claude.md
- raw/ttai/TTAI_Project_Context.md
