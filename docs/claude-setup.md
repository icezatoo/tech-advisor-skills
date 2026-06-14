# Claude Code Setup

## Option A — Local plugin directory
```bash
git clone <repo-url> tech-advisor-skills
claude --plugin-dir /path/to/tech-advisor-skills
```

## Option B — Manual
Copy `skills/tech-advisor/` into your project (or `~/.claude/skills/`), and the command file to `.claude/commands/tech-advisor.md`.

## Use
```text
/tech-advisor analyze OAPI-12345
/tech-advisor analyze <pasted requirement or plan>
/tech-advisor compare <toolA> vs <toolB>
/tech-advisor stack <project description>
/tech-advisor explain <tool | pattern>
```

## Connectors / MCP
If a Jira/Confluence/GitHub/GitLab/Notion MCP server is configured, Tech Advisor can fetch sources automatically. If not, it asks you to paste content. Both paths produce the same report. See `skills/tech-advisor/references/connector-detection.md`.
