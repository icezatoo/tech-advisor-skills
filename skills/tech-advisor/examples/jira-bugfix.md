# Example: Jira Bugfix (with connector fallback)

This example shows the **no-connector fallback** path, then a normal analysis.

**Input**
```text
/tech-advisor:analyze OAPI-12345
```

**Step 1 — connector not available**, so Tech Advisor responds:

```markdown
Jira ticket detected.

No Jira connector or MCP access is available in the current environment.

Please provide one of the following:

- Jira Summary
- Jira Description
- Acceptance Criteria
- Existing Implementation Plan

Tech Advisor will continue analysis using direct input mode.
```

**Step 2 — user pastes ticket content**
```markdown
Title: Payment webhook handler drops events under load
Description: Webhook returns 200 before persisting; events lost when DB is slow.
Acceptance Criteria: No event loss; retries safe; observable failures.
```

**Output**

# Tech Advisor Report

## Source
Jira (OAPI-12345) — provided via copy/paste fallback

## Task Type
Bugfix / Backend / Reliability

## Summary
A payment webhook acknowledges before persisting, losing events when the database is slow. Needs durable intake, safe retries, and observability.

## Technical Needs
- Durable, idempotent event intake
- Async processing with retries
- Observability on failures

## Recommended Technologies

| Category | Tool | Score | Comment |
|---|---|---:|---|
| Queue | BullMQ (Redis) | 8/10 | Durable jobs + retries/backoff |
| Idempotency | DB unique key on event id | 9/10 | Prevents duplicate processing |
| Observability | OpenTelemetry | 8/10 | Traces + metrics across the path |

## Why These Tools
Persist the raw event first (with the provider's event id as a unique key), enqueue async work, and process with retries. Idempotency keys make retries safe. OTel makes drops visible.

## Popularity Analysis

| Tool | Popularity | Maintenance | Community | Comment |
|---|---|---|---|---|
| BullMQ | High | Active | Strong | Standard Node/Redis queue |
| OpenTelemetry | High | Active | Strong | Vendor-neutral observability |

## Suggested Plan Enhancements
1. Persist the event before returning 200 (or return 202 + durable enqueue).
2. Add a unique constraint on provider event id for idempotency.
3. Process via a retrying queue with backoff and a dead-letter queue.
4. Add metrics: received, processed, failed, DLQ depth.
5. Add tests simulating slow/failing DB.

## Risks
- Retry **duplicates** without an idempotency key.
- Redis is a new dependency to operate and monitor.
- Webhook signature verification must be preserved.

## Alternatives

| Tool | When to Use |
|---|---|
| SQS / RabbitMQ | When already on that infra or need managed durability |
| Outbox pattern | When you want intake durability without a separate broker |

## Final Recommendation
Persist-then-enqueue with an idempotency key is the core fix. Use BullMQ if Redis is available; otherwise the transactional outbox pattern achieves the same guarantee with your existing DB. Add OTel regardless.
