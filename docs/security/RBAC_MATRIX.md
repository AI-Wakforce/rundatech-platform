# Initial RBAC Matrix

Legend: `R` read, `E` edit/draft, `P` publish/approve, `A` administer, `-` none by default.

| Capability | Owner | Platform Admin | Catalog Mgr | Product Editor | Product Reviewer | Pricing Mgr | Pricing Ops | Content Mgr | Content Editor | Support | Analyst | Auditor |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Catalog | A | A | A | E | P | R | R | R | R | R | R | R |
| Evidence/source records | A | A | A | E | P | R | R | R | R | - | R | R |
| Retailers/offers | A | A | R | R | R | A | E | R | - | R | R | R |
| Editorial content | A | A | R | R | R | R | R | A/P | E | R | R | R |
| User support data | A | A | - | - | - | - | - | - | - | E | R | R |
| Roles/permissions | A | A* | - | - | - | - | - | - | - | - | - | R |
| Audit log | R | R | R | R | R | R | R | R | R | limited | R | R |
| AI prompt production | A | A | R | - | R | R | R | R | R | - | R | R |
| Deployments | A | scoped | - | - | - | - | - | - | - | - | - | R |

`*` Highly privileged role assignments should later require security/owner approval or dual control.

This table is policy intent. The application should enforce granular permission keys and optional market scopes rather than checking this table/role name directly.