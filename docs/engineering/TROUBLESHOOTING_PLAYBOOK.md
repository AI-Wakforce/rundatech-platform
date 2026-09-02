# Troubleshooting Playbook

## Purpose
Provide a repeatable, evidence-based way for humans and AI agents to diagnose and fix RundaTech issues without random changes or broad rewrites.

## Standard flow
1. **Define the symptom.** What is wrong, who is affected, when did it start, and what should happen instead?
2. **Determine severity and blast radius.** Is it one record, one market, one worker, one integration, or platform-wide?
3. **Reproduce safely.** Prefer local/staging or read-only production observation. Never create destructive test data in production without approval.
4. **Collect evidence.** Gather request/job/trace IDs, logs, metrics, audit events, recent deploys, queue status, dependency/provider status, and relevant DB records.
5. **Localize the failing boundary.** UI, API, authorization, database, queue, worker, adapter, external provider, cache/search, or configuration.
6. **Check recent changes.** Review recent PRs, migrations, feature flags, config changes, secret rotations, and provider changes.
7. **Form one or more explicit hypotheses.** State what evidence would confirm or reject each.
8. **Test the smallest hypothesis first.** Do not change unrelated code while diagnosing.
9. **Mitigate ongoing impact.** Roll back, disable a feature/adapter, pause a queue, revoke a credential, or isolate a worker when appropriate.
10. **Fix the root cause.** Avoid symptom-only patches unless used as an emergency mitigation.
11. **Add regression protection.** Test, validation, alert, invariant, runbook update, or other control that catches recurrence.
12. **Verify recovery.** Validate expected behavior and monitor after the change.
13. **Document the resolution.** Record cause, evidence, fix, verification, and prevention in the troubleshooting knowledge base or incident record.

## No random-change debugging
Do not:
- edit many files hoping an error disappears
- restart the whole platform before collecting useful evidence unless availability/safety requires it
- disable security controls to make an error go away
- mutate production data without preserving audit/provenance
- assume an AI-generated explanation is the root cause without validating evidence
- hide unresolved errors with broad exception catching

## Observability identifiers
Every meaningful request/background operation should support correlation where practical:
```text
request_id
trace_id
job_id
batch_id
actor_id (when authenticated, subject to privacy/logging rules)
```
Workers should propagate relevant IDs across queue boundaries so one operation can be traced end-to-end.

## Component isolation map
Prefer the narrowest recovery lever:
- web/API issue → rollback feature/deployment or disable feature flag
- retailer issue → disable only that retailer adapter
- price processing issue → pause/retry only the affected queue/worker
- AI provider issue → disable/switch only AI workflow; browsing remains available
- bad import → quarantine/unpublish affected batch
- compromised credential → revoke/rotate only affected principal/secret
- search/index issue → rebuild index without changing canonical product data

## Data issue workflow
For incorrect product/price/content data:
1. identify record and source evidence
2. inspect revision/audit history
3. determine whether source, extraction, normalization, validation, or manual edit caused the error
4. correct using the approved record-correction process
5. preserve previous value and provenance
6. re-run affected derived outputs/indexes
7. add validation or test if systemic

## Security issue workflow
If compromise is plausible: prioritize containment and evidence preservation over normal debugging. Follow `docs/operations/INCIDENT_RUNBOOK.md` and `docs/security/SECURITY_BASELINE.md`. Rotate/revoke credentials when appropriate and do not erase relevant logs.

## Definition of resolved
An issue is resolved only when:
- user/system behavior is restored
- root/contributing cause is understood to reasonable confidence
- fix or mitigation is verified
- security/data integrity impact is assessed
- regression protection is added where feasible
- resolution is documented for recurrence.