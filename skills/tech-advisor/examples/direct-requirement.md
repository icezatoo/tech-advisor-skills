# Example: Direct Requirement

**Input**
```text
/tech-advisor analyze

Need to fix HTTP timeout when calling external API.
Need retry and logging. Service is written in Go.
```

**Output**

# Tech Advisor Report

## Source
Direct Input

## Task Type
Bugfix / Backend

## Summary
A Go service calling an external API has no timeout, retry, or logging. Calls can hang and failures are invisible.

## Technical Needs
- Request timeout
- Retry with backoff
- Structured logging
- Testable HTTP layer

## Recommended Technologies

| Category | Tool | Score | Comment |
|---|---|---:|---|
| HTTP Client | Resty | 9/10 | Popular Go client with built-in timeout + retry |
| Logging | slog | 9/10 | Modern structured logging in the Go stdlib |
| Testing | httptest | 9/10 | Native HTTP server stubs for tests |

## Why These Tools
Resty covers timeout and retry without hand-rolling transport code. slog ships in the stdlib (no dependency) and gives structured logs for observability. httptest lets you test the client against a fake upstream.

## Popularity Analysis

| Tool | Popularity | Maintenance | Community | Comment |
|---|---|---|---|---|
| Resty | High | Active | Strong | Common choice for Go service integration |
| slog | High | Active (stdlib) | Strong | Standard since Go 1.21 |

## Suggested Plan Enhancements
1. Add a reusable HTTP client wrapper.
2. Configure timeouts (connect + total).
3. Add a retry policy with backoff and a max attempts cap.
4. Emit structured logs (request id, status, latency).
5. Add unit tests with httptest.
6. Add an integration test against a sandbox endpoint.

## Risks
- Retry may cause **duplicate requests** if the endpoint is not idempotent.
- Timeout values must match the upstream SLA.
- Adding Resty introduces a third-party dependency to review.

## Alternatives

| Tool | When to Use |
|---|---|
| net/http | When minimizing dependencies matters more than convenience |
| Heimdall | When you need advanced resilience (circuit breaking, hedging) |

## Final Recommendation
Use Resty for fast implementation with retry + timeout, paired with slog and httptest. Verify retry idempotency first. If the team wants zero new dependencies, use net/http with a custom `http.Client` and manual backoff.
