# Antigravity Setup

[Antigravity](https://antigravity.google/) is Google's agentic IDE (Gemini-powered). Tech Advisor ships an Antigravity entry point and, because the skill is plain Markdown, also works via a copy/paste fallback.

> **Path note:** The slash-command location below (`commands/`) follows the convention used by [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills). If your Antigravity version expects a different location, the stub is a ≤15-line file that only points to the canonical skill, so re-pointing it is a one-line change. The fallback (Option B) works regardless.

## Option A — Slash command stub

The entry point is:

```text
commands/tech-advisor.md   →  points to skills/tech-advisor/SKILL.md
```

Keep `skills/tech-advisor/` in your workspace so the stub can reference the canonical logic and references. Invoke with:

```text
/tech-advisor:analyze <ticket | url | pasted content>
/tech-advisor:compare <toolA> vs <toolB>
/tech-advisor:stack <project description>
/tech-advisor:explain <tool | pattern>
```

## Option B — Manual (always works)

Paste the contents of `skills/tech-advisor/SKILL.md` into Antigravity's system instructions or workspace rules. Then ask naturally, e.g. "Analyze this ticket and recommend a stack." Tech Advisor returns the full report (Source → Final Recommendation).

## Connectors / MCP

Antigravity is Gemini-based, so connector/MCP availability is **environment-dependent** (same bucket as Gemini CLI in `provider-compatibility.md`). Tech Advisor detects whatever is available and otherwise falls back to copy/paste — it never fails because a connector is missing. See `skills/tech-advisor/references/connector-detection.md`.

## Verify the convention

Antigravity's skill/command format is still evolving. If `/tech-advisor` isn't picked up, confirm the expected command directory in the current Antigravity docs and move `commands/tech-advisor.md` accordingly (or use Option B). The canonical logic in `skills/tech-advisor/SKILL.md` does not change.
