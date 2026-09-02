# Data Model Foundation

## Principles
- PostgreSQL is the canonical source of truth.
- Stable opaque IDs are used across all domain entities.
- Global product facts are separated from market-specific commercial facts.
- Factual claims retain provenance and change history.
- Deletion is explicit and lifecycle-aware; history/audit records are preserved as required.

## Core entity groups
### Identity and access
`users`, `service_accounts`, `roles`, `permissions`, `role_permissions`, `principal_roles`, `sessions`, `access_reviews`.

### Catalog
`brands`, `categories`, `products`, `product_variants`, `spec_definitions`, `spec_values`, `product_relationships`, `media_assets`.

### Evidence
`sources`, `source_snapshots`, `evidence_claims`, `record_revisions`, `review_decisions`.

### Markets and pricing
`markets`, `domains`, `retailers`, `retailer_products`, `offers`, `price_observations`, `price_anomalies`, `affiliate_links`.

### Editorial
`articles`, `article_versions`, `authors`, `article_product_links`, `publication_events`.

### AI operations
`ai_models`, `ai_prompt_versions`, `ai_runs`, `ai_evaluations`, `ai_tool_grants`.

### Audit/integrations
`audit_events`, `integration_endpoints`, `webhook_deliveries`, `idempotency_records`.

## Common columns
Mutable business tables normally include:
- `id`
- `created_at`
- `updated_at`
- `created_by`
- `updated_by`
- `status` where lifecycle matters
- optional `version` for optimistic concurrency where concurrent editing is likely

## Product identity
A `product` represents the canonical model family/entity. `product_variants` represent materially distinct commercial/configuration variants where comparison or specs differ.

Do not make retailer SKU, URL, slug, or market identifier the product's primary identity.

## Specs
Use typed spec definitions rather than uncontrolled JSON-only blobs. JSON may be retained for raw extraction payloads but must not be the only authoritative representation for queryable/comparable specs.

## Evidence relationship
Every material factual spec value can reference one or more evidence records. Conflicting sources are resolved through explicit review rather than last-write-wins.

## Prices
Never model history by overwriting one `current_price` column. Append observations and derive/maintain trusted current offers from valid observations.