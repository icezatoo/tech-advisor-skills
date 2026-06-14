# Popularity Criteria

Popularity is a **signal, not a verdict**. A tool is not "good" because it has stars. This file defines what Tech Advisor actually inspects, and the honesty rules for claiming it.

## Signals (in priority order)

1. **Maintenance cadence** — recent releases, commit recency, issue/PR responsiveness. *Most important.*
2. **Community size & activity** — contributors, discussion volume, real production case studies.
3. **Ecosystem integration** — first-class support in major frameworks/platforms; well-maintained adapters.
4. **Documentation quality** — current docs, examples, migration guides.
5. **Security posture** — CVE history and response time, dependency hygiene.
6. **Raw stars / downloads** — *weakest* signal; easily gamed and lagging. Use only as a tiebreaker.

## Rating scale

| Rating | Popularity | Maintenance | Community |
| --- | --- | --- | --- |
| High | Widely used in production | Frequent releases, active | Large, responsive |
| Medium | Used but niche | Periodic updates | Moderate |
| Low | Rare or declining | Infrequent / stale | Small or quiet |

## Honesty rules (anti-overconfidence)

- Never claim "most popular" without a comparator and a signal. Prefer "widely adopted for X".
- If you cannot verify current maintenance, say **"popularity claim unverified — confirm before adopting"** instead of asserting High.
- Flag a tool as a **Red Flag** if maintenance looks stale (no release in a long time, archived repo, unanswered security issues).
- Popularity never overrides Fit, Security, or existing-stack constraints. A popular tool that doesn't fit is still the wrong tool.
