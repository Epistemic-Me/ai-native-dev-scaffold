# Context Status

Get a quick overview of current project context.

## When to Use

Run this to understand:
- What PRs are currently in progress
- Recent architectural decisions
- Current project state

Example usage: `/project:context-status`

## Instructions

1. **Read current context files**:
   - `docs/.context/ACTIVE_PRS.md`
   - `docs/.context/RECENT_DECISIONS.md`

2. **Summarize open PRs**:
   - List each open PR with its status
   - Note which ones have incomplete documentation

3. **Summarize recent decisions**:
   - List last 5 decisions
   - Note any pending or under-review decisions

4. **Check for issues**:
   - Stale PRs (open for >2 weeks)
   - Missing paper trails
   - Decisions needing follow-up

5. **Present summary** in a clear format:

```
## Current Context

### Open PRs ({count})
- PR #{num}: {title} - {status}

### Recent Decisions ({count})
- ADR-{num}: {title} - {status}

### Action Items
- {Any issues found}
```
