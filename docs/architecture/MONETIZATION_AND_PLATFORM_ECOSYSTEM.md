# Monetization and Platform Ecosystem Architecture

## Goal
RundaTech must be able to add revenue models, third-party integrations and commercial APIs without rewriting the canonical catalog or coupling business logic to one payment, affiliate, analytics, identity or API-management vendor.

## Principle: monetize capabilities, not the core schema
The canonical product/evidence/pricing database remains the source of truth. Monetization is layered through products, entitlements, subscriptions, metering and partner interfaces. Payment-provider objects must not become canonical RundaTech identities or product IDs.

## Revenue-ready capabilities
The architecture should support, without requiring all of them at launch:
- retailer affiliate/deep-link revenue
- sponsored placements with explicit disclosure and separation from organic ranking
- display/native advertising adapters
- premium consumer features
- retailer/vendor analytics products
- paid data exports and feeds
- commercial API plans
- enterprise/partner contracts
- referral/lead-generation products
- future licensing of normalized datasets where source rights permit

Editorial ranking, evidence status and factual product truth must not silently change because a party pays RundaTech.

## Commercial API foundation
Treat the external API as a product boundary separate from internal APIs.

Recommended entities/capabilities:
- organizations / developer accounts
- applications
- API credentials or OAuth clients
- API products/plans
- entitlements/scopes
- quotas and rate limits
- usage events/metering
- subscriptions/contracts
- billing-customer references
- webhook endpoints and delivery attempts
- API audit/security events

Never store raw API keys when a secure hash/identifier is sufficient. Keys require creation metadata, prefix/identifier, scopes, status, owner, rotation/revocation and last-used information.

## API product requirements
- OpenAPI contract and generated/reference documentation
- stable resource identifiers
- explicit compatibility/versioning policy
- pagination, filtering and deterministic error formats
- idempotency for appropriate writes
- per-app/per-plan quotas and rate limits
- usage analytics and metering
- sandbox/test environment where practical
- self-service key rotation/revocation
- signed/versioned webhooks
- deprecation notices and migration windows
- status/incident communication
- SDKs only after the API contract is stable enough to justify maintenance

A developer portal should eventually support onboarding, documentation, examples, credentials, plan/usage visibility, billing/subscription management and support.

## Integration architecture
All third-party systems use adapters/ports. Core domain modules must not depend on Stripe-, ad-network-, analytics-, CRM-, email-, search-, affiliate-network- or cloud-specific object models.

Example ports:
- `PaymentProvider`
- `BillingProvider`
- `AffiliateNetworkAdapter`
- `AdProvider`
- `AnalyticsSink`
- `CRMAdapter`
- `EmailProvider`
- `SearchProvider`
- `IdentityProvider`
- `WebhookPublisher`
- `ObjectStorageProvider`

Provider-specific IDs live in integration mapping tables/metadata, not as canonical primary keys.

## Event-driven integration boundary
Use a transactional outbox for durable domain events. Consumers may integrate asynchronously with events such as:
- product.published
- product.updated
- offer.observed
- offer.price_changed
- article.published
- api.subscription_changed
- api.usage_recorded

Events are versioned contracts. Consumers must be idempotent. Do not make core catalog writes depend synchronously on optional marketing/analytics/CRM systems.

## Monetization data separation
Keep commercial data separate from factual catalog truth. Suggested domains:
- `commercial`: campaigns, placements, affiliate mappings, disclosures
- `billing`: customers, subscriptions, plans, invoices/provider references
- `developer_platform`: apps, credentials, entitlements, quotas, usage

This separation allows monetization providers to change without contaminating catalog data.

## Usage metering
Meter commercial API use at a stable gateway/service boundary. Usage events should capture at least principal/app, API product, operation, timestamp, quantity, outcome and correlation ID. Billing aggregation is derived from immutable/raw usage records where practical.

Protect against duplicate charging with idempotency/deduplication. Billing adjustments must be auditable.

## Integration security
- least-privilege credentials per provider/environment
- signed webhook verification and replay protection
- outbound destination allowlists where applicable
- secrets in managed secret storage
- provider-specific rate limits/circuit breakers
- audit trail for credential/plan/entitlement changes
- tenant/object-level authorization
- no privileged service credential in browser code

## Portability
RundaTech must be able to replace an integration provider by implementing a new adapter and migrating mapping/configuration data. A provider change should not require rewriting catalog, pricing, editorial or identity domain logic.

## Build order
Do not build a full billing/API marketplace during the catalog MVP. Build the seams now:
1. stable IDs and canonical domain model
2. adapter interfaces and integration mappings
3. outbox/events
4. organization/service-principal model
5. API contracts/security/quotas
6. usage metering
7. developer portal
8. billing/monetization plans when demand exists

## Commercial integrity
Sponsored content and paid placement must be identifiable. Organic comparison/ranking logic should have documented rules independent of commercial payments. Data licensing must respect source licenses, contracts, privacy requirements and database/content rights.