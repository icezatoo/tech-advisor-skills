# Multi-Agent Support Reference

Tech Advisor is one canonical skill exposed to many agents through thin entry points. This file is the **portability contract**. Design modeled on [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills).

## Canonical-Source Rule

There is exactly one source of truth:

```text
skills/tech-advisor/SKILL.md   + skills/tech-advisor/references/*
```

Every provider-specific file is a **stub** that points to the canonical skill. Stubs must:

- Be short (≈ 15 lines or fewer).
- Contain **no** scoring logic, no connector logic, no output template.
- Reference `skills/tech-advisor/SKILL.md` so logic never drifts.

> If you find yourself copying workflow rules into a provider file, stop — put it in SKILL.md or a reference instead.

## Provider Entry-Point Map

| Provider | Folder / File | Mechanism | Points to |
| --- | --- | --- | --- |
| Claude Code | `.claude/commands/tech-advisor.md` | Slash command + plugin skill | `skills/tech-advisor/SKILL.md` |
| Cursor | `.cursor/rules/tech-advisor.md` | Project rule | `skills/tech-advisor/SKILL.md` |
| Gemini CLI | `.gemini/commands/tech-advisor.md` | Slash command | `skills/tech-advisor/SKILL.md` |
| Antigravity | `commands/tech-advisor.md` | Slash command | `skills/tech-advisor/SKILL.md` |
| OpenCode | `.opencode/tech-advisor.md` | Agent-driven execution | `skills/tech-advisor/SKILL.md` |
| Kiro | `.kiro/skills/tech-advisor.md` | Skill storage | `skills/tech-advisor/SKILL.md` |
| GitHub Copilot | `.github/copilot-instructions.md` | Repo instructions | `skills/tech-advisor/SKILL.md` |
| Windsurf / Codex / other | use `SKILL.md` directly | System prompt / project rules | `skills/tech-advisor/SKILL.md` |

## SKILL.md Template Contract

Every skill that follows this design uses:

**Frontmatter**
```yaml
name: lowercase-hyphen-name
description: <what it does>. Use when ...
```

**Section order ("Process, not prose" — executable workflow, not reference docs):**
1. Overview
2. When to Use
3. Inputs
4. Process (with ✅ checkpoints)
5. Output
6. Rationalizations (anti-rationalization table)
7. Red Flags
8. Verification (evidence required)

## Install Methods

```text
# Claude Code — local plugin dir
git clone <repo> && claude --plugin-dir /path/to/tech-advisor

# Gemini CLI
gemini skills install ./skills/

# Manual (any agent)
Paste skills/tech-advisor/SKILL.md as system instructions or project rules.
```

## Connector Layering

Connector/MCP behavior is defined once in `references/connector-detection.md`. Each provider plugs its own MCP/connector model underneath it:

| Provider | Connector support |
| --- | --- |
| Claude Code | MCP |
| Cursor | MCP |
| OpenCode | MCP |
| Windsurf | MCP |
| Kiro | MCP |
| Gemini CLI | Depends on environment |
| GitHub Copilot | Connector dependent |
| Codex | Connector dependent |

Regardless of connector support, the **Fallback Rule** guarantees copy/paste always works.

## Versioning Note

Antigravity, OpenCode, and Kiro folder conventions are newer and may change. Because stubs are trivial and reference-only, re-pointing them is a one-line edit — keep them minimal.
