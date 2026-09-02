# Architecture Diagram

```text
                           ┌───────────────────────────┐
                           │ CDN / WAF / DNS / TLS     │
                           │ .co.ke .ug .tz .com       │
                           └─────────────┬─────────────┘
                                         │
                          ┌──────────────▼──────────────┐
                          │ Public Web / API (Next.js)  │
                          └──────────────┬──────────────┘
                                         │
             ┌───────────────────────────┼───────────────────────────┐
             │                           │                           │
     ┌───────▼────────┐        ┌─────────▼────────┐        ┌────────▼────────┐
     │ PostgreSQL      │        │ Queue / Cache    │        │ Object Storage  │
     │ canonical truth │        │ bounded async    │        │ source/media    │
     └─────────────────┘        └─────────┬────────┘        └─────────────────┘
                                         │
                 ┌───────────────────────┼────────────────────────┐
                 │                       │                        │
       ┌─────────▼────────┐    ┌─────────▼────────┐     ┌────────▼─────────┐
       │ Pricing Worker    │    │ AI Worker         │     │ Data Worker       │
       │ retailer adapters │    │ extract/evaluate  │     │ imports/indexing  │
       └─────────┬────────┘    └─────────┬────────┘     └──────────────────┘
                 │                       │
        ┌────────▼─────────┐    ┌────────▼──────────┐
        │ Retailer APIs/    │    │ AI Provider        │
        │ feeds/web sources │    │ adapters            │
        └───────────────────┘    └────────────────────┘
```

## Operational principle
The public browsing path depends on RundaTech's durable canonical data, not on live retailer or AI availability. External failures are isolated behind workers, queues, adapters and cached/verified state.