# GEMINI.md

Guidance for using **tech-advisor** with Gemini CLI.

## Canonical source

```text
skills/tech-advisor/SKILL.md
```

Load this as the source of truth. The Gemini entry point is `.gemini/commands/tech-advisor.md` (a stub that points here).

## Install

```bash
gemini skills install ./skills/
```

Or paste `skills/tech-advisor/SKILL.md` into your Gemini project rules / system instructions.

## Usage

```text
/tech-advisor:analyze <ticket | url | pasted content>
/tech-advisor:compare <toolA> vs <toolB>
/tech-advisor:stack <project description>
/tech-advisor:explain <tool | pattern>
```

## Connector note

Gemini connector/MCP availability depends on your environment. Tech Advisor detects what's available and otherwise falls back to copy/paste — it never fails because a connector is missing. See `skills/tech-advisor/references/connector-detection.md`.
