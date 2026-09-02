# ADR-0001 — Modular Monolith + Isolated Workers

**Status:** Accepted  
**Date:** 2026-09-02

## Context
RundaTech needs a codebase that remains simple for a small team and AI-assisted development, while isolating failure-prone workloads such as crawling, price fetching, AI extraction, indexing and bulk imports.

## Decision
Use a modular monolith for core synchronous product functionality, with explicit domain boundaries and isolated containerized workers for asynchronous/high-risk workloads.

## Consequences
Benefits:
- lower operational complexity than premature microservices
- easier local development and migration
- consistent transactions for core domain operations
- background failures can be isolated
- future service extraction remains possible through explicit interfaces/events

Costs:
- module discipline is required inside one codebase
- some deployments may still share release cadence initially
- scaling one module independently may later require extraction

## Guardrails
- no cross-module table mutation without an approved contract
- background workloads use queues when practical
- workers use bounded resources/retries and idempotency
- architecture changes require ADR updates

## Revisit when
Measured scale, security isolation, availability requirements or independent team ownership make a service boundary economically justified.