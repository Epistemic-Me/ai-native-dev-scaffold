# Claude Code Project Context

This project uses the AI-Native Development Lifecycle with a 3-command PR workflow.

## The 3-Command Loop

```
/project:start-pr  →  /project:execute-pr  →  /project:review-pr
```

1. **`/project:start-pr {num} {slug}`** — Create branch + docs scaffold
2. **`/project:execute-pr {num}`** — Implement from IMPLEMENTATION-PLAN.md with tracking
3. **`/project:review-pr {num}`** — AI review + docs-gate + merge + archive + close

## MANDATORY: PR Workflow Rules

**NEVER commit directly to master/main.** All code changes MUST follow PR workflow.

1. Check current branch: `git branch --show-current`
2. If on master/main → **STOP** and create feature branch via `/project:start-pr`
3. Never merge without human approval

See `.claude/commands/shared/branch-safety.md` for enforcement details.

## Fill Order (CRITICAL)

Before running `/project:execute-pr`, fill these docs IN ORDER:

1. **RESEARCH.md** — Understand the problem. Iterate with AI: "what am I missing?"
2. **TEST-STRATEGY.md** — Define exit criteria BEFORE code. ACs + test matrix.
3. **IMPLEMENTATION-PLAN.md** — Step-by-step plan mapped to ACs.

The thinking happens in steps 1-3. Execution (step 4: execute-pr) is just following the plan.

## Project Structure

```
your-project/
├── .claude/commands/
│   ├── project/
│   │   ├── start-pr.md         # 1. Scaffold
│   │   ├── execute-pr.md       # 2. Implement
│   │   ├── review-pr.md        # 3. Review + merge + close
│   │   ├── decision.md         # Create ADRs
│   │   └── context-update.md   # Refresh .context/ docs
│   └── shared/
│       └── branch-safety.md    # PR enforcement
├── docs/
│   ├── .context/               # Project brain (AI reads at session start)
│   │   ├── ARCHITECTURE-TAXONOMY.md
│   │   ├── KNOWN_ISSUES.md
│   │   ├── ROADMAP.md
│   │   ├── CURRENT_SPRINT.md
│   │   ├── ACTIVE_PRS.md
│   │   └── RECENT_DECISIONS.md
│   ├── decisions/              # ADRs (_INDEX.md + _TEMPLATE.md + per-decision)
│   ├── prs/                    # PR paper trails
│   │   ├── planning/           # PRs in research/planning
│   │   ├── implementing/       # PRs being coded
│   │   ├── _archive/           # Merged PRs
│   │   └── _TEMPLATE/          # RESEARCH, TEST-STRATEGY, IMPLEMENTATION-PLAN, IMPLEMENTATION
│   └── research/               # Codebase research
├── scripts/
│   └── pr_docs_check.py        # Docs-gate validator
├── .github/workflows/
│   └── pr-docs-gate.yml        # CI: blocks merge if docs missing
└── CLAUDE.md                   # This file
```

## Available Commands

| Command | Purpose |
|---------|---------|
| `/project:start-pr {num} {slug}` | Create branch + docs scaffold |
| `/project:execute-pr {num}` | Implement from plan with progress tracking |
| `/project:review-pr {num}` | AI review + docs-gate + merge + close |
| `/project:decision {slug}` | Create Architecture Decision Record |
| `/project:context-update` | Refresh .context/ docs |

## CI Docs Gate

Every PR to main is checked by `.github/workflows/pr-docs-gate.yml`:
- RESEARCH.md exists (>50 bytes)
- TEST-STRATEGY.md exists (>50 bytes)
- IMPLEMENTATION-PLAN.md exists (>50 bytes)

PRs with 5 or fewer changed lines in docs/config skip the gate.

## Best Practices

- **Fill RESEARCH.md before coding** — understand the problem first
- **Define exit criteria in TEST-STRATEGY.md before planning** — know what "done" looks like
- **Update docs when scope changes** — docs lead, code follows
- **Record significant decisions as ADRs** — especially ones future devs will question
- **Run `/project:context-update` regularly** — keep the project brain current
