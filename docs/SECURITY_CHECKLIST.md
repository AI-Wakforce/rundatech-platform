# Security Checklist

This is the implementation/review checklist. The binding requirements live in [`docs/security/SECURITY_BASELINE.md`](security/SECURITY_BASELINE.md). A checked box does not override or replace a baseline control.

## Secrets and credentials
- [ ] no secret API keys, tokens, private keys, service-role DB credentials, or signing secrets in Git, prompts, logs, screenshots, docs, container images, or frontend bundles
- [ ] production secrets injected at runtime from approved secret storage
- [ ] browser receives only explicitly public/anonymous configuration and DB credentials
- [ ] secret scanning enabled in repository/CI where available
- [ ] exposed secrets are revoked/rotated before Git cleanup
- [ ] development, staging, and production credentials separated
- [ ] secrets inventory, owners, and rotation process documented

## Identity and sessions
- [ ] mature auth provider/framework used instead of custom password crypto
- [ ] if passwords are stored directly, use modern salted password hashing (prefer Argon2id)
- [ ] MFA required for privileged staff
- [ ] no shared human accounts
- [ ] immutable `user_id`
- [ ] service accounts separate from humans
- [ ] login, reset, recovery, and MFA endpoints rate-limited
- [ ] bot/abuse protection applied to authentication and other high-risk flows
- [ ] session cookies use `HttpOnly`, `Secure`, and appropriate `SameSite`
- [ ] sessions rotate/revoke on privilege changes, deactivation, and relevant security events

## Authorization and records
- [ ] least privilege and default deny
- [ ] server-side authorization on every protected action
- [ ] object-level authorization on resources addressed by ID
- [ ] function/capability authorization for privileged actions
- [ ] market/team/resource scopes enforced server-side
- [ ] RLS enabled for client-facing database API tables unless an approved ADR documents an exception
- [ ] protected fields cannot be client-tampered; write DTOs/input allowlists are explicit
- [ ] deactivation revokes access without destroying attribution/audit history

## Database
- [ ] parameterized queries/prepared statements/safe ORM usage; no untrusted SQL concatenation
- [ ] runtime application/worker roles are not DB owner/superuser
- [ ] private network/access controls where supported
- [ ] critical invariants enforced with constraints where practical
- [ ] database connections encrypted
- [ ] sensitive data encrypted at rest and field-encrypted where classification requires it
- [ ] privileged/material changes audited
- [ ] schema migrations reviewed and rollback/restore considered
- [ ] no silent factual record repair; evidence/provenance preserved

## Input and API output
- [ ] all server-side trust boundaries use explicit schema/input validation
- [ ] webhook payloads validated and signatures verified where available
- [ ] user-controlled output contextually escaped
- [ ] rich HTML/markup sanitized using allowlists
- [ ] APIs use response DTOs/allowlists instead of serializing whole DB/ORM records
- [ ] secrets, internal flags, private notes, unnecessary PII, and privileged fields excluded from API responses
- [ ] production error responses do not expose stack traces, SQL, credentials, or infrastructure internals

## File uploads
- [ ] upload file types explicitly allowlisted
- [ ] size, MIME/signature, filename, and application limits validated
- [ ] uploads stored outside executable/static application roots
- [ ] higher-risk uploads quarantined/scanned before use
- [ ] image/document parsing runs with resource limits and isolated workers where appropriate

## Browser and transport
- [ ] HTTPS forced in production
- [ ] HSTS enabled after domain behavior is validated
- [ ] approved security headers configured, including CSP where appropriate
- [ ] CSRF protections applied to cookie-authenticated state changes
- [ ] CORS explicitly restricts trusted origins; no credentialed wildcard origins
- [ ] no debug/admin endpoints exposed publicly

## API, bot, and integration abuse
- [ ] route-appropriate API rate limits defined
- [ ] tighter quotas/concurrency controls on expensive AI, crawl, search, export, import, and admin operations
- [ ] layered bot protection using CDN/WAF/rate/velocity/risk controls where appropriate
- [ ] challenges/CAPTCHA selective/risk-based where practical
- [ ] account/sensitive-object enumeration minimized
- [ ] idempotency used for retryable side effects where duplicates are harmful
- [ ] webhook replay controls where supported
- [ ] SSRF controls on crawlers, price fetchers, URL importers, AI tools, and other outbound fetchers

## Dependencies and supply chain
- [ ] dependency vulnerability scanning runs in CI and on a schedule
- [ ] lockfiles committed where ecosystem supports them
- [ ] lint/tests/secret scanning/security checks run in CI
- [ ] production container images use maintained minimal bases where practical
- [ ] container images scanned for known vulnerabilities
- [ ] deployment credentials isolated from untrusted pull-request code
- [ ] protected-branch/review controls enabled as the team grows

## AI and automation
- [ ] AI output treated as untrusted
- [ ] prompt injection controls in place for crawled/user/file content
- [ ] AI tools have bounded least-privilege permissions
- [ ] AI/automation has no unrestricted production DB/admin credential
- [ ] evidence required for factual publication
- [ ] structured AI output schema-validated before persistence
- [ ] destructive production actions require human approval unless separately approved bounded automation exists
- [ ] external AI receives no secrets, raw auth tokens, unnecessary PII, or private employee data
- [ ] evals performed before production prompt/model changes

## Operations and infrastructure
- [ ] risky/background workloads isolated from user request process
- [ ] worker/container CPU, memory, timeout, retry, and concurrency limits configured
- [ ] development/staging/production environments and credentials separated
- [ ] structured redacted logs and traces
- [ ] OpenTelemetry-compatible monitoring
- [ ] security/admin/auth abuse events detectable and alertable
- [ ] database backups + point-in-time recovery where feasible
- [ ] restore drills performed periodically
- [ ] incident and break-glass procedures documented

## Release gate
A release must not knowingly ship with:
- [ ] committed or browser-exposed secrets
- [ ] unparameterized SQL using untrusted input
- [ ] missing server-side authorization on protected operations
- [ ] privileged service/database credentials exposed to clients
- [ ] unrestricted file uploads
- [ ] known critical dependency vulnerabilities without documented mitigation/exception
- [ ] public production HTTP where HTTPS is expected
- [ ] AI/worker credentials with unnecessary production-wide privileges

This checklist is a baseline verification aid, not a substitute for threat modeling, testing, or periodic security review.