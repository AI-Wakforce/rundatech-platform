# Media Rights and Asset Policy

RundaTech must not assume that an image is reusable merely because it is visible online or credited. Every externally sourced media asset used in publication should have a known rights basis.

## Approved asset sources
Preferred sources include:
- RundaTech-owned photography, graphics, diagrams, screenshots where lawful, and branded social cards
- manufacturer/company press assets whose published terms permit the intended editorial/commercial use
- media supplied directly with press releases where reuse rights are clear
- public-domain material
- Creative Commons material whose specific license permits the intended use and whose attribution/derivative/commercial conditions are satisfied
- properly licensed stock/editorial media services
- commissioned/licensed contributor assets
- AI-generated illustrations when appropriate, clearly governed by RundaTech policy and not misleadingly presented as documentary photography

## Prohibited/default-deny behavior
Do not automatically copy images from Google Images, another publisher, social media posts, blogs, or arbitrary websites. Attribution alone is not treated as permission.

If rights cannot be established, status is `rights_unknown` and the asset must not be published.

## Asset rights record
Each publishable external asset should track:
- asset ID
- source URL/source record
- creator/rights holder where known
- license/permission basis
- commercial use allowed?
- modification/derivative restrictions
- attribution requirement and exact credit text
- geographic/term restrictions where relevant
- rights-evidence snapshot/reference
- review date and reviewer
- expiration/review date where applicable
- publication contexts where approved

Suggested states: `owned`, `licensed`, `press_use_approved`, `public_domain`, `cc_approved`, `restricted`, `rights_unknown`, `expired`, `removed`.

## Branded fallback
When a story has no safely reusable documentary image, the CMS should be able to generate a RundaTech-branded visual card using headline/topic/entity information without copying a protected third-party image. This is the default safe fallback for breaking news.

## Takedown and disputes
If a rights complaint is received: preserve evidence, temporarily remove or replace the disputed asset when appropriate, verify the license/permission, log the action, and follow legal review/takedown procedures. Removing an asset must not erase its audit/history record.

## AI and media
AI agents may suggest candidate assets but must not infer rights from appearance or attribution. A rights state must come from documented permission/license evidence or an approved RundaTech-owned generation workflow.