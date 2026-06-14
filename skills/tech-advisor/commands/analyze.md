# Command: analyze

Primary Tech Advisor command. Analyzes any **direct** or **connected** source and returns the full Tech Advisor Report.

## Usage

```text
/tech-advisor:analyze <ticket-key | url | pasted content>
```

## Input modes

This command must support **connected input OR direct input** — both produce the same report (see `references/connector-detection.md`).

### Connected — Jira key
```text
/tech-advisor:analyze OAPI-12345
```
Detect the key → check for a Jira connector/MCP → fetch summary, description, acceptance criteria, components, labels, comments, linked issues → analyze.

### Connected — URL
```text
/tech-advisor:analyze
https://company.atlassian.net/browse/OAPI-12345
```
Detect the URL → if a connector is available, fetch; otherwise request the user paste the content.

### Fallback — connector not available
If no connector/MCP matches the detected source, respond with the templated message in `references/connector-detection.md` (Mode 3) and continue in direct mode once the user pastes content.

### Direct — pasted requirement / plan / ticket
```text
/tech-advisor:analyze

Need to fix HTTP timeout when calling external API.
Need retry and logging.
```
Treat as direct input → analyze immediately.

## Steps

1. Run the **Connector-Aware Detection** flow (SKILL.md §A).
2. Run the **Analysis Workflow** (SKILL.md §B).
3. Emit the full report in the exact field order from SKILL.md → Output.
4. Run the **Verification** checklist before returning.

## Must

- Never invent ticket content. Fetch it or ask for it.
- Always include Risks **and** Alternatives.
- Enhance any existing plan; never replace it.
- Produce identical quality whether the source was connected or pasted.
