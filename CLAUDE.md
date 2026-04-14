# Claude Code Project Context

This project is the **Walk** stage of the Crawl → Walk → Run AI-native maturity model. It demonstrates an enforceable PR lifecycle built on top of a Crawl-stage context foundation.

## You Are Here: Crawl / Walk / Run

- **Crawl** — Context Foundation: `CLAUDE.md`, `docs/.context/` core set, `docs/.context/MCP_SERVERS.md`, credential policy. No PR workflow. See `ai-native-dev-scaffold-crawl` *(coming soon)*.
- **Walk** — Paper Trail + Gate *(← you are here)*: Crawl + 5-stage PR lifecycle + docs-gate CI + ADR index. Clarity integration begins here via `/project:start-pr` capturing intent as an episode.
- **Run** — Compounding Intelligence: Walk + `/stakeholder-alignment` + `/compound` + `/process-transcript` + self-model API integration. See `ai-native-dev-scaffold-run`.

Start here if your team needs a verifiable PR paper trail and CI-enforced docs gate. Upgrade to the `-compound` repo when you're ready for the compounding loop.

## The PR Lifecycle (5 stages)

```
/project:start-pr  →  develop  →  /project:review-pr  →  /project:check-pr  →  /project:close-pr
```

1. **`/project:start-pr {num} {slug}`** — Create branch + docs scaffold (RESEARCH / TEST-STRATEGY / IMPLEMENTATION-PLAN)
2. **develop** — Iterate on the artifacts, then implement against IMPLEMENTATION-PLAN.md
3. **`/project:review-pr {num}`** — AI code review + verdict written to REVIEW.md
4. **`/project:check-pr {num}`** — Run docs-gate locally (same checks as CI)
5. **`/project:close-pr {num}`** — Merge + archive docs to `_archive/` + update ACTIVE_PRS.md

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

## Credential Policy (Crawl-stage foundation)

This repo treats tool access and secrets as **context that must be declared**, not tribal knowledge. Agents and new engineers read this policy before touching anything.

1. **No secrets in the repo.** `.env` files are gitignored. `.env.example` documents what variables exist without values. Secrets in commits are a blocking issue — rotate immediately and force-push a clean history.
2. **Vault is the source of truth.** Every credential has a canonical path like `vault://engineering/{service}`. `CLAUDE.md`, `docs/.context/MCP_SERVERS.md`, and ticket Context Declarations reference vault paths, never the secret values.
3. **Service accounts, not personal credentials.** AI agents run as a dedicated identity separate from human developers. Linear, GitHub, and any third-party API access use a bot account whose blast radius is bounded.
4. **Least-privilege per task.** Credentials loaded for a ticket grant access only to what that ticket needs. No blanket admin tokens for day-to-day work.
5. **Short-lived where possible.** Prefer dynamic, expiring credentials over long-lived static keys. The exact mechanism (Vault dynamic secrets, 1Password Unified Access, cloud IAM role assumption, etc.) is an org-level choice — this scaffold declares the policy, not the vendor.

See `docs/.context/MCP_SERVERS.md` for per-server credential paths and the Context Declaration template for ticket descriptions.

## Best Practices

- **Fill RESEARCH.md before coding** — understand the problem first
- **Define exit criteria in TEST-STRATEGY.md before planning** — know what "done" looks like
- **Declare context up-front** — every ticket includes a Context Declaration block (see `docs/.context/MCP_SERVERS.md`)
- **Update docs when scope changes** — docs lead, code follows
- **Record significant decisions as ADRs** — especially ones future devs will question
- **Run `/project:context-update` regularly** — keep the project brain current
