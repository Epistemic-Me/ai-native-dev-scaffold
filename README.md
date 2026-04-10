# AI-Native Development Scaffold

A project scaffold for AI-native software development with Claude Code. Three commands. Zero ambiguity.

## The 3-Command Loop

```
/start-pr  →  /execute-pr  →  /review-pr
```

| Command | What it does |
|---------|-------------|
| `/project:start-pr 042 add-auth` | Creates branch + docs scaffold (RESEARCH, TEST-STRATEGY, IMPLEMENTATION-PLAN, IMPLEMENTATION) |
| `/project:execute-pr 042` | Reads IMPLEMENTATION-PLAN.md, implements phase by phase, tracks progress |
| `/project:review-pr 042` | AI code review → docs-gate check → merge → archive → close |

That's the entire workflow. No close command — `review-pr` handles merge and cleanup when approved.

## The Philosophy: Brainpower Moves Left

**Old world**: Think a little → code a lot → discover problems in QA → fix in prod.
**New world**: Think a LOT → define exit criteria → plan step-by-step → execute fast with confidence.

You spend 60-70% of your effort in **RESEARCH.md → TEST-STRATEGY.md → IMPLEMENTATION-PLAN.md**. By the time you run `/execute-pr`, the thinking is done. Execution is mechanical.

### Fill Order

Before running `/execute-pr`, fill these docs IN ORDER:

1. **RESEARCH.md** — Understand the problem. Iterate with AI: "what am I missing? what are the edge cases?"
2. **TEST-STRATEGY.md** — Define acceptance criteria and test matrix BEFORE code. If you can't write this, you don't understand the problem yet.
3. **IMPLEMENTATION-PLAN.md** — Step-by-step plan mapped to ACs. Anyone should be able to follow this.

## Getting Started (15 minutes)

### 1. Clone and reinitialize

```bash
git clone https://github.com/Epistemic-Me/ai-native-dev-scaffold.git my-project
cd my-project
rm -rf .git
git init
git add -A
git commit -m "init: scaffold from ai-native-dev-scaffold"
```

### 2. Customize CLAUDE.md

Add your project-specific instructions: how to run locally, run tests, key files, environment variables.

### 3. Fill in your context docs

Fill `docs/.context/ARCHITECTURE-TAXONOMY.md` and `docs/.context/KNOWN_ISSUES.md` at minimum.

### 4. Start your first PR

```
/project:start-pr 001 initial-feature
```

## What's Included

```
ai-native-dev-scaffold/
├── .claude/commands/
│   ├── project/              # 5 commands total
│   │   ├── start-pr.md      # 1. Create branch + docs scaffold
│   │   ├── execute-pr.md    # 2. Implement from plan
│   │   ├── review-pr.md     # 3. Review + merge + close
│   │   ├── decision.md      # Create ADRs
│   │   └── context-update.md
│   └── shared/
│       └── branch-safety.md
├── docs/
│   ├── .context/             # Project brain (6 template files)
│   ├── decisions/            # ADRs (_INDEX + _TEMPLATE)
│   ├── prs/
│   │   ├── planning/         # PRs in research phase
│   │   ├── implementing/     # PRs being coded
│   │   ├── _archive/         # Merged PRs (includes filled example)
│   │   └── _TEMPLATE/        # RESEARCH, TEST-STRATEGY, IMPL-PLAN, IMPL
│   └── research/
├── scripts/
│   └── pr_docs_check.py      # Docs-gate validator
├── .github/workflows/
│   └── pr-docs-gate.yml      # CI: blocks merge if docs missing
└── CLAUDE.md
```

## Example

See `docs/prs/_archive/2026-01-15-PR-001-add-user-registration/` for a complete filled example.

## CI Docs Gate

Every PR to `main` is checked automatically. Blocks merge if RESEARCH.md, TEST-STRATEGY.md, or IMPLEMENTATION-PLAN.md are missing.

## Maturity Levels

This is the **Walk** repo (Level 1-2). When ready for stakeholder alignment + digital twin compound loop, upgrade to **Run**: [ai-native-dev-scaffold-compound](https://github.com/Epistemic-Me/ai-native-dev-scaffold-compound).

Same 3 commands — `review-pr` just does more behind the scenes at Run level.

## License

MIT — Use freely.

---

*Built for AI-native development with Claude Code by [Epistemic Me](https://github.com/Epistemic-Me)*
