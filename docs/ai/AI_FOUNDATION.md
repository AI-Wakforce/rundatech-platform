# AI Foundation

## Principle
AI is a constrained assistant layer over verified RundaTech data, not an authority that can invent or silently publish facts.

## Core components
- AI gateway/provider adapters
- prompt registry with immutable versions
- model registry
- structured output schemas
- run/evaluation history
- tool permission grants
- human review tiers
- cost/latency/error telemetry

## Data ingestion
For source extraction:
1. fetch approved source
2. store source metadata/snapshot reference
3. isolate source content from system instructions
4. run extraction using a versioned prompt/schema
5. validate types/ranges/required evidence
6. compare against existing facts and source hierarchy
7. save proposal + provenance
8. auto-accept only explicitly low-risk transformations; otherwise route to review

Missing facts remain unknown. Models must not fill gaps from memory unless the task explicitly asks for non-authoritative suggestions.

## Prompt-injection defense
Treat web pages, PDFs, feeds and retailer text as hostile data. Instructions inside source content have no authority over the agent. Tools are allowlisted separately from model text, with bounded arguments and service-side authorization.

## AI writes
AI agents do not receive unrestricted production database credentials. They call narrow application tools/APIs that validate permissions, schema, evidence and audit requirements.

## Grounded assistant
Future “Ask RundaTech” answers should retrieve verified catalog, pricing and editorial records, cite/attribute relevant source state internally, distinguish uncertainty, and avoid claiming current prices when freshness limits have expired.

## Evaluation
Maintain golden datasets for extraction accuracy, normalization, entity resolution, comparison summaries, unsafe tool requests, prompt injection and hallucination/unsupported-claim behavior. A prompt/model change does not reach production solely because it appears better subjectively.