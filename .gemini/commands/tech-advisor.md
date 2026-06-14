# /tech-advisor (Gemini CLI)

Run the **tech-advisor** skill. Canonical logic: `skills/tech-advisor/SKILL.md` — load and follow it.

Subcommands: `analyze` · `compare` · `stack` · `explain` (see `skills/tech-advisor/commands/`).

Connector-aware: detect connectors/MCP if available; otherwise fall back to copy/paste. Never fail because a connector is missing.
