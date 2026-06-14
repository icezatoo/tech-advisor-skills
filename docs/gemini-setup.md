# Gemini CLI Setup

## Install
```bash
gemini skills install ./skills/
```
Or paste `skills/tech-advisor/SKILL.md` into your Gemini project rules / system instructions.

The Gemini command stub is `.gemini/commands/tech-advisor.md` and points to the canonical skill.

## Use
```text
/tech-advisor analyze <ticket | url | pasted content>
/tech-advisor compare <toolA> vs <toolB>
/tech-advisor stack <project description>
/tech-advisor explain <tool | pattern>
```

## Connectors / MCP
Gemini connector/MCP support depends on your environment. Tech Advisor detects what's available and otherwise falls back to copy/paste. See `skills/tech-advisor/references/connector-detection.md`.
