# Evidence Baseline

## Principle
RundaTech factual product and pricing claims should be evidence-backed and attributable to a source state.

## Evidence record
Capture, where applicable:
- source URL or external identifier
- source type/authority
- retrieved/observed timestamp
- content hash or snapshot reference
- exact product/model/market context
- extractor/parser version
- factual claim(s) supported
- reviewer/verification status

## Evidence hierarchy
Prefer primary manufacturer documentation for technical specifications and direct retailer/API/feed observations for prices. Secondary sources may supplement missing data but should not silently override stronger evidence.

## Conflicts
When authoritative sources disagree, keep the conflict visible internally, preserve both evidence records and require explicit resolution. Do not use AI confidence as the deciding evidence.

## Freshness
Technical specifications may be effectively stable after verification, while prices, stock and some firmware/software fields need freshness windows. Every freshness-sensitive field should have a documented policy.

## AI
Generated prose can summarize verified evidence but is not itself evidence. AI may identify candidate facts or inconsistencies only through a traceable proposal workflow.