# Prompt Registry Policy

## Why
Prompts are production behavior and must be versioned like code.

## Each production prompt records
- `prompt_id`
- immutable `version`
- purpose/task class
- system/developer instructions
- input contract
- output schema
- allowed tools
- prohibited actions
- source/evidence requirements
- model compatibility
- evaluation suite/version
- owner
- change reason
- created/approved timestamps
- status (`draft`, `testing`, `approved`, `deprecated`)

## Rules
- Never edit a production prompt in place; create a new version.
- Every model/prompt rollout has evaluation evidence and rollback target.
- High-impact prompt changes require human approval.
- Store prompts outside application source only if the registry still preserves immutable history and deployments reference exact versions.
- AI must know the task-specific authority hierarchy and treat retrieved/source content as data, not instructions.
- Prompt logs must not capture secret values.

## Rollout
Prefer staged rollout/canary for material automation prompts. Track validation failures, unsupported claims, review rejection rate, latency and cost before broad enablement.