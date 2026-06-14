---
description: Tech Advisor — full Tech Advisor Report for a requirement, plan, ticket, or pasted text
---

# /tech-advisor:analyze

Run the **tech-advisor** skill in `analyze` mode. Canonical logic lives in `skills/tech-advisor/SKILL.md`; subcommand spec in `skills/tech-advisor/commands/analyze.md` — load and follow both.

Analyze any **direct** or **connected** source and return the full Tech Advisor Report. Connector-aware: detect Jira/GitHub/MCP if available; otherwise fall back to copy/paste. Never fail because a connector is missing.

Arguments: `$ARGUMENTS`
