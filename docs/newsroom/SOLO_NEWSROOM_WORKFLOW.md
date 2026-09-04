# Solo Newsroom Workflow

RundaTech should be operable by one person without requiring continuous manual monitoring of dozens of websites.

## Daily operating loop
1. News Radar ingests approved sources and clusters duplicates.
2. Dashboard ranks candidates by urgency, relevance, confidence, and source quality.
3. Editor opens a candidate and sees primary sources, extracted claims, contradictions, related RundaTech products/companies, and prior coverage.
4. AI prepares a structured draft and suggested headline/metadata.
5. Editor verifies material claims, edits framing/context, checks image rights, and approves publication.
6. CMS publishes the article and generates platform-specific social variants.
7. Editor approves/schedules the social bundle.
8. Distribution adapters publish; failures are isolated and retryable.
9. Analytics and correction signals feed back into the dashboard.

## Time-saving defaults
- Reuse verified structured product/company facts rather than rewriting specs manually.
- Prefer reusable article templates for launches, funding, regulation, product announcements, and breaking briefs.
- Auto-suggest internal links, comparison pages, related products, prior stories, and market context.
- Generate a branded RundaTech visual card when no rights-cleared image exists.
- Keep drafts and social content in a review queue rather than forcing immediate publication.

## Recommended cadence
The system should support a small number of high-value stories rather than maximizing article volume. Breaking briefs can be short when verified; deeper analysis should be reserved for stories where RundaTech adds original context, data, interviews, testing, or interpretation.

## Guardrails
Speed never overrides evidence requirements. AI must not invent missing facts, quotes, sources, or image rights. High-risk stories remain human-approved.