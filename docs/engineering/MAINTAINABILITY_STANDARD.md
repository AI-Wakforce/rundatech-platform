# Maintainability Standard

## Purpose
RundaTech must remain understandable and changeable by a small team, future employees, and AI coding agents without requiring knowledge of the entire platform.

## Mandatory principles
1. Prefer simple, boring, portable technology over novelty.
2. Keep business domains modular. A change in pricing should not require unrelated changes in identity, editorial, or catalog modules.
3. Keep domain/business logic separate from HTTP handlers, UI components, persistence, queues, and vendor SDKs.
4. Every external provider must be behind an adapter/interface owned by RundaTech.
5. Avoid duplicated business rules. One rule should have one canonical implementation.
6. Avoid catch-all `utils` modules. Shared code must have a clear domain or technical responsibility.
7. Keep files, functions, classes, and modules small enough to understand in one review. Split by responsibility, not arbitrary line count.
8. New dependencies require a clear need, security/license review, and an exit path when material.
9. Public APIs, events, and module interfaces must use explicit contracts and versioning rules.
10. Database access must follow approved repository/query patterns; do not scatter raw queries throughout the codebase.
11. Critical business behavior requires automated tests. Every non-trivial bug fix should add a regression test where feasible.
12. Prefer backward-compatible migrations and reversible deployments.
13. Use feature flags or staged rollout for high-risk changes.
14. Delete obsolete code deliberately after migrations/rollouts complete; do not accumulate permanent compatibility debris.
15. Every module must have a README describing purpose, ownership, interfaces, dependencies, data owned, operational risks, and common troubleshooting paths.

## Target repository structure
```text
apps/
  web/
  admin/
modules/
  catalog/
  pricing/
  identity/
  editorial/
  markets/
  retailers/
  comparisons/
  search/
  ai/
workers/
  price-fetcher/
  product-ingestion/
  ai-extraction/
  indexing/
packages/
  database/
  auth/
  validation/
  logging/
  events/
  shared-types/
docs/
```

This is a direction, not permission to create empty folders prematurely. Create modules when implementation begins.

## Module quality bar
Each production module should make clear:
- what it owns
- what it does not own
- its public interface
- database tables/data it owns
- events it publishes/consumes
- external systems it integrates with
- permissions required
- failure modes and isolation controls
- tests and how to run them
- operational dashboards/logs
- troubleshooting links

## Change quality bar
Before merging non-trivial work, verify:
- smallest reasonable scope
- no unrelated refactor mixed into the feature
- tests cover changed behavior
- interfaces remain clear
- no duplicate business rule introduced
- observability is sufficient to diagnose failure
- docs/changelog updated
- rollback path exists
- security baseline is satisfied

## AI coding rule
AI agents must optimize for long-term clarity, not merely making the current test pass. Large rewrites, framework swaps, new infrastructure, or cross-module restructuring require explicit architectural approval/ADR.