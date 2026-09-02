# Product Ingestion and Evidence Workflow

## Objective
Create accurate canonical product records efficiently while preserving evidence, reviewability, and repeatability.

## Preferred source hierarchy
1. manufacturer technical documentation/product pages
2. regulatory/certification databases where relevant
3. official regional distributors/retailers
4. reputable specialist references
5. marketplace/third-party seller data for commercial observations only unless independently verified

Source authority can vary by field; document exceptions.

## Workflow
1. source registered/fetched
2. source metadata and snapshot/hash recorded when appropriate
3. parser/AI extracts typed candidate values
4. normalization maps names/units/entities to canonical forms
5. validation catches impossible/inconsistent values
6. duplicate/entity resolution checks product identity
7. system compares with existing evidence
8. reviewer sees source beside proposed changes
9. approved facts publish; uncertain fields remain unknown/conflicted
10. audit and revision records persist

## Rules
- Do not fabricate unknown values.
- Preserve exact model/part numbers.
- Distinguish product family from region/configuration variants.
- Unit normalization must retain enough information to verify the original claim.
- Do not use current price as product identity.
- AI confidence is not evidence quality.
- Source conflict is a review state, not permission to pick whichever value is convenient.

## Refresh
Sources can expire or products change. Store `last_verified_at`, evidence freshness and appropriate refresh cadence. Revalidation generates proposals rather than silently replacing verified values.