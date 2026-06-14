# Example: API Integration

**Input**
```text
/tech-advisor:analyze

Integrate a third-party shipping rates API into our Node/TS backend.
Need typed responses, caching, and graceful degradation if the API is down.
```

**Output**

# Tech Advisor Report

## Source
Direct Input

## Task Type
Feature / Backend / Integration

## Summary
Add a third-party shipping-rates integration to a Node/TS backend with typed responses, caching, and a fallback when the upstream is unavailable.

## Technical Needs
- Typed HTTP client + response validation
- Caching of rate lookups
- Graceful degradation / circuit breaking
- Tests with mocked upstream

## Recommended Technologies

| Category | Tool | Score | Comment |
|---|---|---:|---|
| HTTP Client | undici / fetch | 8/10 | Fast, native; no extra dep |
| Validation | Zod | 9/10 | Runtime-validate + infer types |
| Cache | Redis | 8/10 | Shared TTL cache for rates |
| Resilience | opossum (circuit breaker) | 7/10 | Degrade when upstream fails |

## Why These Tools
Native fetch keeps deps minimal; Zod turns untrusted JSON into typed, validated data; Redis caches rate lookups to cut latency and cost; a circuit breaker prevents the upstream's outage from taking you down.

## Popularity Analysis

| Tool | Popularity | Maintenance | Community | Comment |
|---|---|---|---|---|
| Zod | High | Active | Strong | De facto TS validation |
| Redis | High | Active | Strong | Ubiquitous cache |
| opossum | Medium | Active | Moderate | Mature circuit breaker |

## Suggested Plan Enhancements
1. Wrap the API in a typed client module.
2. Validate every response with Zod before use.
3. Cache rates in Redis with a sensible TTL.
4. Add a circuit breaker + cached/last-known fallback.
5. Add contract tests with a mocked upstream.

## Risks
- Stale cached rates if TTL is too long.
- Third-party API/contract changes break parsing — validation catches this.
- Circuit-breaker thresholds need tuning to upstream SLA.

## Alternatives

| Tool | When to Use |
|---|---|
| ky / axios | When you want a richer client ergonomics layer |
| In-process LRU | When a shared cache isn't needed (single instance) |

## Final Recommendation
Native fetch + Zod + Redis covers typing, caching, and safety with minimal deps. Add opossum for graceful degradation if the upstream's reliability is uncertain; otherwise a simpler timeout + cached-fallback may suffice.
