# Identity, RBAC and Account Lifecycle

## User identifiers
Use immutable opaque application identifiers (`user_id`, UUIDv7-style). Emails and usernames are attributes, never identifiers in foreign keys.

## Account states
Recommended state machine:
- `invited`
- `active`
- `suspended`
- `deactivated`
- `pending_deletion`
- `deleted/anonymized` where legally/operationally appropriate

Deactivation revokes sessions and privileged access but preserves required authored records and audit history. Never break historical attribution by deleting referenced user IDs.

## Authentication
- Prefer mature identity provider/auth framework over custom password cryptography.
- MFA required for privileged employees.
- Short-lived sessions/tokens where practical; rotate refresh credentials.
- Service accounts are separate principals from humans.

## Authorization model
Use RBAC for role assignment plus explicit resource/market scopes where needed.

### Initial roles
- `platform_owner`
- `platform_admin`
- `security_admin`
- `engineering_admin`
- `catalog_manager`
- `product_editor`
- `product_reviewer`
- `pricing_manager`
- `pricing_operator`
- `content_manager`
- `content_editor`
- `support_agent`
- `analyst`
- `auditor`

## Separation of duties
High-risk actions should support dual control later. Examples: assigning admin role, changing payment/affiliate settlement destinations, destroying data, changing security policies, approving high-impact AI automation.

## Permission representation
Prefer capability names such as:
`catalog.product.read`, `catalog.product.edit`, `catalog.product.publish`, `pricing.offer.override`, `iam.role.assign`.
Roles map to permissions; code checks permissions, not hard-coded role names.

## Scope
Permissions may be restricted by market (`KE`, `UG`, `TZ`) and team. Future organization/vendor accounts can use the same principal + role + scope model.