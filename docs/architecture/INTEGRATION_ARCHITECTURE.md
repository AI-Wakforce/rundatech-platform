# Integration Architecture

## Goal
Make external systems easy to add, replace, test and isolate without embedding provider-specific behavior throughout RundaTech.

## Adapter rule
Every external dependency is accessed through a narrow internal interface. Examples: AI providers, retailer feeds, object storage, email, search, analytics, auth providers and payment/affiliate systems.

Core domain code depends on RundaTech contracts, not vendor SDK types.

## API standards
- document HTTP APIs with OpenAPI where practical
- version public/partner contracts explicitly
- validate all input/output schemas at trust boundaries
- enforce authentication and object/function-level authorization server-side
- use idempotency keys on side-effecting operations that may be retried
- define rate limits and quotas for external clients

## Webhooks
- verify signatures and timestamp/replay controls
- persist delivery identity/idempotency state
- acknowledge quickly and process heavy work asynchronously
- retain bounded retry and dead-letter policy

## Events
Internal asynchronous events use stable names and versioned payload schemas. Consumers must tolerate additive compatible changes. Do not treat an event bus as a hidden database.

## Resilience
External failures use timeouts, bounded retry with backoff/jitter, circuit breaking and graceful degradation. An unavailable third party must not cascade into total public-site failure when cached/canonical RundaTech data remains usable.

## Exit strategy
For each material provider, document exported data, replacement interface, credentials/secrets ownership, and provider-specific features that would complicate migration.