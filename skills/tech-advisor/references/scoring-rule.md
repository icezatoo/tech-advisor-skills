# Scoring Rule

Every recommended tool gets a **score out of 10**. Scores are evidence-based, not vibes. Be conservative — a score above 8 is a strong claim.

## Dimensions (weighted)

| Dimension | Weight | What it measures |
| --- | --- | --- |
| Fit | 30% | How directly the tool solves the detected technical need |
| Maintenance | 20% | Active releases, responsive maintainers, no abandonment |
| Adoption | 15% | Real-world production usage and community size |
| Stability / Maturity | 15% | API stability, breaking-change history, battle-tested |
| Security | 10% | CVE history, supply-chain hygiene, secure defaults |
| Ecosystem fit | 10% | Works with the existing stack, language, and tooling |

## Computing the score

1. Rate each dimension 0–10.
2. Multiply by weight, sum → weighted score (0–10).
3. Round to the nearest whole number for the table; keep one decimal if it changes the recommendation.

## Bands

| Score | Meaning |
| --- | --- |
| 9–10 | Strong default. Mature, maintained, ideal fit. |
| 7–8 | Solid choice with minor caveats. |
| 5–6 | Workable but with real trade-offs — explain them. |
| 3–4 | Use only with specific justification. |
| 0–2 | Avoid / deprecated / poor fit. |

## Rules

- Never give a score without naming the dominant dimension that drove it.
- If a tool scores high on Adoption but low on Maintenance, the **lower** dimension caps confidence — say so.
- A tool you cannot verify the maintenance status of caps at **7** with an explicit "verify currency" note.
- Two tools within 1 point are effectively tied → present both and let the team choose on a secondary axis (deps, license, team familiarity).
