# Command: stack

Recommend a full technology stack for a project or feature.

## Usage

```text
/tech-advisor:stack <project description | connected source>
```

Accepts **connected input OR direct input** (same rules as `analyze`; see `references/connector-detection.md`).

Example:
```text
/tech-advisor:stack

Building a B2B dashboard: needs auth, charts, REST API, Postgres, deployed on AWS.
```

## Steps

1. Run Connector-Aware Detection if the input is a ticket/URL; otherwise treat as direct.
2. Break the project into **layers**: frontend, backend/API, data, auth, infra/DevOps, observability, testing.
3. For each layer, recommend a primary tool + alternatives from `references/tech-catalog.md`, scored via `references/scoring-rule.md`.
4. Note cross-layer fit (do the choices work together?).

## Output

```markdown
## Recommended Stack: <project>

| Layer | Recommended | Score | Alternative | Why |
|---|---|---:|---|---|

## Integration Notes
<how the pieces fit; any friction>

## Risks
<per references/risk-checklist.md>

## Final Recommendation
```

## Must

- Respect any stated existing stack / constraints.
- Keep the stack coherent — avoid mixing tools that fight each other.
- Include observability and testing layers; do not omit them.
