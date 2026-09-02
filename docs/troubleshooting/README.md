# Troubleshooting Knowledge Base

This directory stores reusable resolutions for non-trivial RundaTech problems. It is not a dump of transient errors; add entries when future humans or AI agents would benefit from knowing how an issue was diagnosed and resolved.

## Before troubleshooting
Read:
- `docs/engineering/TROUBLESHOOTING_PLAYBOOK.md`
- the affected module README
- relevant ADRs and security controls
- existing entries in this directory

## Suggested structure
```text
docs/troubleshooting/
  database/
  pricing/
  auth/
  ai/
  deployments/
  search/
  catalog/
```

Create folders only when needed.

## Entry template
```markdown
# <Issue title>

## Summary
## Symptoms
## Affected component / market
## Severity / impact
## First observed
## How to reproduce
## Evidence collected
## Root cause
## Resolution
## Rollback / emergency mitigation
## Verification
## Prevention / regression protection
## Related PRs / incidents / ADRs / controls
## Last reviewed
```

## Rules
- Do not include passwords, tokens, secret values, unnecessary PII, or sensitive dumps.
- Prefer concrete evidence over speculation.
- Document failed hypotheses only when they are likely to save meaningful future debugging time.
- Link to durable identifiers such as PRs, incidents, ADRs, control IDs, trace/dashboard references, or migration IDs where appropriate.
- Update or retire an entry when architecture changes make its resolution obsolete.
- Security incidents may require restricted documentation; public repository documentation should contain only safe operational knowledge.

## AI-agent use
Before proposing broad changes for a recurring or unfamiliar issue, AI agents should search this knowledge base and recent relevant change history. Existing resolutions are guidance, not permission to repeat a fix blindly; validate that symptoms, architecture, versions, and evidence still match.