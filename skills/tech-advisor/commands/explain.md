# Command: explain

Explain a single tool, pattern, or technology decision in depth — like a tech lead walking a teammate through the "why".

## Usage

```text
/tech-advisor:explain <tool | pattern | decision> [for <context>]
```

Example:
```text
/tech-advisor:explain circuit breaker pattern for external API calls
```

## Output

```markdown
## <Topic>

### What it is
<plain-language definition>

### When to use it
<the problems it solves; signals you need it>

### When NOT to use it
<over-engineering / simpler alternatives>

### Trade-offs
<cost, complexity, failure modes>

### How it fits a modern stack
<concrete tools that implement it — see references/tech-catalog.md>

### Risks
<per references/risk-checklist.md>
```

## Must

- Be honest about when the thing is overkill.
- Tie the explanation to concrete, maintained tooling.
- Keep it decision-useful, not encyclopedic.
