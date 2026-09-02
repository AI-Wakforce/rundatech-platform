# Multi-Country and Domain Architecture

## Goal
Operate one RundaTech platform across markets without copying the application or product database.

## Core rule
A product has one global internal identity. Country-specific information is attached through market-scoped records.

## Market model
Recommended fields:
- `market_id`
- `country_code` (ISO 3166-1 alpha-2, e.g. `KE`, `UG`, `TZ`)
- `currency_code` (ISO 4217)
- `locale`
- `timezone`
- `status`

Domains are separate records:
- `domain_id`
- `market_id` nullable for global domains
- `hostname`
- `canonical`
- `redirect_policy`
- `status`

Examples:
- `rundatech.co.ke` -> `KE`
- `rundatech.ug` -> `UG`
- `rundatech.co.tz` -> `TZ`
- `rundatech.com` -> global selector or configured default

## What is global
- brand identity
- canonical product/model/variant identity
- technical specifications
- source/evidence records when globally applicable

## What is market-scoped
- retailers
- offers and prices
- currency
- local availability
- affiliate relationships
- warranty/import notes
- localized editorial overrides where needed
- legal notices and market configuration

## Routing
Resolve hostname -> domain registry -> market context. Pass market explicitly through request context; never infer authorization scope only from URL strings.

## SEO/canonicalization
Define canonical and hreflang policy before enabling additional domains. Avoid duplicate market pages that differ only trivially. Localize useful market facts rather than cloning content.

## Expansion rule
Adding a country should primarily be configuration + market data + local integrations. It must not require a fork such as `rundatech-uganda` or duplicated database schemas.