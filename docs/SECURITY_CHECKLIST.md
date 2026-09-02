# Security Checklist

## Identity and access
- MFA for privileged staff
- no shared human accounts
- immutable `user_id`
- service accounts separate from humans
- least privilege and default deny
- market/resource scopes enforced server-side
- deactivation revokes sessions and access without destroying attribution

## Secrets
- no secrets in Git, prompts, logs, screenshots or frontend bundles
- separate environment credentials
- runtime secret injection
- rotation and ownership inventory
- webhook signature verification

## Application/API
- object-level and function-level authorization
- schema/input validation
- rate limiting for abuse-prone and costly routes
- CSRF/session protections appropriate to auth design
- SSRF controls on outbound fetchers
- secure headers and dependency scanning
- no debug/admin endpoints exposed publicly

## Database
- private network/access controls
- scoped application roles
- constraints for critical invariants
- RLS where useful as defense-in-depth
- audited privileged changes
- migration review and restore testing

## AI and automation
- AI output treated as untrusted
- prompt injection controls
- bounded tool permissions
- no unrestricted production DB credentials
- evidence required for factual publication
- evals before production prompt/model changes

## Operations
- structured redacted logs
- OpenTelemetry-compatible monitoring
- alerts on auth abuse, queue failures, price freshness and unusual admin actions
- backup + point-in-time recovery where feasible
- restore drills
- incident and break-glass procedures

This checklist is a baseline, not a substitute for threat modeling or periodic security review.