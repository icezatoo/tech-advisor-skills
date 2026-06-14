# Example: Frontend Feature

**Input**
```text
/tech-advisor:analyze

Add a data table with server-side pagination, sorting, and filtering
to our React app. Needs to stay fast with 10k+ rows.
```

**Output**

# Tech Advisor Report

## Source
Direct Input

## Task Type
Feature / Frontend

## Summary
Add a performant React data table with server-side pagination, sorting, and filtering that scales to large datasets.

## Technical Needs
- Server-driven pagination/sort/filter
- Efficient rendering for large lists
- Type-safe data fetching + caching
- Accessible table semantics

## Recommended Technologies

| Category | Tool | Score | Comment |
|---|---|---:|---|
| Table | TanStack Table | 9/10 | Headless, server-side mode, a11y-friendly |
| Data fetching | TanStack Query | 9/10 | Caching, pagination, request dedup |
| Virtualization | TanStack Virtual | 8/10 | Render only visible rows |
| Validation | Zod | 8/10 | Validate API responses |

## Why These Tools
TanStack Table is headless (you own markup/styles) and supports manual/server-side pagination. TanStack Query handles caching and keeps server state in sync. Virtualization keeps the DOM small at 10k+ rows.

## Popularity Analysis

| Tool | Popularity | Maintenance | Community | Comment |
|---|---|---|---|---|
| TanStack Table | High | Active | Strong | Standard React table |
| TanStack Query | High | Active | Strong | Standard server-state lib |

## Suggested Plan Enhancements
1. Define a typed query contract (page, sort, filter) with Zod.
2. Use TanStack Query for fetching + keep-previous-data on page change.
3. Configure TanStack Table in manual (server-side) mode.
4. Add virtualization once row counts are large.
5. Ensure accessible table semantics and keyboard nav.
6. Add component tests + a perf check at 10k rows.

## Risks
- Over-fetching if filters aren't debounced.
- Virtualization complicates a11y/focus — test it.
- Server must support the pagination/sort/filter contract.

## Alternatives

| Tool | When to Use |
|---|---|
| AG Grid | When you need an all-in-one enterprise grid out of the box |
| Plain table + manual logic | For small datasets where libraries are overkill |

## Final Recommendation
TanStack Table + Query (+ Virtual for large sets) gives a fast, type-safe, accessible table you fully control. Reach for AG Grid only if you need heavy built-in features and accept the bundle/licensing trade-offs.
