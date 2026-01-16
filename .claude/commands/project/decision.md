# Decision

Create a new Architecture Decision Record (ADR).

## Arguments

The user should provide:
- Decision slug (e.g., "api-versioning-strategy")

Example usage: `/project:decision api-versioning-strategy`

## Instructions

1. **Get the next ADR number**:
   - Read `docs/decisions/_INDEX.md`
   - Find the highest ADR number
   - Increment by 1

2. **Get today's date** in YYYY-MM-DD format

3. **Create the ADR file** at `docs/decisions/ADR-{num}-{slug}.md`:

```markdown
# ADR-{num}: {Title from slug}

**Date**: {date}
**Status**: Proposed

## Context

{What is the issue that we're seeing that motivates this decision?}

## Decision

{What is the change that we're proposing and/or doing?}

## Consequences

### Positive
- {Good outcomes}

### Negative
- {Trade-offs and costs}

### Neutral
- {Other notable effects}

## Alternatives Considered

### {Alternative 1}
- **Description**:
- **Pros**:
- **Cons**:
- **Why not chosen**:

### {Alternative 2}
- **Description**:
- **Pros**:
- **Cons**:
- **Why not chosen**:

## References

- {Related PRs, docs, external resources}
```

4. **Update `docs/decisions/_INDEX.md`**:
   - Add new entry to the decision table
   - Include date, title, status, and link

5. **Update `docs/.context/RECENT_DECISIONS.md`**:
   - Add entry to recent decisions list
   - Keep only last 10 decisions in this file

6. **Report to user** what was created
