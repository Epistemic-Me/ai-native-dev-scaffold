# Claude Code Project Context

This file provides guidance to Claude Code instances when working with projects using this scaffold.

## Philosophy

This scaffold enables AI-native software development through:

1. **Paper Trails Over Comments** - Living documentation that captures research, planning, and implementation
2. **Decisions as First-Class Citizens** - ADRs that document why, not just what
3. **AI as Collaborator** - Commands that automate documentation scaffolding

## Project Structure

```
your-project/
├── .claude/
│   └── commands/
│       └── project/           # PR and decision commands
├── docs/
│   ├── .context/              # Living project context
│   │   ├── ACTIVE_PRS.md      # Currently open PRs
│   │   └── RECENT_DECISIONS.md # Recent architectural decisions
│   ├── decisions/             # Architecture Decision Records
│   │   ├── _INDEX.md          # Decision catalog
│   │   └── _TEMPLATE.md       # ADR template
│   └── prs/                   # PR paper trails
│       └── _TEMPLATE/         # Template PR folder
├── CLAUDE.md                  # This file
└── ... your code ...
```

## Available Commands

### `/project:start-pr {number} {slug}`

Creates a new PR paper trail folder with:
- `RESEARCH.md` - Problem exploration and options analysis
- `PLAN.md` - Implementation strategy and scope
- `IMPLEMENTATION.md` - What was actually built

Example: `/project:start-pr 042 user-authentication`

### `/project:close-pr {number}`

Completes PR documentation:
- Ensures all sections are filled
- Moves PR from active to merged
- Prompts for ADR creation if decisions were made

Example: `/project:close-pr 042`

### `/project:decision {slug}`

Creates a new Architecture Decision Record:
- Auto-numbers based on existing ADRs
- Updates the decision index

Example: `/project:decision api-versioning-strategy`

## Workflow

### Starting Work on a Feature

1. **Create PR paper trail**: `/project:start-pr {num} {slug}`
2. **Research phase**: Fill in RESEARCH.md with problem statement and options
3. **Planning phase**: Fill in PLAN.md with chosen approach and scope
4. **Implementation**: Write code, update IMPLEMENTATION.md as you go
5. **Close PR**: `/project:close-pr {num}` when merged

### Making Architectural Decisions

1. When you identify a significant decision, use `/project:decision {slug}`
2. Fill in context, options considered, and consequences
3. Link from PR paper trail if related to current work

## Documentation Patterns

### When to Create ADRs

- Choosing between competing technologies
- Establishing patterns for the codebase
- Making trade-offs that affect the system
- Decisions that future developers will question

### When to Use PR Paper Trails

- Any PR that takes more than a day
- Complex features or refactors
- Work that involves research or options
- Changes that need to be understood later

## Best Practices for AI Collaboration

### Context Maintenance

- Keep `docs/.context/` files updated
- Reference ADRs when making related decisions
- Link PR paper trails in PR descriptions

### Documentation Quality

- Fill in RESEARCH.md before coding
- Update PLAN.md when scope changes
- Complete IMPLEMENTATION.md with learnings

### Decision Hygiene

- One decision per ADR
- Update status as decisions evolve
- Supersede rather than delete old decisions
