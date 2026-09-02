# RundaTech Master Blueprint — Foundation v0.1

## What we are building
A multi-country, AI-native technology intelligence platform: canonical product/spec database, comparisons, search, price intelligence, editorial content, retailer integrations and future partner APIs.

## Core design decisions
- Modular monolith for core domain + isolated containerized workers.
- PostgreSQL canonical datastore.
- TypeScript for product/web/API application; Python for AI/crawling/data workers; SQL for data constraints/querying.
- Stable UUID-style IDs.
- RBAC permissions + resource/market scopes; MFA for privileged staff.
- Append-only material audit trail.
- Source/evidence provenance per factual claim.
- AI outputs are untrusted proposals until validated according to risk tier.
- Vendor/provider access only through adapters.
- Market/domain configuration separates global product truth from local prices/availability/content.
- OpenTelemetry-compatible observability.
- Versioned migrations, prompts, API/event contracts and ADRs.

## System shape
Public web traffic is isolated from crawling, price, indexing and AI jobs through queues and worker containers. PostgreSQL and object storage are durable infrastructure. A retailer failure or AI outage should not make normal product browsing fail.

## Security posture
Default deny, least privilege, private database, server-side authorization, RLS defense-in-depth where useful, secrets manager/runtime injection, no secret values in Git/logs/prompts, rate limits, SSRF controls, signed webhooks, idempotency, secure audit and tested backups/restores.

## Data quality posture
Every product fact can carry provenance. Corrections use proposed revisions and reviewer approval for material facts, with history retained. Price observations are append-only historical events from which current prices are derived.

## AI posture
Prompt registry + model registry + evaluation suite + tool permissions + audit. Crawled content is never trusted as instruction. High-risk writes or destructive/privileged actions require humans.

## Regional expansion
`rundatech.co.ke`, `.ug`, `.tz`, `.com` resolve into a `market` configuration. Products retain the same internal IDs. Country-specific offers, retailers, currency, availability and editorial overrides are market-scoped.

## Future employees
Teams receive capability-based access: Platform Engineering, Product Data, Pricing Ops, Editorial, AI/Automation, Security, Commercial, Support and Audit. No shared human accounts; joiner/mover/leaver workflow is mandatory.

## First implementation order
1. repository/CI/container baseline
2. PostgreSQL schemas/migrations
3. authentication + user lifecycle
4. permissions/RBAC + audit
5. canonical catalog/evidence model
6. admin review/correction workflow
7. public product pages/search
8. comparison engine
9. market/pricing model
10. isolated price fetcher
11. AI gateway/prompt registry/evals
12. regional domains and later partner APIs