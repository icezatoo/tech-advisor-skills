# CLAUDE.md

Project memory for **tech-advisor** in Claude Code.

## What this repo is

A portable, connector-aware "AI Tech Lead" skill. Canonical definition:

```text
skills/tech-advisor/SKILL.md
```

## How to use it here

- Slash command: `.claude/commands/tech-advisor.md` (invokes the skill).
- Plugin manifest: `plugin.json` registers `skills/tech-advisor/SKILL.md`.
- Invoke with `/tech-advisor analyze | compare | stack | explain`.

## Working rules (when editing this repo)

- **Single source of truth.** Put logic in `SKILL.md` or `references/`, never in provider stubs. Stubs stay ≤ ~15 lines and only point to `SKILL.md`. See `skills/tech-advisor/references/multi-agent-support.md`.
- **Connector-aware + offline-friendly.** Never make the skill depend on a connector existing; always allow copy/paste fallback. See `skills/tech-advisor/references/connector-detection.md`.
- Every recommendation must include **scores, risks, and alternatives**, and must enhance (not replace) any existing plan.

## Connectors / MCP

If a Jira/Confluence/GitHub/GitLab/Notion MCP resource is available, the skill may fetch sources automatically. Otherwise it asks the user to paste content. Both paths must yield the same report quality.
