# RundaTech Newsroom Architecture

RundaTech may operate both as a product-intelligence platform and a technology publication. The newsroom must be designed for a small team/solo operator first, with AI used to reduce repetitive work while preserving human editorial accountability.

## Editorial product
RundaTech News should prioritize technology stories where RundaTech can add distinctive value: Kenya/East Africa technology, consumer technology, AI, startups, fintech, telecoms, cybersecurity, enterprise technology, technology policy, and product launches.

The newsroom should connect to RundaTech's structured catalog, market, pricing, company, and evidence data so news stories can reference products, companies, prices, comparisons, historical context, and prior coverage without duplicating facts.

## Publishing speeds
The CMS should support at least three editorial formats:
- Breaking Brief: fast, concise verified update
- News: fuller context and local relevance
- Analysis/Feature: original reporting, interpretation, datasets, reviews, guides, or deeper analysis

## News Radar
A dedicated asynchronous `news-radar` capability may monitor approved public sources such as official company blogs, press rooms, regulator/government sources, RSS/Atom feeds, GitHub releases, startup/investor announcements, product launch feeds, and reputable publications used as discovery signals.

Flow:
source adapters -> fetch/snapshot -> normalize -> deduplicate/cluster -> classify -> importance/relevance score -> evidence/verification queue -> editorial dashboard.

No source adapter may bypass SSRF, rate-limit, robots/terms, licensing, or evidence policies.

## Story object
A candidate story should track identifiers, discovered timestamp, topic/category, geographic relevance, entities/products/companies, source references, primary-source status, confidence, verification state, urgency, duplicate cluster, risk flags, assigned reviewer, draft state, and publication status.

## AI-assisted newsroom roles
AI may perform scoped tasks such as:
- radar triage and clustering
- extraction of factual claims from sources
- entity/product/company matching
- source comparison and contradiction detection
- timeline/context assembly
- structured first-draft creation
- headline/meta/summary suggestions
- internal-link suggestions
- social-platform variants
- copy-editing and style checks
- risk flags for unsupported claims or suspicious sources

AI output remains untrusted. It may prepare or propose publication artifacts but cannot treat an unsupported statement as verified fact.

## Human approval
Initial operating model:
Internet/source -> evidence collection -> AI research/draft -> human editor review -> publish.

Automatic publication of sensitive, breaking, defamatory, legal/regulatory, financial, security, rumor/leak, or otherwise high-impact claims is prohibited unless a later approved policy defines a tightly bounded workflow.

## Evidence-first journalism
Where practical, discovery from another publication should lead back to primary evidence: company statements, filings, regulator notices, official repositories, investor statements, official product materials, direct interviews, or other original sources. RundaTech must not operate as an automated rewrite engine for other publishers.

Important factual claims should link to source records/snapshots and preserve verification history. Conflicting claims should be stored and surfaced rather than silently discarded.

## Solo-operator dashboard
The editorial dashboard should emphasize attention management: high-priority stories, Kenya/East Africa relevance, product launches, funding events, regulatory changes, AI developments, source count, primary-source availability, confidence, age, and recommended next action.

## Failure isolation
News monitoring, crawling, clustering, AI drafting, image processing, and social publishing run asynchronously in isolated workers/queues. A broken source or social platform must never take the public RundaTech site offline.

## Metrics
Track source freshness, candidate-to-publish conversion, time-to-first-draft, time-to-publish, corrections, unsupported-claim flags, source diversity, social distribution success/failure, and editorial workload. Optimize for trustworthy useful coverage, not raw article count.