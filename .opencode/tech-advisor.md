# tech-advisor (OpenCode)

Agent-driven entry point for the **tech-advisor** skill.

Canonical logic: `skills/tech-advisor/SKILL.md` — load and follow it (plus `skills/tech-advisor/references/`).

Subcommands: `analyze` · `compare` · `stack` · `explain`.

Connector-aware via MCP: detect Jira/Confluence/GitHub/GitLab/Notion resources if available; otherwise fall back to copy/paste. Never fail because a connector is missing.
