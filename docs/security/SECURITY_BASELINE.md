# RundaTech Security Baseline v1

This document defines mandatory minimum security controls for all RundaTech production systems, services, workers, APIs, databases, admin tools, AI workflows, and integrations.

Normative language:
- **MUST / MUST NOT** = mandatory unless an approved ADR documents an exception, owner, risk, and expiry/review date.
- **SHOULD / SHOULD NOT** = expected default; exceptions require documented rationale.
- **MAY** = optional.

Security controls must be implemented as close as possible to the trust boundary and must not rely on UI-only restrictions.

## 1. Secrets and credentials

### SEC-SECRETS-001 — Hide secret API keys
Secret API keys, service-role database credentials, signing keys, OAuth client secrets, deployment tokens, webhook secrets, and encryption keys MUST NOT be exposed to browsers, mobile clients, public bundles, repositories, logs, traces, prompts, screenshots, tickets, or documentation.

### SEC-SECRETS-002 — Managed secret storage
Production secrets MUST be supplied at runtime by an approved secret manager or deployment platform secret facility. Secrets MUST NOT be hard-coded in source files or container images.

### SEC-SECRETS-003 — Public vs privileged database keys
Client applications MAY receive only credentials explicitly designed to be public/anonymous. Privileged database/service credentials MUST remain server-side and MUST NOT be used to bypass user authorization in normal user flows.

### SEC-SECRETS-004 — Secret scanning and purge procedure
The repository MUST enable secret scanning where available and CI MUST scan commits for known credential patterns. If a secret is committed, it MUST be treated as compromised: revoke/rotate first, then remove it from current code and, where necessary, rewrite Git history following an approved incident procedure.

### SEC-SECRETS-005 — Least privilege and rotation
Every service receives only the credentials required for its purpose. Development, staging, and production credentials MUST be separated. Rotation ownership and cadence MUST be documented.

## 2. Authentication and sessions

### SEC-AUTH-001 — Mature authentication
RundaTech SHOULD use a mature identity provider or proven authentication framework rather than custom authentication cryptography.

### SEC-AUTH-002 — Password storage
If RundaTech ever stores passwords directly, passwords MUST be salted and hashed with a modern password-hashing algorithm such as Argon2id. Plaintext passwords or reversible password encryption are prohibited.

### SEC-AUTH-003 — Login rate limiting
Login, password reset, account recovery, MFA verification, and other authentication endpoints MUST implement rate limiting and abuse controls by appropriate combinations of account, IP, device/session, and velocity signals. Controls SHOULD escalate rather than permanently locking legitimate users after a small number of attempts.

### SEC-AUTH-004 — Bot protection
Public authentication, registration, password-reset, scraping-sensitive, form-submission, and expensive AI/API endpoints MUST have layered bot/abuse protection. Challenges/CAPTCHA SHOULD be risk-triggered rather than imposed on every normal visitor where practical.

### SEC-AUTH-005 — Secure session cookies
Cookie-based sessions MUST use `HttpOnly`, `Secure`, and an appropriate `SameSite` policy. Session identifiers MUST be unpredictable, rotated after authentication or privilege changes, expire appropriately, and be revoked on deactivation or security-sensitive account changes.

### SEC-AUTH-006 — MFA
MFA MUST be required for privileged employee/admin accounts and SHOULD be available for all accounts where relevant.

### SEC-AUTH-007 — Account lifecycle
Suspension/deactivation MUST revoke active sessions and privileged access without destroying required audit attribution or authored records.

## 3. Authorization and record access

### SEC-AZ-001 — Server-side authorization
Every protected action MUST enforce authorization server-side. Hiding a button or route in the UI is not authorization.

### SEC-AZ-002 — Object-level authorization
Any API or operation addressing a resource by ID MUST verify that the acting principal is permitted to access that specific object.

### SEC-AZ-003 — Function-level authorization
Privileged operations MUST require explicit permissions/capabilities, not merely successful authentication.

### SEC-AZ-004 — Record locking and scopes
Access to market-, team-, tenant-, user-, or role-scoped records MUST be enforced using server-side authorization and, where appropriate, PostgreSQL Row-Level Security.

### SEC-AZ-005 — Mandatory RLS boundary
RLS MUST be enabled for tables directly exposed through client-facing database APIs unless an approved ADR explicitly documents why it is unnecessary. RLS is defense-in-depth and does not replace application authorization.

### SEC-AZ-006 — Block field/property tampering
Write endpoints MUST use explicit input schemas/DTO allowlists. Clients MUST NOT be allowed to set protected fields such as ownership, approval status, audit fields, privileged roles, verification flags, publisher identity, trust scores, or system-generated state unless the operation explicitly authorizes it.

### SEC-AZ-007 — Default deny
Privileged permissions and sensitive records MUST default to deny unless access is explicitly granted.

## 4. Database and query security

### SEC-DB-001 — Parameterized queries
Application code MUST use parameterized queries, prepared statements, or a safe ORM/query builder. Concatenating untrusted input into SQL is prohibited.

### SEC-DB-002 — Database least privilege
Application, worker, migration, analytics, and admin roles SHOULD be separate. Runtime services MUST NOT use database owner/superuser credentials for ordinary operations.

### SEC-DB-003 — Critical constraints
Critical business invariants SHOULD be enforced with database constraints where possible, not only application validation.

### SEC-DB-004 — Encryption
Production database connections MUST use encrypted transport. Sensitive data MUST be encrypted at rest using provider/platform controls, with application/field-level encryption for data whose risk classification requires it.

### SEC-DB-005 — Auditability
Privileged or material data changes MUST produce attributable audit events. Audit records MUST NOT be silently altered or deleted by ordinary application roles.

### SEC-DB-006 — No silent record repair
Production factual records MUST NOT be silently overwritten to “fix” data. Material corrections MUST follow the record-correction and evidence policies and preserve provenance/history.

## 5. Input, output, and content safety

### SEC-INPUT-001 — Validate all input
All external input MUST be validated at the server-side trust boundary using explicit schemas, including API bodies, query parameters, route parameters, headers used by business logic, webhooks, imported files, crawled data, and AI structured output.

### SEC-INPUT-002 — Normalize safely
Normalization MUST occur after validation rules are understood and MUST NOT convert invalid or ambiguous input into silently trusted data.

### SEC-OUTPUT-001 — Escape user content
User-controlled content MUST be contextually encoded/escaped at output. Rich HTML/markup, where allowed, MUST be sanitized with an allowlist-based sanitizer before rendering.

### SEC-OUTPUT-002 — Trim API responses
APIs MUST return explicit response DTOs/allowlists and MUST NOT serialize entire database rows or ORM entities directly to clients. Internal flags, secrets, credential metadata, private notes, audit internals, unnecessary PII, and privileged fields MUST be omitted.

### SEC-OUTPUT-003 — Error handling
Production errors MUST avoid leaking stack traces, credentials, SQL, infrastructure internals, or private payloads to clients.

## 6. File uploads

### SEC-UPLOAD-001 — Restrict upload types
File uploads MUST use an explicit allowlist of permitted formats based on the use case. Extension alone MUST NOT determine trust.

### SEC-UPLOAD-002 — Verify file characteristics
Uploads MUST be checked for size, detected MIME/type/signature where practical, filename safety, and application-specific limits before processing.

### SEC-UPLOAD-003 — Isolate storage
Untrusted uploads SHOULD be stored outside the application executable/static root, preferably in object storage with generated object names and least-privilege access.

### SEC-UPLOAD-004 — Malware/content scanning
Higher-risk uploads SHOULD be quarantined and scanned before becoming accessible or entering downstream processing.

### SEC-UPLOAD-005 — Image/document processing
Image/document parsers MUST run with resource limits and, where practical, isolated worker execution to reduce parser and decompression-bomb risk.

## 7. Browser and transport security

### SEC-WEB-001 — HTTPS only
Production traffic MUST use HTTPS. Plain HTTP MUST redirect to HTTPS where exposed, and internal service transport SHOULD be encrypted when crossing untrusted networks or platform boundaries.

### SEC-WEB-002 — HSTS
Production web domains SHOULD use HSTS after HTTPS deployment and domain/subdomain behavior has been validated.

### SEC-WEB-003 — Security headers
Production web responses MUST define an approved security-header baseline including, as appropriate, Content-Security-Policy, frame-ancestors/X-Frame-Options compatibility handling, X-Content-Type-Options, Referrer-Policy, and Permissions-Policy.

### SEC-WEB-004 — CSRF
State-changing cookie-authenticated operations MUST implement appropriate CSRF defenses.

### SEC-WEB-005 — CORS
CORS MUST use explicit trusted-origin policy. Wildcard origins MUST NOT be combined with credentialed access.

## 8. API and bot/abuse security

### SEC-API-001 — Rate limiting
Public and authenticated APIs MUST define route-appropriate rate limits. Expensive AI, search, compare, import, crawl, export, and admin endpoints require tighter quotas or concurrency controls.

### SEC-API-002 — Enumeration resistance
Authentication/account-recovery and sensitive lookup flows SHOULD avoid unnecessarily revealing whether a specific account or private object exists.

### SEC-API-003 — Idempotency
Side-effecting integration/API operations that may be retried MUST use idempotency controls where duplicate execution could cause harm or inconsistent state.

### SEC-API-004 — Webhook verification
Inbound webhooks MUST verify provider signatures/authenticity where supported and SHOULD implement replay protections using timestamp/event identifiers where available.

### SEC-API-005 — SSRF protection
Price fetchers, URL importers, metadata tools, crawlers, AI agents, and any server-side URL fetch capability MUST validate destinations and block access to private/internal/link-local/metadata networks unless explicitly required and isolated.

### SEC-BOT-001 — Layered protection
Bot defense SHOULD combine CDN/WAF controls, velocity/rate limits, reputation/risk signals, application quotas, and selective challenges. Business-critical public catalog pages SHOULD remain usable by legitimate users and approved search crawlers.

### SEC-BOT-002 — Cost-amplification protection
Endpoints that can trigger AI inference, scraping, exports, indexing, or other expensive work MUST enforce authentication/quotas/budgets appropriate to cost and abuse risk.

## 9. Dependencies, CI/CD, and supply chain

### SEC-SUPPLY-001 — Dependency scanning
Dependencies MUST be automatically scanned in CI and on a scheduled basis using approved vulnerability tooling.

### SEC-SUPPLY-002 — Lockfiles and pinned builds
Application dependency lockfiles MUST be committed where ecosystem tooling supports them. Production builds SHOULD be reproducible and version-pinned enough to prevent unreviewed dependency drift.

### SEC-SUPPLY-003 — Static/security analysis
CI SHOULD run linting, tests, secret scanning, and suitable static/application security checks for changed code.

### SEC-SUPPLY-004 — Container image scanning
Production container images MUST be built from maintained minimal bases where practical and SHOULD be scanned for known vulnerabilities before release.

### SEC-SUPPLY-005 — Protected delivery
Production deployment credentials MUST be isolated from untrusted pull-request code. Branch/review protections SHOULD be enabled for protected branches as the team grows.

## 10. Logs, audits, and sensitive data

### SEC-LOG-001 — Log redaction
Logs, traces, and analytics MUST NOT contain passwords, access tokens, private keys, full secret values, or unnecessarily sensitive request/response payloads.

### SEC-LOG-002 — Security events
The platform SHOULD produce detectable events for suspicious authentication activity, privilege changes, repeated authorization failures, secret/security configuration changes, unusual admin operations, queue failures, and other high-impact behavior.

### SEC-LOG-003 — Immutable attribution
Audit events MUST identify actor/service principal, action, target, timestamp, result, and relevant request/change metadata. Historical attribution MUST survive user deactivation.

## 11. AI, crawlers, and autonomous workers

### SEC-AI-001 — AI output is untrusted
AI output MUST be validated before persistence or execution and MUST NOT be treated as factual evidence by itself.

### SEC-AI-002 — Prompt injection boundary
Content fetched from websites, files, feeds, users, or integrations MUST be treated as untrusted data and MUST NOT override agent system instructions, permissions, or security policy.

### SEC-AI-003 — Tool least privilege
AI agents/workers MUST have bounded tools and credentials. They MUST NOT receive unrestricted production database/admin credentials.

### SEC-AI-004 — Destructive actions
AI MAY propose destructive or privileged production changes but MUST NOT autonomously execute them unless a separately approved policy defines the exact bounded automation and safety controls.

### SEC-AI-005 — Data minimization
Secrets, raw auth tokens, unnecessary PII, confidential employee data, and unrelated commercial data MUST NOT be sent to external AI providers.

## 12. Infrastructure and isolation

### SEC-INFRA-001 — Failure isolation
Price crawling, bulk imports, AI extraction, indexing, uploads processing, and other high-risk/background workloads MUST run outside the user request process with isolated workers/containers where appropriate.

### SEC-INFRA-002 — Resource limits
Workers and containers SHOULD have CPU, memory, timeout, retry, and concurrency limits so one malformed job cannot exhaust the platform.

### SEC-INFRA-003 — Environment separation
Development, staging, and production data, credentials, and infrastructure MUST be separated. Production secrets/data MUST NOT be copied into lower environments without an approved sanitization process.

### SEC-INFRA-004 — Backups and recovery
Critical production databases MUST have automated backups and appropriate point-in-time recovery where supported. Restore procedures MUST be tested periodically.

## 13. Security change governance

### SEC-GOV-001 — Security impact review
Changes affecting authentication, authorization, secrets, external network access, sensitive data, payments/affiliate destinations, AI tool permissions, uploads, or database access MUST include a security-impact note.

### SEC-GOV-002 — Exceptions
Any exception to a MUST control requires an ADR or security exception record identifying the control ID, rationale, risk, compensating controls, owner, approval, and review/expiry date.

### SEC-GOV-003 — Evidence
Security claims SHOULD be evidenced by tests, configuration, CI results, monitoring, or documented operational verification rather than relying on developer/AI assertion alone.

## 14. Minimum release gate

A production release MUST NOT knowingly introduce:
- committed or browser-exposed secrets
- unparameterized SQL with untrusted data
- missing server-side authorization for a protected operation
- direct client access using privileged service credentials
- unrestricted file uploads
- known critical dependency vulnerabilities without documented mitigation/exception
- public production HTTP when HTTPS is expected
- AI/worker credentials with unnecessary production-wide privileges

As implementation matures, these requirements should be mapped to automated CI checks, tests, infrastructure policies, and runtime alerts.