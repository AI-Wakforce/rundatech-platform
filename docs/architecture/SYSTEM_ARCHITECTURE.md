# System Architecture

## Architecture style
Use a **modular monolith for core synchronous product functions** and **isolated worker services** for asynchronous/high-risk workloads.

### Why
This preserves maintainability for a small team while giving failure isolation for crawlers, AI jobs, pricing, bulk imports, indexing and notifications. Modules communicate through explicit interfaces/events so they can be extracted into services later without redesigning domain logic.

## Initial deployable containers
- `web`: public site + API/BFF
- `admin`: internal management interface (may share repository/runtime initially but separate deployment/security surface recommended)
- `worker-ai`: AI extraction/generation/evaluation jobs
- `worker-pricing`: retailer connectors and price observations
- `worker-data`: imports, normalization, reconciliation, indexing tasks
- `scheduler`: enqueues periodic work; contains no core business truth

Durable services:
- PostgreSQL
- Redis-compatible queue/cache/rate-limit layer
- S3-compatible object storage
- search engine only when PostgreSQL search ceases to meet requirements

## Module boundaries
Core domain modules:
- identity/access
- catalog
- taxonomy/spec-schema
- evidence/provenance
- markets/localization
- retailers/offers/pricing
- comparisons
- editorial
- AI operations
- audit
- integrations

Modules do not directly modify another module's private tables without an approved contract.

## Failure isolation rules
- External retailer/AI/provider call failures must degrade gracefully.
- Use queues, bounded retries, exponential backoff, dead-letter handling and circuit breakers.
- Workers have CPU/memory/concurrency limits.
- User-facing requests do not wait on crawlers or long-running AI.
- Each integration exposes health/freshness metrics.
- Retries are idempotent.

## Portability
- Domain logic avoids cloud-provider-specific APIs.
- Persist canonical data in PostgreSQL and S3-compatible formats.
- Wrap AI, auth, email, search, object storage and queue providers behind adapters.
- Infrastructure configuration is reproducible.
- Data exports/restores are tested.

## Evolution path
Split a module into a service only when measurable scale, team ownership, security isolation or availability needs justify operational complexity. Do not use microservices as an organizational aesthetic.