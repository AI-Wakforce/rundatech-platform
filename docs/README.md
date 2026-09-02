# RundaTech Platform Engineering & Governance Handbook

**Status:** Foundation v0.1  
**Date:** 2026-09-02  
**Purpose:** The authoritative operating manual for humans and AI agents building, operating, securing, and extending the RundaTech technology intelligence platform.

## North Star
RundaTech is designed as a multi-country technology data, comparison, pricing, editorial, and AI platform. The system must remain secure, evidence-based, maintainable, portable, observable, auditable, and easy to extend.

## Non-negotiable principles
1. **Database is the source of truth; AI is never the source of truth.**
2. **Evidence before publication.** Every factual product claim should be traceable to a source.
3. **Least privilege everywhere.** Humans, services, AI agents, and database roles receive only the access they require.
4. **No direct public database access.** All writes go through controlled application/service boundaries.
5. **Failure isolation.** Background import, AI, and price-fetching workloads run independently from the user-facing product.
6. **Append-only audit trail for material actions.** Never silently rewrite history.
7. **Portable by design.** Prefer PostgreSQL, containers, open protocols, exportable object storage, and vendor-neutral observability.
8. **Stable identifiers.** Internal IDs never depend on domain names, slugs, emails, or country.
9. **Country configuration, not country forks.** `.co.ke`, `.ug`, `.tz`, `.com`, etc. map to market configuration rather than duplicated codebases.
10. **AI must be constrained, evaluated, and reversible.** No autonomous destructive production changes.

## Recommended technology baseline
- **Web / admin / API edge:** TypeScript + Next.js
- **Database:** PostgreSQL
- **AI/data/ingestion workers:** Python
- **Queue/cache/rate limits:** Redis-compatible service initially; queue abstraction retained
- **Object storage:** S3-compatible storage
- **Containers:** Docker / OCI images
- **Infrastructure as Code:** Terraform/OpenTofu-compatible approach when infrastructure matures
- **Observability:** OpenTelemetry instrumentation
- **API contracts:** OpenAPI; webhooks/events use versioned schemas

## Document map
- `../AGENTS.md` — mandatory instructions for future AI coding agents
- `architecture/` — system boundaries, modules, isolation, portability and country routing
- `security/` — identity, RBAC, secrets, audit, threat model and secure SDLC
- `data/` — core data model, lifecycle, record correction, provenance and database rules
- `ai/` — AI architecture, governance, prompt versioning and evals
- `product/` — product ingestion and automated price system
- `operations/` — deployments, migrations, incidents, observability, backup/DR and expansion
- `governance/` — evidence, naming, change management and documentation policy
- `team/` — future employee/team responsibilities
- `roadmap/` — master implementation roadmap
- `adr/` — Architecture Decision Records
- `prompts/` — version-controlled production prompt specifications

## Status language
- **Proposed**: not approved for production implementation.
- **Accepted**: default architecture/policy.
- **Deprecated**: should not be used for new work.
- **Superseded**: replaced by a newer ADR/policy.

Start every build session by reading `AGENTS.md`, this document, the relevant module docs, and accepted ADRs.