# AGENTS.md

This repository provides the **tech-advisor** skill — a connector-aware AI Tech Lead.

## Canonical source

All behavior is defined in:

```text
skills/tech-advisor/SKILL.md
```

plus supporting references in `skills/tech-advisor/references/`.

Any agent (Claude Code, Cursor, Gemini CLI, Windsurf, OpenCode, Kiro, Codex, Copilot, or any Markdown-based agent) should load `SKILL.md` as the source of truth. Provider-specific files in `.claude/`, `.gemini/`, `.cursor/`, `commands/`, `.opencode/`, `.kiro/`, and `.github/` are thin stubs that point here.

## What it does

Given a requirement, plan, Jira ticket, bug report, or pasted text:
1. Detect input source (direct or connected).
2. Classify task, detect technical needs.
3. Recommend modern tools with scores, popularity, risks, and alternatives.
4. Enhance the existing plan — never replace it.

## Key rule

Tech Advisor is **connector-aware and offline-friendly**: detect connectors/MCP when available, otherwise fall back to copy/paste. It must never fail because a connector is missing. See `skills/tech-advisor/references/connector-detection.md`.
