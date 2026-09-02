# Handbook Changelog

## 0.1.2 — 2026-09-02
Maintainability and troubleshooting hardening: added `docs/engineering/MAINTAINABILITY_STANDARD.md`, `docs/engineering/TROUBLESHOOTING_PLAYBOOK.md`, `docs/engineering/MODULE_DESIGN_STANDARD.md`, and `docs/troubleshooting/README.md`. Updated `AGENTS.md` so future AI agents must use evidence-based diagnosis, search existing troubleshooting knowledge, respect module/data ownership, avoid broad speculative changes, add regression protection for bugs, and optimize for long-term code clarity.

## 0.1.1 — 2026-09-02
Security hardening: added the mandatory `docs/security/SECURITY_BASELINE.md` with numbered controls for secrets, authentication/session security, login rate limiting, bot protection, server-side authorization, RLS, field tampering, parameterized queries, encryption, input/output handling, file uploads, HTTPS/security headers, CSRF/CORS, API abuse, SSRF, dependency/container scanning, logging/auditing, AI/agent boundaries, workload isolation, backups, and security exception governance. Updated `AGENTS.md` and the implementation checklist so future AI/code changes must comply with the baseline.

## 0.1 — 2026-09-02
Initial foundation: principles, architecture, multi-country model, IAM/RBAC, secrets, audit/threat model, data model, record correction, database safety, AI foundation/prompt governance, price fetcher, product ingestion, observability/DR, release/migrations, evidence/change governance, team model, roadmap, ADR framework and starter prompts.