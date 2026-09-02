# Module Design Standard

## Goal
Each RundaTech module should be independently understandable, testable, observable, and replaceable enough that changes stay local.

## Recommended internal shape
Use this only where it improves clarity; do not create ceremony for trivial modules.

```text
module-name/
  domain/          # business rules/entities/value objects
  application/     # use cases/orchestration
  infrastructure/  # DB/provider/queue adapters
  api/             # HTTP/RPC handlers or controllers
  tests/
  README.md
```

## Dependency direction
- Domain code must not depend on web frameworks, database clients, queue SDKs, AI SDKs, or retailer SDKs.
- Application code may depend on domain contracts and abstract ports/interfaces.
- Infrastructure implements ports and may depend on vendor libraries.
- API/UI layers call application use cases rather than embedding business rules.
- Cross-module calls use explicit interfaces/events; do not reach into another module's internal tables/classes casually.

## Data ownership
A module that owns a business concept is the default writer for its canonical data. Other modules should consume through approved interfaces, read models, or events rather than creating a second source of truth.

Cross-module database writes require explicit design review. Reporting/search read models may denormalize data but must be rebuildable from canonical sources.

## Interface rules
- Define typed request/response contracts.
- Validate at trust boundaries.
- Do not leak ORM/database models as public contracts.
- Version externally consumed contracts when breaking changes are unavoidable.
- Use idempotency for retryable side-effecting operations where duplicate execution is harmful.

## External integration rules
Retailers, payment/affiliate providers, AI providers, email systems, object storage, search engines, and similar dependencies must be wrapped in RundaTech-owned adapters. Vendor-specific fields should be normalized at the boundary when practical.

## Background work
Long-running, failure-prone, untrusted, expensive, or retryable tasks belong in dedicated workers/queues where appropriate. Workers must support timeouts, bounded retries, dead-letter/failure handling, idempotency where needed, observability, and safe reprocessing.

## Error handling
- Use typed/domain errors where useful.
- Do not swallow exceptions silently.
- Translate internal failures to safe external error responses.
- Preserve correlation IDs.
- Never expose secrets, stack traces, SQL, internal topology, or sensitive data to public clients.

## Module README template
Every substantial module README should include:
1. Purpose
2. Ownership
3. Responsibilities
4. Non-responsibilities
5. Public interfaces
6. Data/tables owned
7. Events produced/consumed
8. Dependencies/adapters
9. Permissions/security considerations
10. Operational metrics/logs
11. Failure/isolation behavior
12. Local test/run instructions
13. Common troubleshooting links
14. Related ADRs

## Review warning signs
Pause and redesign if a feature requires:
- touching many unrelated modules
- direct writes into several modules' canonical tables
- circular dependencies
- repeated copies of the same rule
- vendor SDK objects leaking across the application
- giant shared utility/service classes
- HTTP handlers with substantial business logic
- one worker/service needing every secret in the platform

These are signals of lost boundaries, not conveniences to normalize.