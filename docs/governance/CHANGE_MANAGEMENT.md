# Change Management

## Principle
Every material change should be understandable by a future engineer or AI agent without relying on institutional memory.

## Required documentation
Non-trivial changes should include, as applicable:
- purpose and scope
- files/modules affected
- schema/API/event/prompt changes
- security/privacy impact
- rollout plan
- rollback/forward recovery
- tests/evidence
- monitoring changes
- changelog entry
- ADR when architecture or long-lived policy changes

## ADR trigger
Create/update an ADR when changing a durable architectural choice such as database technology, auth approach, service boundaries, queue/event system, canonical identity model, domain routing, storage, AI provider abstraction, or major security control.

## No silent policy drift
If implementation intentionally differs from documented policy, either update the policy/ADR through review or treat the implementation as non-compliant technical debt with an owner.