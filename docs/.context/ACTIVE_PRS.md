# Active PRs

Living document tracking currently open pull requests and their status.

## Open PRs

| PR | Title | Started | Paper Trail | Status |
|----|-------|---------|-------------|--------|
| <!-- PRs will be added here by /start-pr --> |

## Recently Merged

| PR | Title | Merged | Paper Trail |
|----|-------|--------|-------------|
| <!-- Merged PRs will be moved here by /review-pr --> |

## How to Use

### Starting a PR
```
/project:start-pr {number} {slug}
```
Creates a paper trail folder and adds an entry here.

### Closing a PR
```
/project:review-pr {number}
```
When approved: merges, moves PR from "Open" to "Recently Merged", archives docs.

## Paper Trail Location

All PR documentation lives in `docs/prs/{lifecycle}/{date}-PR-{num}-{slug}/`:
- `RESEARCH.md` — Problem exploration and options
- `TEST-STRATEGY.md` — Acceptance criteria and test matrix
- `IMPLEMENTATION-PLAN.md` — Step-by-step implementation plan
- `IMPLEMENTATION.md` — What was actually built
