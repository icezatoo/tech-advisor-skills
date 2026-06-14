---
description: Tech Advisor — recommend modern tech for a requirement, plan, ticket, or pasted text (analyze | compare | stack | explain)
---

# /tech-advisor

Run the **tech-advisor** skill. Canonical logic lives in `skills/tech-advisor/SKILL.md` — load and follow it.

Subcommands (see `skills/tech-advisor/commands/`):
- `analyze` — full Tech Advisor Report for a direct or connected source.
- `compare` — compare 2+ tools.
- `stack` — recommend a full stack.
- `explain` — explain a tool / pattern / decision.

Connector-aware: detect Jira/GitHub/MCP if available; otherwise fall back to copy/paste. Never fail because a connector is missing.

Arguments: `$ARGUMENTS`
