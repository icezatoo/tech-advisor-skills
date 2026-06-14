---
description: Tech Advisor — recommend a full technology stack for a project or feature
---

# /tech-advisor:stack

Run the **tech-advisor** skill in `stack` mode. Canonical logic lives in `skills/tech-advisor/SKILL.md`; subcommand spec in `skills/tech-advisor/commands/stack.md` — load and follow both.

Break the project into layers (frontend, backend/API, data, auth, infra, observability, testing) and recommend a coherent, scored stack with alternatives. Respect any stated existing stack. Accepts connected or direct input.

Arguments: `$ARGUMENTS`
