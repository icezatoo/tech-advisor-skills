---
name: tech-advisor
description: Analyze requirements, plans, Jira tickets, and bug reports to recommend modern technologies, libraries, frameworks, and engineering practices. Connector-aware and works offline via copy/paste.
---

# Tech Advisor

## Overview

Tech Advisor is a **Technology Decision Enhancement Skill**. It behaves like an AI Tech Lead.

Given a requirement, implementation plan, Jira ticket, bug report, or pasted text, it:

1. Detects the input source (direct or connected).
2. Classifies the task type.
3. Detects missing technical needs.
4. Recommends modern and popular tools — with scores.
5. Adds popularity and maintenance analysis.
6. Adds risk analysis and alternatives.
7. **Enhances the original plan without replacing it.**

It does not just say "Use Resty." It says *why*, *with what caveats*, and *what to use instead*.

## When to Use

Use this skill when the user:

- Provides a requirement, feature request, or bug report.
- Provides an implementation plan or bugfix plan.
- References a Jira ticket, GitHub/GitLab issue, Confluence page, or similar.
- Asks what framework, library, or tool should be used.
- Wants modern and popular technology recommendations.

## Inputs

Tech Advisor accepts two **categories** of input. See `references/connector-detection.md` for the full resolution flow.

### Direct sources (no connector required)
Requirement · feature request · bug report · implementation plan · architecture doc · markdown file · PRD · ECC/Claude/Cursor/Gemini plan · pasted ticket text.

### Connected sources (fetched via MCP / connectors)
Jira · Confluence · GitHub Issues · GitLab Issues · Linear · Notion · Azure DevOps · custom MCP sources.

> **Core principle:** Tech Advisor must remain fully usable without any connector. If a connector is missing, fall back to copy/paste mode — never fail.

## Process

Run the **connector-aware detection flow** first, then the analysis workflow.

### A. Connector-Aware Detection (always first)

1. **Detect input type** — match against the source-detection patterns in `references/connector-detection.md` (e.g. `OAPI-12345` → Jira key, `github.com/*/issues/*` → GitHub issue, markdown heading → document).
2. **Determine connector access** — check for available MCP resources / connectors (`jira`, `confluence`, `github`, `gitlab`, `notion`, …).
3. **If a matching connector is available** → fetch the source automatically.
4. **If not available** → request direct input using the templated fallback message.
5. **Continue** to analysis with whatever content was obtained.

> ✅ Checkpoint: You must have the actual content (summary/description/acceptance/plan text) before scoring anything. Do not invent ticket contents.

### B. Analysis Workflow

1. Identify the input source. *(Source field)*
2. Extract a task summary. *(Summary field)*
3. Classify the task type. *(Task Type field)*
4. Detect technical needs. *(Technical Needs field)*
5. Recommend tools — score each with `references/scoring-rule.md`.
6. Check popularity and maintenance with `references/popularity-criteria.md`.
7. Add risk analysis with `references/risk-checklist.md`.
8. Add alternatives.
9. Enhance the original plan (add to it; never replace it).
10. Provide a final recommendation.

> ✅ Checkpoint: Connected input and direct input must produce the **same** report quality.

## Output

Always return, in this order:

- **Source** — Direct Input / Jira / GitHub / Confluence / Existing Plan
- **Task Type** — Feature / Bugfix / Refactor / Performance / Security / DevOps / Frontend / Backend
- **Summary**
- **Technical Needs**
- **Recommended Technologies** (table: Category · Tool · Score · Comment)
- **Why These Tools**
- **Popularity Analysis** (table: Tool · Popularity · Maintenance · Community · Comment)
- **Suggested Plan Enhancements**
- **Risks**
- **Alternatives** (table: Tool · When to Use)
- **Final Recommendation**

Use the exact template shown in `examples/` for formatting.

## Rationalizations

| Excuse | Response |
| --- | --- |
| "This is just a small bugfix." | Small changes still need correct tool selection if they affect reliability. |
| "Use the most popular tool." | Popularity is not enough. Fit, maintenance, security, and existing stack must be checked. |
| "No need to mention risks." | Every recommendation must include risks and alternatives. |
| "The plan already exists." | The skill enhances the plan. It must not replace the original plan. |
| "No Jira connector, so I can't analyze." | Fall back to copy/paste. The skill must never fail because a connector is missing. |

## Red Flags

Stop and warn if:

- Recommendation ignores the existing stack.
- Tool is deprecated or unmaintained.
- Tool adds unnecessary complexity.
- Popularity is claimed without confidence.
- A security-sensitive task has no security recommendation.
- A bugfix with an external call has no timeout or retry consideration.
- A production feature has no testing or observability suggestion.
- You fabricated ticket/issue content instead of fetching it or asking for it.

## Verification

Before final output, verify:

- [ ] Recommendation fits the existing stack.
- [ ] Each tool is relevant to the task.
- [ ] Popularity claims are not overconfident (backed by `popularity-criteria.md`).
- [ ] Risks **and** alternatives are included.
- [ ] The original plan was enhanced, not replaced.
- [ ] A final recommendation comment is included.
- [ ] The report is identical in quality whether input came from a connector or copy/paste.

## Commands

- `analyze` — primary; analyze any direct or connected source → full report. See `commands/analyze.md`.
- `compare` — compare 2+ tools head-to-head. See `commands/compare.md`.
- `stack` — recommend a full stack for a project. See `commands/stack.md`.
- `explain` — explain a single tool or decision in depth. See `commands/explain.md`.

## References

- `references/connector-detection.md` — connector/MCP discovery, source detection, Jira input modes.
- `references/multi-agent-support.md` — portability contract across agents/providers.
- `references/scoring-rule.md` — the 1–10 scoring rubric.
- `references/popularity-criteria.md` — how popularity/maintenance is judged.
- `references/risk-checklist.md` — risk and red-flag checklist.
- `references/tech-catalog.md` — curated catalog of modern tools by category.
