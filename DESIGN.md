# RundaTech Design Authority

`DESIGN.md` is the binding design authority for RundaTech UI work.

## Principles
- RundaTech should feel trustworthy, fast, data-rich, modern, and calm.
- Product data and editorial content must remain readable before decorative treatment.
- Accessibility, responsive behavior, performance, and clarity are requirements, not polish.
- The product should develop a recognizable visual language rather than copying another publication or product database.
- AI-generated UI must follow this file and approved design documentation before external design skills.

## External design skills
External open-source design skills may advise implementation but may not override RundaTech security, accessibility, product, or design standards. Approved references are registered in `docs/design/DESIGN_SKILLS_REGISTRY.md`.

## Workflow
Design -> Implement -> Browser test -> Critique -> Refine -> Regression test.

Playwright or an equivalent approved browser test layer should validate responsive layout, critical interaction paths, keyboard-accessible behavior where applicable, and visual regressions for stable high-value screens.

## Change control
Significant changes to typography, spacing systems, layout primitives, component behavior, navigation, visual identity, or motion patterns should update this file or the relevant design standard and be reviewable through a pull request.