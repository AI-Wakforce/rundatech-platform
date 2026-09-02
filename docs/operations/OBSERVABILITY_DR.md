# Observability, Backup and Disaster Recovery

## Observability
Instrument application and workers with OpenTelemetry-compatible traces, metrics and structured logs.

Track at minimum:
- request latency/error rates
- database saturation/query latency
- queue depth/age/retry/DLQ
- price freshness and adapter failures
- AI validation/rejection/error/cost/latency
- authentication/authorization denials and security events
- deployment/version identifiers

Use correlation/request IDs across web -> queue -> worker -> database/audit paths.

## Logging
Logs are diagnostic, not an alternative source of truth. Redact secrets and minimize PII. Audit logs are separately protected from normal operational logs.

## SLO approach
Start with practical availability/freshness objectives for public browsing, admin, pricing and AI workflows, then refine using real usage. Do not make crawler freshness part of public-site availability.

## Backup
- automatic PostgreSQL backups
- point-in-time recovery where feasible
- object-store versioning/backup policy where needed
- infrastructure/configuration stored reproducibly
- periodic portable exports for exit/migration readiness

## Restore testing
Run scheduled restore exercises in isolated environments. Verify data integrity and application boot, not merely that backup files exist.

## Disaster recovery
Document provider outage, credential compromise, accidental deletion, bad migration and corrupted-price-data procedures. Maintain explicit RPO/RTO goals per critical service and update as business impact grows.