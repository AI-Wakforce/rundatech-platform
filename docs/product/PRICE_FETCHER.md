# Automated Price Fetcher

## Objective
Collect current market prices safely and historically without allowing one retailer or crawler failure to affect RundaTech availability.

## Pipeline
Scheduler -> queue -> retailer adapter -> fetch -> parse/extract -> normalize -> validate -> append price observation -> anomaly checks -> update derived current offer -> downstream cache/search events.

## Adapter contract
Each retailer/affiliate source implements a common contract rather than leaking source-specific parsing into core pricing logic.

Adapter outputs should include:
- retailer/product mapping
- observed price + currency
- stock/availability where trustworthy
- source URL/identifier
- observed timestamp
- raw payload/snapshot reference where legally/operationally appropriate
- parser/adapter version
- confidence/validation flags

## Safety
- Respect lawful access, retailer terms and robots/site constraints as applicable.
- Prefer official feeds/APIs/affiliate feeds over brittle scraping when available.
- Outbound requests use allowlisted hosts and SSRF protections.
- Rate limits and concurrency are retailer-specific.
- Timeouts, bounded retries, jitter/backoff, circuit breakers and dead-letter queues.
- Browser execution/scrapers are sandboxed with strict resource/egress policy.
- Never place retailer secrets in URLs/logs.

## Price history
`price_observations` are historical append-only measurements. Incorrect observations are invalidated/flagged, not erased silently.

`offers` maintain current derived state based on the latest valid/trusted observation and freshness policy.

## Anomaly checks
Examples:
- price changes beyond configured percentage/absolute threshold
- currency mismatch
- price outside plausible category range
- dramatic price change without matching product identity
- stale source
- parser returning multiple conflicting prices

Suspicious observations are held from current-price promotion pending another observation or review.

## Monitoring
Per-adapter metrics: fetch success, parsing success, HTTP errors, rate limits, freshness, queue age, anomaly rate, product mapping misses and latency.