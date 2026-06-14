# Tech Advisor

A portable, **connector-aware AI Tech Lead** skill. It analyzes requirements, implementation plans, Jira tickets, bug reports, or pasted text and recommends modern, popular technologies — with scores, popularity analysis, risks, and alternatives. It **enhances** your plan; it never replaces it.

Works across Claude Code, Cursor, Gemini CLI, Windsurf, OpenCode, GitHub Copilot, Kiro, Codex, and any Markdown-based agent.

## Why it's different

It doesn't just say *"Use Resty."* It says:

> Use Resty because this task needs HTTP timeout, retry, logging, and testability. It's a practical, popular Go client, but verify retry idempotency and your dependency policy. If avoiding dependencies is required, use net/http.

## Core principles

- **Connector-aware** — detects Jira/Confluence/GitHub/GitLab/Notion/MCP dynamically.
- **Offline-friendly** — always falls back to copy/paste; never fails because a connector is missing.
- **Provider-agnostic** — one canonical `SKILL.md`, thin per-provider entry points.

## Repository layout

```text
tech-advisor-skills/
├── skills/tech-advisor/             # the skill (single source of truth)
│   ├── SKILL.md                     # canonical skill definition
│   ├── commands/                    # analyze · compare · stack · explain
│   ├── references/                  # connector-detection · multi-agent-support
│   │                                # scoring-rule · popularity-criteria
│   │                                # risk-checklist · tech-catalog
│   └── examples/                    # 4 worked Tech Advisor Reports
├── .claude/                         # Claude Code entry points
│   └── commands/
│       ├── tech-advisor.md          # combined router command
│       └── tech-advisor/            # registered sub-commands
│           └── analyze · compare · stack · explain
├── .cursor/ .gemini/                # provider entry points (stubs)
├── .opencode/ .kiro/ commands/      # provider entry points (stubs)
├── .github/copilot-instructions.md  # GitHub Copilot stub
├── AGENTS.md CLAUDE.md GEMINI.md     # agent / project guidance
├── docs/                            # per-tool setup + compatibility matrix
├── plugin.json                      # Claude Code plugin manifest
├── README.md
└── LICENSE                          # MIT
```

## Commands

| Command | Purpose |
|---|---|
| `/tech-advisor:analyze` | Analyze a requirement, plan, ticket, or pasted text → full report |
| `/tech-advisor:compare` | Compare 2+ tools head-to-head |
| `/tech-advisor:stack` | Recommend a full stack for a project |
| `/tech-advisor:explain` | Explain a tool, pattern, or decision in depth |

In Claude Code each sub-command is a **registered slash command** (declared in `plugin.json`), so `analyze`, `compare`, `stack`, and `explain` appear individually in the `/` menu. `/tech-advisor` on its own still works as a combined router.

## Usage

```text
/tech-advisor:analyze OAPI-12345          # connected (Jira)
/tech-advisor:analyze <pasted ticket>     # direct
/tech-advisor:analyze <implementation plan>
```

All three produce the same Tech Advisor Report.

## Install

See [`docs/`](docs/) for per-tool setup. Quick paths:

- **Claude Code:** `claude --plugin-dir /path/to/tech-advisor-skills` (clone the repo first).
- **Cursor:** the rule in `.cursor/rules/tech-advisor.md` points to `skills/tech-advisor/SKILL.md`.
- **Gemini CLI:** `gemini skills install ./skills/`.
- **Any agent:** paste `skills/tech-advisor/SKILL.md` as system instructions.

## Design

The portability contract lives in [`skills/tech-advisor/references/multi-agent-support.md`](skills/tech-advisor/references/multi-agent-support.md), modeled on [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills). Provider files are thin stubs; all logic lives in `SKILL.md` and `references/`.

## License

[MIT](LICENSE).
