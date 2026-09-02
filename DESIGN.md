# RundaTech DESIGN.md

This file is the authoritative entry point for RundaTech UI design decisions.

## Product character
RundaTech should feel trustworthy, technical, fast, information-dense without being cluttered, and optimized for helping people compare technology and make buying decisions. Visual polish must never reduce readability, accessibility, performance or factual clarity.

## Design authority
RundaTech's approved tokens, components, interaction patterns and accessibility standards override external design-skill preferences. External skills are advisers, not authorities.

See `docs/design/DESIGN_SKILLS_REGISTRY.md` for governed external references including Awesome DESIGN.md/getdesign, Taste Skill, Impeccable, Emil Kowalski skills and Playwright.

## Core rules
- Reuse approved components and tokens before inventing new ones.
- Product/specification data must remain scannable and comparable.
- Comparison tables must prioritize legibility, responsive behavior and keyboard usability.
- Avoid decorative motion that delays tasks; respect reduced-motion preferences.
- Do not hide essential actions behind hover-only interactions.
- Responsive design is required, not a later patch.
- Accessibility is a release requirement.
- Performance is part of design quality, especially on image-heavy product pages.
- Sponsored/affiliate/commercial UI must be distinguishable from factual/editorial content.
- UI tests should cover critical flows with Playwright or the approved browser-test layer.

## Change governance
Material changes to the design language, token model, component architecture or core interaction patterns require documentation and review. New external design skills must be added to the registry before they are treated as recurring project guidance.