# Record Correction Policy

## Purpose
Fix inaccurate data without silently rewriting history or allowing automation to corrupt trusted facts.

## Workflow
1. Detect an issue through user report, employee review, automated conflict detection or source refresh.
2. Create a proposed revision containing target record/field, current value, proposed value, evidence, actor, reason and timestamp.
3. Validate type/schema/range and check source quality/conflicts.
4. Low-risk mechanical corrections may follow configured approval rules; material technical facts, merges, identity changes and contentious values require reviewer approval.
5. Apply through the application/domain service in a transaction—not ad-hoc direct SQL except approved emergency procedure.
6. Persist revision and append audit event linking old/new versions.
7. Recompute dependent comparisons/search/cache/index records asynchronously.
8. Monitor for regression.

## Never
- delete an incorrect value just to hide the mistake when it has been published materially
- let an AI model silently overwrite a verified fact
- fix duplicate products by deleting IDs that are referenced; use an explicit merge/redirect process
- edit historical price observations to make a chart look cleaner; flag/invalidate anomalous observations with reasons

## Emergency correction
Security/legal-critical content may be unpublished immediately by authorized staff, then documented/reviewed afterward. The emergency action itself is audited.

## Merge policy
When duplicate canonical entities are merged, designate a surviving ID and maintain redirects/aliases from retired identifiers where feasible. Record who merged them, why and which evidence supported the decision.