# Start PR

Create paper trail folder for a new PR.

## Arguments

The user should provide:
- PR number (e.g., "142")
- Short slug describing the PR (e.g., "belief-extraction")

Example usage: `/project:start-pr 142 belief-extraction`

## Instructions

1. **Get today's date** in YYYY-MM-DD format

2. **Create PR folder**:
   ```
   docs/prs/{date}-PR-{num}-{slug}/
   ```
   Example: `docs/prs/2024-12-14-PR-142-belief-extraction/`

3. **Create RESEARCH.md** with this template:

```markdown
# PR #{num}: {slug} - Research

**Created**: {date}
**Author**: @{get from git config}

## Problem Statement

{To be filled: What problem are we solving? Why now?}

## Context Gathered

### Existing Code
- {To be filled: Relevant files and patterns}

### Related Work
- {To be filled: Related PRs, decisions}

### User/Business Context
- {To be filled: Relevant JTBD, user feedback}

## Options Considered

### Option A: {Name}
- **Approach**:
- **Pros**:
- **Cons**:
- **Effort**: {Low|Medium|High}

### Option B: {Name}
- **Approach**:
- **Pros**:
- **Cons**:
- **Effort**:

## Recommendation

{To be filled after research}

## Open Questions

- [ ] {Questions to answer before planning}
```

4. **Create PLAN.md** with this template:

```markdown
# PR #{num}: {slug} - Plan

**Created**: {date}
**Based on**: [RESEARCH.md](./RESEARCH.md)

## Chosen Approach

{To be filled after research complete}

## Scope

### In Scope
-

### Out of Scope
-

## Technical Design

### Changes Required

| File | Change | Why |
|------|--------|-----|
| | | |

### New Files

| File | Purpose |
|------|---------|
| | |

## Implementation Order

1.
2.
3.

## Testing Strategy

- [ ]

## Rollback Plan

{How to revert if needed}

## Definition of Done

- [ ] Code complete
- [ ] Tests passing
- [ ] Documentation updated
- [ ] PR reviewed
```

5. **Create IMPLEMENTATION.md** with this template:

```markdown
# PR #{num}: {slug} - Implementation

**Status**: In Progress
**Based on**: [PLAN.md](./PLAN.md)

## Summary

{To be filled when PR complete}

## Key Changes

### {Component/Area}
-

## Deviations from Plan

| Planned | Actual | Reason |
|---------|--------|--------|
| | | |

## Testing Done

- [ ]

## Learnings

### What Worked Well
-

### What Was Harder Than Expected
-

### What We'd Do Differently
-

## Follow-up Items

- [ ]

---
*PR Merged: {to be filled}*
```

6. **Update ACTIVE_PRS.md**:
   - Add entry for this PR in the "Open PRs" section
   - Include link to paper trail folder

7. **Report to user** what was created
