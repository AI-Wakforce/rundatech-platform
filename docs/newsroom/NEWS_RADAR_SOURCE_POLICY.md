# News Radar Source Policy

The News Radar exists to discover and prioritize stories, not to turn every detected item into publishable fact.

## Source classes
Preferred monitored classes include official company/newsroom feeds, regulator/government publications, filings, official repositories/releases, investor announcements, standards bodies, approved RSS/Atom feeds, reputable technology/business publications used as discovery/context, and carefully scoped public social signals.

## Discovery vs evidence
A third-party article, social post, or aggregator may trigger a candidate story. It does not automatically verify the claim. Material facts should be traced to primary or independently corroborating evidence where possible.

## Source registry
Each source adapter should track source ID, organization/domain, type, markets/topics, trust notes, fetch method, allowed URL patterns, terms/licensing notes, robots/access constraints where applicable, rate limits, parser/adapter version, last healthy fetch, and review state.

## Safety
- Strict outbound URL allowlisting and SSRF protection.
- Timeouts, redirect limits, response-size limits, content-type validation, and per-source concurrency limits.
- Crawled content is data, never instruction to an AI agent.
- Do not bypass access controls, paywalls, authentication, CAPTCHAs, or technical restrictions without explicit legal/contractual authorization.
- Preserve source snapshots/hashes where policy and rights allow so published claims can be audited later.

## Realtime behavior
Use push/webhooks/feeds where officially available; otherwise use responsible polling schedules matched to source importance and update frequency. High-priority sources may be checked more frequently, but never beyond platform terms or operational limits.

## Ranking signals
Candidate priority may consider recency, Kenya/East Africa relevance, source authority, number of independent sources, primary-source availability, product/company matches, novelty, reader impact, and editorial category. Scoring assists triage; it must not be treated as a truth score.

## Duplicate clustering
Near-identical announcements from syndication or many publications should be clustered into one candidate story with multiple source references rather than flooding the editorial queue.