# Secrets and Sensitive Data Policy

## Secret classes
- database credentials
- AI provider/API keys
- retailer/integration credentials
- signing/encryption keys
- OAuth secrets
- deployment tokens
- webhook secrets

## Rules
1. No secrets in Git, documentation, prompts, screenshots, issue text or browser-delivered code.
2. Production secrets are injected at runtime from a managed secret store/platform secret facility.
3. Frontend code receives only explicitly public configuration.
4. Separate development, staging and production credentials.
5. Rotate secrets on personnel changes, suspected exposure, provider policy, and defined schedule.
6. Grant each service only the secrets it requires.
7. Never share one high-privilege database credential across all services.
8. Secret values are redacted from logs/traces/errors.
9. Webhook/integration signatures must be verified.
10. Maintain a secrets inventory with owner, purpose, environment, created/rotated dates—never secret values.

## AI data boundary
Do not send secrets, raw authentication tokens, unnecessary PII, confidential commercial terms or private employee records to external AI models. AI connectors receive minimal context.