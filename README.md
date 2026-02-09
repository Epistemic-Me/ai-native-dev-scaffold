# AI-Native Development Scaffold

A project scaffold for AI-native software development with Claude Code. This repository provides documentation structures, decision records, and Claude commands that enable effective human-AI collaboration on software projects.

## What's Included

```
ai-native-dev-scaffold/
├── .claude/
│   └── commands/
│       ├── project/           # PR lifecycle and decision workflow commands
│       │   ├── start-pr.md       # /project:start-pr - Create branch + paper trail
│       │   ├── implement-pr.md   # /project:implement-pr - Execute from PLAN.md
│       │   ├── verify-pr.md      # /project:verify-pr - Run verification checks
│       │   ├── close-pr.md       # /project:close-pr - Merge PR + complete docs
│       │   ├── execute-pr.md     # /project:execute-pr - Full lifecycle orchestrator
│       │   ├── pr-status.md      # /project:pr-status - PR progress view
│       │   ├── decision.md       # /project:decision - Create ADR
│       │   ├── context-update.md # /project:context-update - Update living context
│       │   └── context-status.md # /project:context-status - Documentation health
│       ├── hl/                # Advanced workflow commands (22 commands)
│       │   ├── create_plan.md         # /hl:create_plan - Interactive plan creation
│       │   ├── create_plan_nt.md      # /hl:create_plan_nt - Lightweight plan (no docs/)
│       │   ├── implement_plan.md      # /hl:implement_plan - Execute plans
│       │   ├── iterate_plan.md        # /hl:iterate_plan - Update existing plans
│       │   ├── iterate_plan_nt.md     # /hl:iterate_plan_nt - Lightweight iteration
│       │   ├── validate_plan.md       # /hl:validate_plan - Verify implementation
│       │   ├── execute_pr.md          # /hl:execute_pr - Implement from PR paper trail
│       │   ├── oneshot.md             # /hl:oneshot - Research + plan in one go
│       │   ├── oneshot_plan.md        # /hl:oneshot_plan - Research + plan + implement
│       │   ├── commit.md              # /hl:commit - Git commits with branch safety
│       │   ├── ci_commit.md           # /hl:ci_commit - Non-interactive commits
│       │   ├── describe_pr.md         # /hl:describe_pr - PR descriptions
│       │   ├── ci_describe_pr.md      # /hl:ci_describe_pr - Non-interactive PR desc
│       │   ├── describe_pr_nt.md      # /hl:describe_pr_nt - Lightweight PR desc
│       │   ├── debug.md               # /hl:debug - Debug issues
│       │   ├── research_codebase.md   # /hl:research_codebase - Research + doc gen
│       │   ├── research_codebase_generic.md  # Deep research with sub-agents
│       │   ├── research_codebase_nt.md       # Lightweight inline research
│       │   ├── local_review.md        # /hl:local_review - Review PRs locally
│       │   ├── founder_mode.md        # /hl:founder_mode - Rapid development
│       │   ├── create_handoff.md      # /hl:create_handoff - Session handoffs
│       │   └── resume_handoff.md      # /hl:resume_handoff - Resume handoffs
│       └── shared/            # Shared utilities
├── docs/
│   ├── .context/              # Living project context
│   │   ├── ACTIVE_PRS.md      # Currently open PRs
│   │   └── RECENT_DECISIONS.md # Recent architectural decisions
│   ├── decisions/             # Architecture Decision Records (ADRs)
│   │   ├── _INDEX.md          # Decision catalog
│   │   └── _TEMPLATE.md       # ADR template
│   ├── handoffs/              # Session handoff documents
│   ├── plans/                 # Implementation plans
│   ├── research/              # Codebase research documents
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

### PR Lifecycle Commands

#### `/project:start-pr [number] [slug]`

Creates feature branch and paper trail folder:
- Creates `git checkout -b feature/pr-{num}-{slug}`
- Creates `docs/prs/{date}-PR-{num}-{slug}/` with RESEARCH.md, PLAN.md, IMPLEMENTATION.md
- Updates ACTIVE_PRS.md and commits paper trail

Example: `/project:start-pr 042 user-authentication`

#### `/project:implement-pr [number]`

Executes implementation from PLAN.md with structured tracking:
- Ensures correct feature branch
- Parses tasks from PLAN.md into TodoWrite
- Implements phase by phase with progress updates
- Tracks deviations in IMPLEMENTATION.md
- Prompts for verification when complete

Example: `/project:implement-pr 042`

#### `/project:verify-pr [number]`

Runs all available project verification checks:
- Auto-detects available tools (lint, typecheck, test, build)
- Works with any project type (Node, Python, Rust, etc.)
- Reports results table with pass/fail status
- Blocks PR closure on failures

Example: `/project:verify-pr 042`

#### `/project:close-pr [number]`

Merges GitHub PR and completes documentation:
- Merges via `gh pr merge --squash --delete-branch`
- Checks out main and pulls
- Completes IMPLEMENTATION.md with learnings
- Moves PR to "Recently Merged" in ACTIVE_PRS.md
- Checks for architectural decisions, prompts ADR creation
- Commits documentation updates

Example: `/project:close-pr 042`

#### `/project:execute-pr [number]`

**Master orchestrator** - runs the complete PR lifecycle:
1. Initialization (start-pr if needed)
2. Implementation (implement-pr)
3. Verification (verify-pr)
4. Push & Create GitHub PR
5. User approval gate
6. Merge & Close (close-pr with ADR checks)
7. Context update (context-update)
8. Final report

Supports `--skip-start`, `--skip-verify`, `--auto-merge`, `--dry-run` flags.

Example: `/project:execute-pr 042`

#### `/project:pr-status [number]`

Quick view of PR progress:
- Detects active PR or accepts number
- Shows task completion, phase, verification status
- Suggests next action and relevant commands

Example: `/project:pr-status 042`

### Documentation Commands

#### `/project:decision [slug]`

Creates Architecture Decision Record:
- Auto-numbers based on existing ADRs
- Creates from template with PR reference and "Related" section
- Updates `_INDEX.md` and `RECENT_DECISIONS.md`
- Prompts to fill Context/Decision sections

Example: `/project:decision api-versioning-strategy`

#### `/project:context-update`

Refreshes living context files:
- Gathers data from git log, branches, open PRs
- Updates ACTIVE_PRS.md with current PR state
- Updates RECENT_DECISIONS.md with recent ADRs
- Flags staleness and documentation gaps

#### `/project:context-status`

Documentation health report:
- Checks `.context/` file freshness (flags >7 days stale)
- Verifies PR paper trails exist for open PRs
- Checks decision index consistency
- Presents structured health report with recommendations

## Advanced Workflow Commands (`/hl:*`)

These commands provide powerful workflows for complex development tasks. Many are sourced from the [HumanLayer](https://github.com/humanlayer/humanlayer) project and adapted for this scaffold.

### Planning Commands

#### `/hl:create_plan [task-file]`

Create a detailed implementation plan through interactive research (uses opus model):
- Researches codebase using parallel sub-agents (codebase-locator, codebase-analyzer, etc.)
- Presents design options with trade-offs
- Writes phased plan with automated + manual success criteria
- Saves to `docs/plans/` or `docs/prs/.../PLAN.md`

#### `/hl:create_plan_nt [task-file]`

Lightweight variant - no docs/ directory required. Plans written to user-specified location or presented inline.

#### `/hl:implement_plan [plan-path]`

Execute an approved plan with branch safety enforcement:
- Follows plan phase by phase with verification
- Pauses for manual testing between phases
- Updates checkboxes as work progresses

#### `/hl:iterate_plan [plan-path] [feedback]`

Update an existing plan based on feedback (uses opus model):
- Surgical edits to specific sections
- Spawns research only when needed

#### `/hl:iterate_plan_nt [plan-path] [feedback]`

Lightweight variant - no docs/ directory required.

#### `/hl:validate_plan [plan-path]`

Validate implementation matches plan:
- Runs all automated verification
- Identifies deviations
- Generates validation report

#### `/hl:execute_pr [number]`

Implement from PR paper trail (RESEARCH.md + PLAN.md).

#### `/hl:oneshot [task-file]`

Quick research-to-planning pipeline - reads a task, does focused research, creates a plan in one flow.

#### `/hl:oneshot_plan [task-file]`

End-to-end: research, plan, and implement in one session. Best for small-to-medium tasks.

### Git & PR Commands

#### `/hl:commit`

Create git commits with user approval and branch safety enforcement:
- Groups related changes into atomic commits
- Enforces PR workflow (never commits to master/main)

#### `/hl:ci_commit`

Non-interactive commit for CI/automated workflows:
- Same quality as `/hl:commit` but doesn't pause for user feedback

#### `/hl:describe_pr [number]`

Generate PR description with paper trail integration:
- Checks for PR templates and paper trail docs
- Analyzes diff and runs verification
- Updates PR on GitHub

#### `/hl:ci_describe_pr [number]`

Non-interactive PR description for CI workflows.

#### `/hl:describe_pr_nt [number]`

Lightweight PR description - no docs/ directory required.

### Research & Debug Commands

#### `/hl:research_codebase`

Comprehensive codebase research with document generation (uses opus model):
- Spawns parallel sub-agents for efficient research
- Generates research document to `docs/research/`
- Documents what IS, not what SHOULD BE

#### `/hl:research_codebase_generic`

Most thorough research variant - aggressive agent deployment with detailed output.

#### `/hl:research_codebase_nt`

Lightweight research - findings presented inline, no file generation.

#### `/hl:debug`

Debug issues by investigating logs and code (read-only investigation).

### Review

#### `/hl:local_review [pr-number]`

Review a colleague's PR locally:
- Analyzes diff and CI status
- Presents structured review with findings
- Can post review to GitHub

### Session Continuity

#### `/hl:create_handoff`

Create handoff document with YAML frontmatter for session transfer.

#### `/hl:resume_handoff [path]`

Resume from handoff - validates state, creates action plan, continues work.

### Special Modes

#### `/hl:founder_mode`

Rapid experimental development:
- Bias toward action over planning
- Makes assumptions instead of asking
- Still enforces branch safety and PRs

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
