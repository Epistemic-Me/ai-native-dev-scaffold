# Claude Code Project Context

This file provides guidance to Claude Code instances when working with projects using this scaffold.

## 🚨 MANDATORY: PR Workflow Rules

**NEVER commit directly to master/main.** All code changes MUST follow PR workflow:

### Before ANY Code Changes
1. Check current branch: `git branch --show-current`
2. If on master/main → **STOP** and create feature branch
3. Check for PR: `gh pr view`
4. If no PR → suggest creating draft PR

### During Implementation
- Work only on feature branches
- Commit to feature branch (use `/hl:commit`)
- Push to remote regularly

### Before Merging
- Always require human review
- Never merge without approval
- Use `/project:close-pr` after merge

### Blocked Operations on master/main
- ❌ `git commit` (any form)
- ❌ `git push origin master/main`
- ❌ File edits without branch check

See `.claude/commands/shared/branch-safety.md` for enforcement details.

---

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
│       ├── hl/                # Advanced workflow commands
│       ├── project/           # PR and decision commands
│       └── shared/            # Shared utilities (branch safety)
├── docs/
│   ├── .context/              # Living project context
│   │   ├── ACTIVE_PRS.md      # Currently open PRs
│   │   └── RECENT_DECISIONS.md # Recent architectural decisions
│   ├── decisions/             # Architecture Decision Records
│   │   ├── _INDEX.md          # Decision catalog
│   │   └── _TEMPLATE.md       # ADR template
│   ├── handoffs/              # Session handoff documents
│   ├── plans/                 # Implementation plans
│   ├── prs/                   # PR paper trails
│   │   └── _TEMPLATE/         # Template PR folder
│   └── research/              # Codebase research documents
├── CLAUDE.md                  # This file
└── ... your code ...
```

## Available Commands

### Project Commands (`/project:*`)

#### `/project:start-pr {number} {slug}`

Creates a new PR paper trail folder with:
- `RESEARCH.md` - Problem exploration and options analysis
- `PLAN.md` - Implementation strategy and scope
- `IMPLEMENTATION.md` - What was actually built

Example: `/project:start-pr 042 user-authentication`

#### `/project:close-pr {number}`

Completes PR documentation:
- Ensures all sections are filled
- Moves PR from active to merged
- Prompts for ADR creation if decisions were made

Example: `/project:close-pr 042`

#### `/project:decision {slug}`

Creates a new Architecture Decision Record:
- Auto-numbers based on existing ADRs
- Updates the decision index

Example: `/project:decision api-versioning-strategy`

### Advanced Workflow Commands (`/hl:*`)

#### Planning & Implementation
- `/hl:create_plan` - Create implementation plans through interactive research (model: opus)
- `/hl:create_plan_nt` - Lightweight plan creation, no docs/ directory required (model: opus)
- `/hl:implement_plan` - Execute plans phase by phase with verification
- `/hl:iterate_plan` - Update existing plans based on feedback (model: opus)
- `/hl:iterate_plan_nt` - Lightweight plan iteration, no docs/ directory required (model: opus)
- `/hl:validate_plan` - Verify implementation matches plan
- `/hl:execute_pr` - Implement from PR paper trail
- `/hl:oneshot` - Research ticket and launch planning session
- `/hl:oneshot_plan` - Research, plan, and implement in one session

#### Git & PR
- `/hl:commit` - Create git commits with user approval (enforces branch safety)
- `/hl:ci_commit` - Non-interactive commit for CI/automated workflows
- `/hl:describe_pr` - Generate PR descriptions with paper trail integration
- `/hl:ci_describe_pr` - Non-interactive PR description for CI workflows
- `/hl:describe_pr_nt` - Lightweight PR description, no docs/ required

#### Research & Debug
- `/hl:research_codebase` - Document codebase with research doc generation (model: opus)
- `/hl:research_codebase_generic` - Comprehensive research with parallel sub-agents (model: opus)
- `/hl:research_codebase_nt` - Lightweight research, findings presented inline (model: opus)
- `/hl:debug` - Debug issues by investigating logs and code

#### Review
- `/hl:local_review` - Review a colleague's PR locally with analysis

#### Session Continuity
- `/hl:create_handoff` - Create handoff for another session
- `/hl:resume_handoff` - Resume from handoff document

#### Special Modes
- `/hl:founder_mode` - Rapid experimental development with bias toward action

## Workflow

### Starting Work on a Feature

1. **Create feature branch FIRST**: `git checkout -b feature/pr-{num}-{slug}`
2. **Create PR paper trail**: `/project:start-pr {num} {slug}`
3. **Create draft PR**: `gh pr create --draft --title "WIP: {description}"`
4. **Research phase**: Fill in RESEARCH.md with problem statement and options
5. **Planning phase**: Fill in PLAN.md with chosen approach and scope
6. **Implementation**: Write code on feature branch, update IMPLEMENTATION.md
7. **Commit regularly**: Use `/hl:commit` (enforces branch safety)
8. **Push to remote**: `git push -u origin feature/pr-{num}-{slug}`
9. **Request review**: Mark PR ready when done
10. **Close PR**: `/project:close-pr {num}` after merge

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
