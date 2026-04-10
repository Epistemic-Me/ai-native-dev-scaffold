# AI-Native Development Scaffold

> 3 commands. That's the entire workflow.

```
/start-pr  →  /execute-pr  →  /review-pr
```

This scaffold gives your team a structured PR workflow with AI-powered code review and a CI quality gate — in 15 minutes.

---

## Quick Start

```bash
# 1. Clone and reinitialize
git clone https://github.com/Epistemic-Me/ai-native-dev-scaffold.git my-project
cd my-project
rm -rf .git && git init && git add -A && git commit -m "init: scaffold"

# 2. Open in your editor with Claude Code (or any AI coding assistant)

# 3. Start your first PR
/project:start-pr 001 my-first-feature
```

That's it. You now have a feature branch, a docs folder with 4 templates, and an entry in ACTIVE_PRS.md.

---

## The 3 Commands

### `/project:start-pr {num} {slug}`
Creates a feature branch and a docs folder with blank templates.

**What you get:**
```
docs/prs/planning/2026-04-10-PR-001-my-first-feature/
├── RESEARCH.md              ← Fill FIRST
├── TEST-STRATEGY.md         ← Fill SECOND  
├── IMPLEMENTATION-PLAN.md   ← Fill THIRD
└── IMPLEMENTATION.md        ← Filled by execute-pr
```

### `/project:execute-pr {num}`
Reads your IMPLEMENTATION-PLAN.md and implements it step by step with progress tracking.

**Before running this**, fill the docs in order:
1. **RESEARCH.md** — What's the problem? What options exist? (Iterate with AI: "what am I missing?")
2. **TEST-STRATEGY.md** — What are the acceptance criteria? What tests prove it works?
3. **IMPLEMENTATION-PLAN.md** — Step-by-step plan mapped to the acceptance criteria.

> The fill order matters. You can't plan until you've defined "done." You can't define "done" until you understand the problem.

### `/project:review-pr {num}`
AI code review → docs-gate check → merge → archive → close. All in one command.

**What happens:**
1. Spawns a fresh AI reviewer (clean context, independent read)
2. Generates REVIEW.md with verdict, per-AC coverage, risk assessment
3. Checks that all required docs exist (same check CI runs)
4. If approved: merges the PR, archives the docs, updates indexes
5. If issues found: tells you what to fix

---

## What's in the Repo

```
.claude/commands/project/
  start-pr.md          # Create branch + docs
  execute-pr.md        # Implement from plan
  review-pr.md         # Review + merge + close
  decision.md          # Create Architecture Decision Record
  context-update.md    # Refresh project context docs

docs/.context/           # Project brain — AI reads these at session start
  ARCHITECTURE-TAXONOMY.md   # Your system layers and boundaries
  KNOWN_ISSUES.md            # Bugs and tech debt
  ROADMAP.md                 # Phase-level plan
  CURRENT_SPRINT.md          # What's in flight now
  ACTIVE_PRS.md              # Open and recently merged PRs
  RECENT_DECISIONS.md        # Latest architectural decisions

docs/decisions/          # Architecture Decision Records
  _INDEX.md              # Master list of all decisions
  _TEMPLATE.md           # Blank ADR template

docs/prs/                # PR paper trails
  planning/              # PRs being researched/planned
  implementing/          # PRs being coded
  _archive/              # Merged PRs (includes a filled example)
  _TEMPLATE/             # Blank templates for new PRs

scripts/
  pr_docs_check.py       # Docs-gate validation script

.github/workflows/
  pr-docs-gate.yml       # CI: blocks merge if docs are missing
```

---

## The Philosophy

**Old world**: Think 10% → Code 40% → Discover problems 20% → Fix 30%.

**This scaffold**: Think 65% → Code 25% → Verify 10%.

You spend most of your effort in RESEARCH → TEST-STRATEGY → IMPLEMENTATION-PLAN. By the time you run `/execute-pr`, the thinking is done. Execution is mechanical.

---

## CI Docs Gate

Every PR to `main` triggers `.github/workflows/pr-docs-gate.yml`.

**Blocks merge if:**
- RESEARCH.md is missing or empty
- TEST-STRATEGY.md is missing or empty
- IMPLEMENTATION-PLAN.md is missing or empty

**Exempt:** PRs with 5 or fewer changed lines in docs/config files.

---

## Example

See `docs/prs/_archive/2026-01-15-PR-001-add-user-registration/` for a complete example with all docs filled. Use it as a reference for your first PR.

---

## Context Docs

Files in `docs/.context/` are read by AI at the start of every session. Keep them accurate:

| File | What to put in it | Who updates it |
|------|-------------------|----------------|
| `ARCHITECTURE-TAXONOMY.md` | System layers, boundaries, key abstractions | Tech Lead |
| `KNOWN_ISSUES.md` | Active bugs and tech debt (P0/P1/P2) | QA / anyone |
| `ROADMAP.md` | Phase-level goals (not sprint-level) | PM |
| `CURRENT_SPRINT.md` | Sprint goal and active items | PM / Scrum Master |
| `ACTIVE_PRS.md` | Open PRs (auto-updated by commands) | Automated |
| `RECENT_DECISIONS.md` | Latest ADRs (auto-updated by /decision) | Automated |

---

## Architecture Decision Records

When you make a significant technical decision:

```
/project:decision jwt-authentication
```

This creates a file in `docs/decisions/` and updates the index. Use ADRs when you're choosing between approaches, making trade-offs, or doing something a future developer will question.

---

## Leveling Up

This is the **Walk** scaffold (Level 1-2). When your team is ready for:
- Stakeholder alignment scoring (digital twin evaluation of every PR)
- Compound self-model loop (organizational learning that compounds)
- Power-user commands (AI-assisted planning, automated PR descriptions, etc.)

Upgrade to **Run**: [ai-native-dev-scaffold-compound](https://github.com/Epistemic-Me/ai-native-dev-scaffold-compound)

Same 3 commands. `review-pr` just does more behind the scenes.

---

## FAQ

**Q: Do I need Claude Code?**
A: The commands are written for Claude Code, but the structure works with any AI assistant. The docs, CI gate, and ADRs are tool-agnostic.

**Q: Do I need all the docs for every PR?**
A: The CI gate exempts PRs with 5 or fewer changed lines. For typo fixes, skip the docs.

**Q: What if I disagree with the AI review?**
A: Update REVIEW.md with your reasoning. The review is a tool, not a boss.

**Q: Can I add more commands?**
A: Yes. The Run repo has 20+ additional commands. Or write your own in `.claude/commands/`.

---

MIT License. Built by [Epistemic Me](https://github.com/Epistemic-Me).
