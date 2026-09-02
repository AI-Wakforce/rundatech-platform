# Database Safety and Scalability Policy

## Goals
Keep the database correct, auditable, performant, recoverable and migration-friendly as catalog, pricing, markets and AI workloads grow.

## Safety rules
- Production access is private and least-privileged.
- Applications use scoped roles; privileged service credentials are never used in browser/user flows.
- Foreign keys, NOT NULL, CHECK and UNIQUE constraints enforce invariants whenever practical.
- Critical uniqueness rules are database-enforced, not UI-enforced.
- Use transactions for multi-record invariants.
- Avoid unbounded queries and accidental table scans in request paths.
- Index for actual query patterns and measure before adding speculative indexes.
- Use optimistic concurrency/version checks on high-contention editorial/catalog records.
- Long/background maintenance jobs run outside synchronous public requests.

## Migrations
- Every schema change is version-controlled.
- Prefer expand -> migrate/backfill -> switch -> contract for breaking changes.
- Large backfills are resumable, observable and rate-limited.
- Never couple an irreversible destructive migration to a single application deploy.
- Test migration and rollback/forward-recovery on staging-like data.

## Scaling strategy
Start with one well-managed PostgreSQL primary. Scale vertically and optimize queries/indexes before introducing distributed-database complexity. Add read replicas, partitioning, dedicated analytics/search stores only when measured load justifies them.

Likely partition candidates at scale include append-heavy `price_observations`, `audit_events`, and high-volume job/event history.

## Recovery
- Automated backups + point-in-time recovery where provider supports it.
- Periodic restore tests are mandatory; a backup that has never been restored is unproven.
- Define RPO/RTO per environment and mature them as business criticality increases.
- Maintain portable logical exports for migration/exit scenarios in addition to provider-native backups where appropriate.

## Bot/automation-proofing
Database correctness must not depend on clients behaving well. Enforce permissions, validation, constraints, idempotency and rate controls server-side. Treat crawlers, scripts, imports and AI workers as potentially buggy clients.