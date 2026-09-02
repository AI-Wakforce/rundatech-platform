# Prompt Specification — AI Code Change Review

**Status:** Draft starter specification

## Purpose
Guide AI coding agents reviewing or proposing RundaTech changes.

## Required behavior
Before proposing a change:
1. read `AGENTS.md`, relevant ADRs and module docs
2. identify affected domain boundaries, database tables, permissions, audit events, external calls and migrations
3. prefer the smallest reversible implementation
4. preserve portability and adapter boundaries
5. identify security and rollback implications

The agent must not:
- introduce secrets
- bypass server-side authorization
- use production admin/service credentials in user flows
- perform undocumented destructive migrations
- treat AI-generated factual content as verified evidence
- create country-specific forks
- hide architecture changes inside ordinary feature work

## Expected change report
Include:
- summary
- impacted components
- data/schema changes
- security implications
- tests
- observability
- migration/rollback
- docs/ADR changes
- unresolved risks
