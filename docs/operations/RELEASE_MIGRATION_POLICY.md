# Release and Migration Policy

## Environments
Maintain separate development, staging and production environments with isolated credentials and data boundaries.

## Releases
- changes enter through reviewed pull requests
- automated tests/lint/type/security checks run before merge
- production deploys identify exact commit/version
- feature flags are preferred for risky incremental rollout
- rollback/forward-fix path is documented before high-risk changes

## Database migrations
- migrations are immutable once applied to shared environments
- use backward-compatible expand/contract patterns for breaking schema changes
- test migrations against realistic staging data
- large backfills are separate resumable jobs
- destructive operations require explicit review and recovery plan

## Configuration
Environment-specific configuration is externalized. Secret values never live in repository configuration files.

## Portability
Avoid release processes that can only be recreated manually in one provider dashboard. Important deployment and infrastructure state should be reproducible through versioned configuration/IaC as the platform matures.

## Emergency changes
Emergency fixes are allowed only through an audited break-glass procedure and must be followed by documentation, review and normalization back into the standard delivery path.