# Future Team Operating Model

## Teams and boundaries
### Platform Engineering
Owns application architecture, APIs, deployments, database migrations, observability and developer platform. Does not approve factual editorial truth by default.

### Product Data / Catalog Operations
Owns taxonomy, product records, spec verification, duplicate resolution and source quality.

### Pricing Operations
Owns retailer integrations, price quality, anomaly review, freshness and retailer mappings.

### Editorial / Content
Owns reviews, guides, news, style and publication workflow. Cannot silently alter canonical catalog facts outside catalog workflow.

### AI & Automation
Owns prompts, model routing, evaluations, agent permissions and automation quality. Cannot grant itself new privileges.

### Security / Compliance
Owns policies, access review, incident response, threat modeling, security exceptions and audits.

### Commercial / Partnerships
Owns affiliate/retailer partnerships and commercial metadata, but cannot change independently verified technical specs for commercial reasons.

### Support
Owns customer/user support with narrowly scoped tools.

## Access governance
- Joiner/mover/leaver workflow
- quarterly privileged access review when team size warrants
- immediate revocation on offboarding
- temporary elevation expires automatically where possible
- no shared human accounts
- service accounts have owners and review dates

## Approval workflows
Critical publishing/data/security actions should support `draft -> review -> approved/published` with actor attribution.