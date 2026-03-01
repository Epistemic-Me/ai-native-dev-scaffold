# Claude Code Project Context

This file provides guidance to Claude Code instances when working with projects using this scaffold.

## MANDATORY: PR Workflow Rules

**NEVER commit directly to master/main.** All code changes MUST follow PR workflow.

### Before ANY Code Changes
1. Check current branch: `git branch --show-current`
2. If on master/main → **STOP** and create feature branch
3. Check for PR: `gh pr view`
4. If no PR → suggest creating draft PR

### Blocked Operations on master/main
- `git commit` (any form)
- `git push origin master/main`
- File edits via Edit/Write tools without branch check

See `.claude/commands/shared/branch-safety.md` for enforcement details.

---

## Workflow: Feature to Production

### The Automated Path

For any feature, the master orchestrator handles everything:

```
/project:execute-pr {num}
```

This runs the full lifecycle automatically:

```
start-pr → implement-pr → verify-pr → push → create GH PR → approval gate → close-pr → context-update
```

It pauses at the approval gate for human review before merging. If interrupted, re-running detects existing state and resumes.

### The Manual Path (Step by Step)

**1. Start the PR** — creates feature branch and paper trail:
```
/project:start-pr {num} {slug}
```
Creates `feature/pr-{num}-{slug}` branch and `docs/prs/planning/{date}-PR-{num}-{slug}/` with RESEARCH.md, PLAN.md, IMPLEMENTATION.md.

**2. Research** — understand the problem before coding:
- Fill in RESEARCH.md with problem statement, options considered, recommendation
- Use `/project:research-codebase-nt` to explore the codebase
- Record architectural decisions with `/project:decision {slug}`

**3. Plan** — define the implementation approach:
- Fill in PLAN.md with scope, technical design, implementation order
- Or generate one: `/project:create-plan`
- Revise after feedback: `/project:iterate-plan {path-to-plan} {feedback}`

**4. Implement** — execute the plan with progress tracking:
```
/project:implement-pr {num}
```
Reads PLAN.md, creates TodoWrite tasks, implements phase by phase, updates IMPLEMENTATION.md.

**5. Verify** — run all available checks:
```
/project:verify-pr {num}
```
Auto-detects lint, typecheck, test, build and reports pass/fail. Must pass before merge.

**6. Commit and push**:
```
/project:commit
git push -u origin feature/pr-{num}-{slug}
```

**7. Create/update GitHub PR**:
```
/project:describe-pr {num}
```
Generates PR description from paper trail, analyzes diff, creates/updates PR on GitHub.

**8. Review** — get human approval:
- Have teammate review, or use `/project:local-review {num}` for local analysis
- Never merge without human approval

**9. Merge and close**:
```
/project:close-pr {num}
```
Merges via `gh pr merge --squash`, completes IMPLEMENTATION.md, updates ACTIVE_PRS.md, checks for ADRs, commits docs.

**10. Update context**:
```
/project:context-update
```
Refreshes all `.context/` files. Check health anytime with `/project:context-status`.

### For Smaller Tasks

| Situation | Use this |
|-----------|----------|
| Medium task (hours) | `/project:oneshot-plan` — research, plan, implement in one session |
| Quick fix | `/project:founder-mode` — bias toward action, still uses PRs |
| Need plan only | `/project:create-plan` then `/project:implement-pr` |
| Continuing work | `/project:resume-handoff` |
| Debugging | `/project:debug` |

---

## Project Structure

```
your-project/
├── .claude/
│   └── commands/
│       ├── project/           # All workflow commands (30+ commands)
│       └── shared/            # Branch safety enforcement
├── docs/
│   ├── .context/              # Living project context
│   │   ├── ACTIVE_PRS.md      # Currently open PRs
│   │   └── RECENT_DECISIONS.md # Recent architectural decisions
│   ├── decisions/             # Architecture Decision Records (ADRs)
│   │   ├── _INDEX.md          # Decision catalog
│   │   └── _TEMPLATE.md       # ADR template
│   ├── handoffs/              # Session handoff documents
│   ├── plans/                 # Implementation plans
│   ├── prs/                   # PR paper trails (lifecycle directories)
│   │   ├── planning/          # PRs in research/planning phase
│   │   ├── implementing/      # PRs actively being implemented
│   │   ├── _archive/          # Merged/closed PRs
│   │   └── _TEMPLATE/         # RESEARCH.md, PLAN.md, IMPLEMENTATION.md
│   └── research/              # Codebase research documents
├── CLAUDE.md                  # This file
└── ... your code ...
```

## Available Commands

### PR Lifecycle (`/project:*`)

| Command | Purpose |
|---------|---------|
| `/project:start-pr {num} {slug}` | Create feature branch + paper trail folder |
| `/project:implement-pr {num}` | Execute implementation from PLAN.md with tracking |
| `/project:verify-pr {num}` | Run lint, typecheck, test, build checks |
| `/project:close-pr {num}` | Merge GitHub PR, complete docs, check for ADRs |
| `/project:execute-pr {num}` | Full lifecycle orchestrator (all of the above) |
| `/project:pr-status [num]` | PR progress, phase, and next action |

### Documentation (`/project:*`)

| Command | Purpose |
|---------|---------|
| `/project:decision {slug}` | Create Architecture Decision Record |
| `/project:context-update` | Refresh ACTIVE_PRS.md and RECENT_DECISIONS.md |
| `/project:context-status` | Documentation health report with staleness checks |

### Planning (`/project:*`)

| Command | Purpose |
|---------|---------|
| `/project:create-plan` | Interactive plan creation with codebase research (opus) |
| `/project:create-plan-nt` | Lightweight plan, no docs/ required (opus) |
| `/project:implement-plan` | Execute plan phase by phase with verification |
| `/project:iterate-plan` | Update existing plan based on feedback (opus) |
| `/project:iterate-plan-nt` | Lightweight plan iteration (opus) |
| `/project:validate-plan` | Verify implementation matches plan |
| `/project:oneshot` | Research + plan in one flow |
| `/project:oneshot-plan` | Research + plan + implement in one session |

### Git & PR (`/project:*`)

| Command | Purpose |
|---------|---------|
| `/project:commit` | Commits with branch safety enforcement |
| `/project:ci-commit` | Non-interactive commit for CI workflows |
| `/project:describe-pr` | Generate PR description from paper trail |
| `/project:ci-describe-pr` | Non-interactive PR description for CI |
| `/project:describe-pr-nt` | Lightweight PR description |

### Research & Debug (`/project:*`)

| Command | Purpose |
|---------|---------|
| `/project:research-codebase` | Codebase research + doc generation (opus) |
| `/project:research-codebase-generic` | Deep research with parallel sub-agents (opus) |
| `/project:research-codebase-nt` | Lightweight inline research (opus) |
| `/project:debug` | Investigate logs and code (read-only) |

### Review, Handoffs, and Modes (`/project:*`)

| Command | Purpose |
|---------|---------|
| `/project:local-review` | Review a colleague's PR locally |
| `/project:create-handoff` | Create session handoff document |
| `/project:resume-handoff` | Resume from handoff document |
| `/project:founder-mode` | Rapid development with bias toward action |

## Documentation Patterns

### PR Paper Trail

Each PR gets a folder with RESEARCH.md, PLAN.md, and IMPLEMENTATION.md that moves through lifecycle directories:

```
docs/prs/planning/{date}-PR-{num}-{slug}/     # Created by /project:start-pr
docs/prs/implementing/{date}-PR-{num}-{slug}/  # Moved by /project:execute-pr
docs/prs/_archive/{date}-PR-{num}-{slug}/      # Moved by /project:close-pr
```

- **RESEARCH.md** — The "why": problem statement, options, recommendation
- **PLAN.md** — The "how": scope, design, implementation order, definition of done
- **IMPLEMENTATION.md** — The "what": changes made, deviations, learnings

### Architecture Decision Records

Record significant decisions with `/project:decision {slug}`. Use ADRs when:
- Choosing between competing technologies
- Establishing patterns for the codebase
- Making trade-offs that affect the system
- Decisions that future developers will question

### Best Practices

- **Fill RESEARCH.md before coding** — understand the problem first
- **Update PLAN.md when scope changes** — keep it current, not aspirational
- **Complete IMPLEMENTATION.md with learnings** — future you will thank you
- **Run `/project:context-update` regularly** — keep living docs current
- **Use `/project:context-status` to check health** — catch staleness early
- **One decision per ADR** — supersede rather than delete old decisions
