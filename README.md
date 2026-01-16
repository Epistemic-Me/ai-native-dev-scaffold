# AI-Native Development Scaffold

A project scaffold for AI-native software development with Claude Code. This repository provides documentation structures, decision records, and Claude commands that enable effective human-AI collaboration on software projects.

## What's Included

```
ai-native-dev-scaffold/
├── .claude/
│   └── commands/
│       └── project/           # Claude slash commands
│           ├── start-pr.md    # /project:start-pr - Create PR paper trail
│           ├── close-pr.md    # /project:close-pr - Complete PR documentation
│           └── decision.md    # /project:decision - Create ADR
├── docs/
│   ├── .context/              # Living project context
│   │   ├── ACTIVE_PRS.md      # Currently open PRs
│   │   └── RECENT_DECISIONS.md # Recent architectural decisions
│   ├── decisions/             # Architecture Decision Records (ADRs)
│   │   ├── _INDEX.md          # Decision catalog
│   │   └── _TEMPLATE.md       # ADR template
│   └── prs/                   # PR paper trails
│       └── _TEMPLATE/         # Template PR folder
│           ├── RESEARCH.md    # Problem exploration & options
│           ├── PLAN.md        # Implementation strategy
│           └── IMPLEMENTATION.md # What was actually built
└── CLAUDE.md                  # Project instructions for Claude
```

## Philosophy

### Paper Trails Over Comments

Instead of inline comments that rot, we maintain living documentation:

- **RESEARCH.md** - Why are we doing this? What options did we consider?
- **PLAN.md** - How will we implement it? What's in/out of scope?
- **IMPLEMENTATION.md** - What did we actually build? What did we learn?

### Decisions Are First-Class

Every significant technical decision gets an ADR:

- Captures context at decision time
- Documents alternatives considered
- Explains trade-offs made
- Linkable from code and PRs

### AI as Collaborator

The `.claude/commands/` folder contains slash commands that:

- Automate documentation scaffolding
- Enforce consistent structure
- Reduce friction in the development process

## Getting Started

### 1. Clone this scaffold

```bash
git clone https://github.com/yourusername/ai-native-dev-scaffold.git my-project
cd my-project
rm -rf .git
git init
```

### 2. Install Claude commands

Copy the `.claude/commands/project/` folder to your global Claude config:

```bash
cp -r .claude/commands/project ~/.claude/commands/
```

Or keep them project-local by leaving them in `.claude/commands/`.

### 3. Start using the commands

```bash
# Starting a new PR
/project:start-pr 001 initial-setup

# Recording a decision
/project:decision authentication-strategy

# Completing a PR
/project:close-pr 001
```

## Commands Reference

### `/project:start-pr [number] [slug]`

Creates a new PR paper trail folder with:
- `RESEARCH.md` - Template for problem exploration
- `PLAN.md` - Template for implementation planning
- `IMPLEMENTATION.md` - Template for tracking what was built

Example: `/project:start-pr 042 user-authentication`

### `/project:close-pr [number]`

Completes PR documentation:
- Ensures all sections are filled
- Updates status to "Complete"
- Moves PR from active to merged in tracking docs
- Prompts for ADR creation if decisions were made

Example: `/project:close-pr 042`

### `/project:decision [slug]`

Creates a new Architecture Decision Record:
- Auto-numbers based on existing ADRs
- Creates from standard ADR template
- Updates the decision index

Example: `/project:decision api-versioning-strategy`

## ADR Format

Architecture Decision Records follow this structure:

```markdown
# ADR-XXX: Title

**Date**: YYYY-MM-DD
**Status**: Proposed | Accepted | Deprecated | Superseded

## Context
What issue motivates this decision?

## Decision
What are we doing?

## Consequences
### Positive
### Negative

## Alternatives Considered
What else did we evaluate?
```

## PR Paper Trail Format

Each PR gets a folder with three documents:

### RESEARCH.md
- Problem statement
- Context gathered (existing code, related work)
- Options considered with pros/cons
- Recommendation

### PLAN.md
- Chosen approach
- Scope (in/out)
- Technical design
- Implementation order
- Testing strategy

### IMPLEMENTATION.md
- Summary of what was built
- Key changes
- Deviations from plan
- Learnings
- Follow-up items

## Best Practices

### When to Create an ADR

- Choosing between technologies
- Establishing patterns for the codebase
- Making trade-offs that affect the system
- Decisions that future developers will question

### When to Use PR Paper Trails

- Any PR that takes more than a day
- Complex features or refactors
- Work that involves research or options
- Changes that need to be understood later

### Keeping Docs Current

- Update `ACTIVE_PRS.md` when starting/closing PRs
- Review `RECENT_DECISIONS.md` periodically
- Link from code to relevant ADRs
- Reference PR paper trails in PR descriptions

## Contributing

This is an open scaffold - please contribute improvements:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## License

MIT License - Use freely in your projects.

---

*Built for AI-native development with Claude Code*
