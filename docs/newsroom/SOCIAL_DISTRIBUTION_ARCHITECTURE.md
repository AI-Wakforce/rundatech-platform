# Social Distribution Architecture

RundaTech should support publishing an approved article into multiple platform-specific social formats without forcing the editorial team to manually rewrite the same story for every network.

## Principle
Publish once to RundaTech, then derive channel-specific distribution artifacts. Do not send identical text everywhere by default.

## Flow
Article approved/published -> social content generator -> channel-specific variants -> approval/scheduling policy -> provider adapters -> delivery receipts -> analytics/failed-job queue.

## Channel adapters
Support official provider APIs where available and permitted. Social platforms must be implemented behind adapters so API/policy changes do not spread through editorial/domain code.

Potential adapters include LinkedIn, Facebook/Instagram, X, Threads, YouTube, Telegram, WhatsApp/business messaging where approved, newsletter/email, and future networks. Not every platform guarantees public publishing APIs; unsupported channels should degrade to export/copy workflows rather than unsafe automation.

## Generated artifacts
A single article may generate:
- short breaking-news post
- professional LinkedIn-style summary
- Facebook post
- Instagram caption + RundaTech visual card
- Threads/X variants
- newsletter snippet
- messaging-channel alert
- short-video script/storyboard
- video title/description where relevant

Each artifact should keep a link to the source article, campaign ID, content version, generated-by identity, approval state, destination account, scheduled/published timestamps, and remote post ID where returned.

## Approval model
Default initially: article approval does not automatically grant unrestricted social posting. The system should support one-click approval of a reviewed distribution bundle, platform-specific edits, and scheduling.

Lower-risk evergreen distribution may later be automated through an approved policy. Sensitive/breaking/legal/regulatory stories should retain human approval.

## Security
- OAuth/API credentials stored in managed secrets, never browser bundles or repository code.
- Least-privilege platform scopes.
- Separate credentials/account identities per provider where practical.
- Token rotation/revocation and audit history.
- Rate limits and provider quotas respected.
- Signed callbacks/webhooks verified.
- Retryable publishing uses idempotency/deduplication to avoid duplicate posts.

## Failure handling
One failed channel must not block the article or other channels. Failed jobs go to a retry/DLQ workflow with provider response, correlation ID, safe error details, and manual retry controls.

## Analytics
Collect attributable referral/engagement metrics through provider adapters and RundaTech analytics where permitted. Keep raw provider metrics distinguishable from normalized metrics; do not fabricate cross-platform equivalence.