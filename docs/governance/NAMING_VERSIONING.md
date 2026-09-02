# Naming and Versioning

## IDs
Use stable opaque internal IDs. Human-readable slugs are mutable routing aliases, not primary identities.

## Naming
- database tables/columns: `snake_case`
- TypeScript/Python domain concepts: language-standard conventions
- permission keys: dot-delimited capabilities, e.g. `catalog.product.publish`
- events: stable domain names with versioned payload schemas
- environment variables: uppercase names with explicit scope/purpose

## Versions
Version independently where needed:
- application releases
- database migrations
- public/partner API contracts
- event/webhook schemas
- production prompts
- AI evaluation suites
- retailer adapter/parser versions

Do not force unrelated domains into one global version number.

## Deprecation
Breaking public/integration contract changes require a documented migration/deprecation window. Internal changes should remain backward-compatible across rolling deploys whenever practical.