# Risk Checklist

Every Tech Advisor report must include **risks and alternatives**. Walk this checklist; include the ones that apply.

## Universal risks

- [ ] Third-party dependency must be reviewed (license, maintenance, supply chain).
- [ ] New tool adds learning curve / cognitive load for the team.
- [ ] Tool may not fit the existing stack or deployment target.
- [ ] Version pinning / upgrade path needs a plan.

## Reliability & external calls

- [ ] Retry can cause **duplicate requests** if the API is not idempotent.
- [ ] Timeout values must match the upstream SLA.
- [ ] No circuit breaker / backoff → cascading failure under load.
- [ ] Missing observability (logs, metrics, traces) on the new path.

## Security-sensitive tasks

- [ ] Input validation and output encoding addressed.
- [ ] Secrets handling (no hard-coding; use a secrets manager).
- [ ] AuthN/AuthZ implications considered.
- [ ] Crypto uses vetted libraries and secure defaults (no homegrown crypto).

## Performance

- [ ] Behavior at scale (N× current load) considered.
- [ ] Caching / N+1 / hot-path allocation reviewed.

## Production features

- [ ] Testing strategy (unit + integration) included.
- [ ] Observability (structured logs, metrics) included.
- [ ] Rollback / feature-flag plan exists.

## Red Flags — stop and warn

- Recommendation ignores the existing stack.
- Tool is deprecated or unmaintained.
- Tool adds unnecessary complexity.
- Popularity is claimed without confidence.
- Security-sensitive task has no security recommendation.
- Bugfix with an external call has no timeout or retry consideration.
- Production feature has no testing or observability suggestion.
