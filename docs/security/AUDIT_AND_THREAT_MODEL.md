# Audit, Security Events and Threat Model

## Audit events
Material administrative and automated mutations generate an append-only audit event containing:
- `audit_event_id`
- timestamp
- actor type (`user`, `service`, `ai_agent`, `system`)
- actor ID
- action
- target type + target ID
- market/tenant scope
- request/correlation ID
- before/after summary or version references
- reason/ticket/change ID when required
- IP/device metadata where appropriate and lawful
- result (`success`, `denied`, `failed`)

Audit tables are not editable through normal admin UI. Retention is defined separately from operational logs.

## Key threats to design against
- broken object/function authorization
- credential theft/session abuse
- automated scraping/resource exhaustion
- retailer/source SSRF
- malicious or poisoned source content
- prompt injection against AI agents
- unsafe AI-generated database writes
- supply-chain dependencies
- exposed admin/debug endpoints
- mass assignment/over-posting
- price manipulation and source spoofing
- duplicate/replayed webhooks/jobs
- compromised employee account
- accidental destructive migrations

## Controls
Server-side authorization, RLS where appropriate, schema validation, allowlisted fetch policies, egress controls, rate limits, WAF/CDN protections, dependency scanning, signed webhooks, idempotency, immutable audit, backups, MFA, least privilege and peer review.