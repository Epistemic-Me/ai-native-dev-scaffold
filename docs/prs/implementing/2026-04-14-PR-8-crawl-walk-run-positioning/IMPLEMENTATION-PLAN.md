# IMPLEMENTATION-PLAN: Reposition scaffold as Walk stage

## Chosen Approach

Docs-only edit. No command files, scripts, or CI configuration change. Three files touched, one new file created.

## Scope

In scope:
- New `docs/.context/MCP_SERVERS.md`
- Edit `CLAUDE.md`: header reframe, real 5-stage lifecycle, Credential Policy section
- Edit `README.md`: title + "You Are Here" table

Out of scope:
- Renaming any existing command file
- Modifying `pr_docs_check.py` or the CI workflow
- Adding any new slash command to `.claude/commands/`
- Creating `ai-native-dev-scaffold-crawl` (tracked separately in DAY-46)

## Files Summary

| File | Action | Purpose |
|---|---|---|
| `docs/.context/MCP_SERVERS.md` | Create | Tool context registry + Context Declaration template |
| `CLAUDE.md` | Edit | Reframe as Walk stage, correct lifecycle, add Credential Policy |
| `README.md` | Edit | Title + "You Are Here" staircase table |

## Step-by-Step Implementation

### Step 1: MCP_SERVERS.md (AC1)
Create `docs/.context/MCP_SERVERS.md` with three sections:
- Registry (Linear, Playwright, GitHub MCP)
- Per-Ticket Context Declaration template
- References (MCP spec, Astrix Security, Anthropic announcement)

### Step 2: CLAUDE.md header + lifecycle (AC2, AC4)
- Replace opening paragraph + "3-Command Loop" section with "Walk Stage" framing and "You Are Here" staircase table
- Rewrite the lifecycle to real 5 stages: `/start-pr → develop → /review-pr → /check-pr → /close-pr`

### Step 3: CLAUDE.md credential policy (AC3)
- Append "Credential Policy (Crawl-stage foundation)" section with 5 abstract principles
- Reference MCP_SERVERS.md for per-server paths

### Step 4: README.md (AC5)
- Change title from "AI-Native Development Scaffold" to "AI-Native Development Scaffold — Walk Stage"
- Replace subtitle and lifecycle block with real 5-stage version
- Insert "You Are Here: Crawl / Walk / Run" table with links to `ai-native-dev-scaffold-crawl` and `ai-native-dev-scaffold-run`

## Verification Checklist

- [x] T1: `docs/.context/MCP_SERVERS.md` exists and has content
- [x] T2: MCP_SERVERS.md contains Linear, Playwright, GitHub MCP entries
- [x] T3: MCP_SERVERS.md contains Context Declaration template
- [x] T4: CLAUDE.md references 5-stage lifecycle
- [x] T5: `/execute-pr` removed from CLAUDE.md top-line lifecycle
- [x] T6: CLAUDE.md contains "Credential Policy"
- [x] T7: CLAUDE.md contains "You Are Here"
- [x] T8: README.md title includes "Walk Stage"
- [x] T9: README.md links to sibling scaffolds
- [ ] T10: CI docs-gate green (verified on draft PR)
