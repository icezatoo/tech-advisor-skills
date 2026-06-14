# Command: compare

Compare two or more tools head-to-head for a specific task.

## Usage

```text
/tech-advisor compare <toolA> vs <toolB> [vs <toolC>] [for <context>]
```

Example:
```text
/tech-advisor compare Resty vs net/http vs Heimdall for external API calls with retry
```

## Steps

1. Confirm the **task context** (what the tools must do). If missing, ask.
2. Score each tool with `references/scoring-rule.md`.
3. Assess each with `references/popularity-criteria.md`.
4. Identify risks per `references/risk-checklist.md`.

## Output

```markdown
## Comparison: <context>

| Tool | Score | Fit | Maintenance | Key strength | Key risk |
|---|---:|---|---|---|---|

## Recommendation
<which to pick, and the condition under which you'd pick each>
```

## Must

- Pick a winner *and* state when each alternative is the better call.
- Never declare a winner on popularity alone — fit, maintenance, and security decide.
