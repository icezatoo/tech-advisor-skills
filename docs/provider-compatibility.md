# Provider Compatibility

Tech Advisor is provider-agnostic. One canonical skill (`skills/tech-advisor/SKILL.md`) is exposed through thin per-provider entry points. See `skills/tech-advisor/references/multi-agent-support.md` for the portability contract.

## Entry points

| Provider | Entry point | Mechanism |
|---|---|---|
| Claude Code | `.claude/commands/tech-advisor.md` + `plugin.json` | Slash command + plugin skill |
| Cursor | `.cursor/rules/tech-advisor.md` | Project rule |
| Gemini CLI | `.gemini/commands/tech-advisor.md` | Slash command |
| Antigravity | `commands/tech-advisor.md` | Slash command |
| OpenCode | `.opencode/tech-advisor.md` | Agent-driven execution |
| Kiro | `.kiro/skills/tech-advisor.md` | Skill storage |
| GitHub Copilot | `.github/copilot-instructions.md` | Repo instructions |
| Windsurf / Codex / other | `skills/tech-advisor/SKILL.md` | System prompt / project rules |

## Connector support

| Provider | Connector support | Notes |
|---|---|---|
| Claude Code | MCP | Jira/Confluence/GitHub/GitLab/Notion via MCP servers |
| Cursor | MCP | |
| OpenCode | MCP | |
| Windsurf | MCP | |
| Kiro | MCP | |
| Gemini CLI | Depends on environment | Falls back to copy/paste |
| GitHub Copilot | Connector dependent | Falls back to copy/paste |
| Codex | Connector dependent | Falls back to copy/paste |

## Guarantee

Regardless of provider or connector support, the **Fallback Rule** holds: if no connector/MCP is available, Tech Advisor uses copy/paste mode and produces the same quality report. It never fails because a connector is missing.
