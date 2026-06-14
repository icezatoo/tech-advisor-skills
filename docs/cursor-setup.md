# Cursor Setup

## Install
The rule lives at `.cursor/rules/tech-advisor.md` and points to the canonical skill at `skills/tech-advisor/SKILL.md`.

1. Keep `skills/tech-advisor/` in your project (so the rule can reference it), **or**
2. Paste the contents of `skills/tech-advisor/SKILL.md` directly into `.cursor/rules/tech-advisor.md` if you prefer a self-contained rule.

## Use
Ask Cursor things like:
- "What should I use to add retry + logging to this Go API call?"
- "Analyze this Jira ticket and recommend a stack."

Tech Advisor will return the full report (Source → Final Recommendation).

## Connectors / MCP
Cursor supports MCP. If a connector is available, sources can be fetched automatically; otherwise paste the content. The skill never fails when a connector is missing.
