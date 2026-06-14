# Connector Detection Reference

Tech Advisor is **connector-aware**, **MCP-aware**, **provider-agnostic**, and **offline-friendly**. It must adapt to whatever the host environment exposes and must always be usable via copy/paste.

## Connector-Aware Detection Flow

When input is received:

```text
Step 1  Detect input type (see Source Detection Rules).
Step 2  Determine whether connector access exists.
Step 3  If a matching connector is available → fetch the source automatically.
Step 4  If not available → request direct input (use the fallback message).
Step 5  Continue analysis with the obtained content.
```

## Connector Discovery Rules

Before requesting manual input, check for any of these:

```text
Jira connector
Confluence connector
GitHub connector
GitLab connector
Linear connector
Notion connector
MCP resources
```

If none match the detected source, fall back to direct input.

## MCP Support

Tech Advisor supports MCP-based environments (Claude Code MCP, Cursor MCP, OpenCode MCP, custom MCP servers).

Supported MCP resource types:

```text
jira
confluence
github
gitlab
notion
documents
knowledge-base
```

### MCP Discovery Flow

When ticket-like input (e.g. `OAPI-12345`) is detected:

```text
Check available MCP resources.
If a Jira MCP exists      → use Jira MCP.
Else if another connected source exists → use it.
Else                      → fall back to direct input.
```

## Source Detection Rules

| Pattern | Source |
| --- | --- |
| `OAPI-12345` | Jira Ticket |
| `ABC-999` (LETTERS-NUMBERS) | Jira Ticket |
| `*.atlassian.net/browse/*` | Jira URL |
| `*.atlassian.net/wiki/*` | Confluence URL |
| `github.com/*/issues/*` | GitHub Issue |
| `gitlab.com/*/issues/*` | GitLab Issue |
| `linear.app/*/issue/*` | Linear Issue |
| `notion.so/*` | Notion Page |
| Markdown heading (`# ...`) | Document |
| Plain text requirement | Requirement |
| Numbered list of steps | Implementation Plan |

> Detection is a **heuristic**. On ambiguity (e.g. is `ABC-999` really a Jira key?), confirm intent with the user before fetching.

## Connected Source Priority

If multiple connected sources resolve the same input, prefer in this order:

```text
1. Jira Ticket
2. Confluence Page
3. GitHub Issue
4. GitLab Issue
5. Notion Page
6. Direct Input
```

## Jira Input Modes

### Mode 1 — Jira connector available
Input: `/tech-advisor analyze OAPI-12345`

```text
Detect Jira ticket key → check Jira connector → fetch:
  Summary · Description · Acceptance Criteria · Components ·
  Labels · Comments · Linked Issues
→ analyze → generate report.
```

### Mode 2 — Jira URL
Input: `/tech-advisor analyze` + `https://company.atlassian.net/browse/OAPI-12345`

```text
Detect Jira URL.
If connector available → fetch ticket.
Otherwise             → request user to paste content.
```

### Mode 3 — Jira connector NOT available
Input: `/tech-advisor analyze OAPI-12345`

Respond exactly with:

```markdown
Jira ticket detected.

No Jira connector or MCP access is available in the current environment.

Please provide one of the following:

- Jira Summary
- Jira Description
- Acceptance Criteria
- Existing Implementation Plan

Tech Advisor will continue analysis using direct input mode.
```

### Mode 4 — Manual Jira copy/paste
Input:

```markdown
Title: Fix timeout issue
Description: Current HTTP client does not retry.
Acceptance Criteria: Retry should occur 3 times.
```

```text
Treat as Jira content → analyze normally.
```

## Fallback Rule (core design principle)

Tech Advisor must **never** fail because:

```text
Jira not connected · Confluence not connected ·
GitHub not connected · MCP not available
```

Instead, always: **fall back to copy/paste mode.**

## Universal Input Rule

Every analysis command must accept **connected input OR direct input**, and all forms must produce the same Tech Advisor Report:

```text
/tech-advisor analyze OAPI-12345             (connected)
/tech-advisor analyze <jira content>         (direct)
/tech-advisor analyze <implementation plan>  (direct)
```
