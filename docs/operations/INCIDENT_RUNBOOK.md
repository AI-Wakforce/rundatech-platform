# Incident Runbook

## Severity
Define severity from user/business/security impact, not from how interesting the technical failure appears.

Suggested baseline:
- `SEV-1`: major outage, active compromise, destructive/corrupting production event
- `SEV-2`: serious degradation, important workflow unavailable, contained security incident
- `SEV-3`: limited degradation with workaround
- `SEV-4`: minor operational issue

## Initial response
1. confirm impact and scope
2. assign incident lead
3. stop ongoing damage where safe
4. preserve evidence/logs/audit data
5. communicate status internally
6. rollback, isolate or disable affected component
7. validate recovery
8. monitor for recurrence

## Isolation levers
- disable one retailer adapter
- pause a queue/worker
- disable a feature flag
- revoke a service credential
- block external egress/domain
- switch AI/provider integration off
- unpublish suspect data batch

Public product browsing should remain available whenever an asynchronous subsystem can be safely isolated.

## After incident
Record timeline, impact, root/contributing causes, corrective actions, owner and due date. Update tests, monitoring, ADR/policy/runbook where the incident exposed a systemic weakness. Avoid blame-oriented retrospectives.