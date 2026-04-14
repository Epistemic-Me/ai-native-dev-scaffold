# TEST-STRATEGY: Reposition scaffold as Walk stage

## Acceptance Criteria

| ID | Criterion |
|---|---|
| AC1 | `docs/.context/MCP_SERVERS.md` exists with at least 3 MCP server entries and a Context Declaration template |
| AC2 | `CLAUDE.md` references the real 5-stage lifecycle (`/start-pr → develop → /review-pr → /check-pr → /close-pr`), not the fictional 3-command loop |
| AC3 | `CLAUDE.md` includes a Credential Policy section with 5 abstract principles (vendor-agnostic) |
| AC4 | `CLAUDE.md` top contains a "You Are Here" Crawl/Walk/Run staircase |
| AC5 | `README.md` title includes "Walk Stage" and contains a "You Are Here" table linking to `ai-native-dev-scaffold-crawl` and `ai-native-dev-scaffold-run` |
| AC6 | Existing docs-gate CI continues to pass (this PR's own docs folder satisfies RESEARCH.md / TEST-STRATEGY.md / IMPLEMENTATION-PLAN.md) |

## Test Matrix

| Test ID | File | Test Case | AC Covered | Pass Criteria |
|---|---|---|---|---|
| T1 | docs/.context/MCP_SERVERS.md | File exists and has content | AC1 | `test -s docs/.context/MCP_SERVERS.md` |
| T2 | docs/.context/MCP_SERVERS.md | Contains Linear, Playwright, GitHub MCP entries | AC1 | `grep -q "Linear MCP" && grep -q "Playwright MCP" && grep -q "GitHub MCP"` |
| T3 | docs/.context/MCP_SERVERS.md | Contains Context Declaration template | AC1 | `grep -q "Context Declaration"` |
| T4 | CLAUDE.md | References 5-stage lifecycle | AC2 | `grep -q "/start-pr" && grep -q "/check-pr" && grep -q "/close-pr"` |
| T5 | CLAUDE.md | Does not reference fictional `/execute-pr` in the lifecycle diagram | AC2 | manual review — old command references removed from the top-line lifecycle |
| T6 | CLAUDE.md | Contains "Credential Policy" section | AC3 | `grep -q "Credential Policy"` |
| T7 | CLAUDE.md | Contains "You Are Here" staircase | AC4 | `grep -q "You Are Here"` |
| T8 | README.md | Title includes "Walk Stage" | AC5 | `head -1 README.md | grep -q "Walk"` |
| T9 | README.md | Contains "You Are Here" table with links to sibling scaffolds | AC5 | `grep -q "ai-native-dev-scaffold-run"` |
| T10 | CI | docs-gate passes on the PR | AC6 | GitHub Actions green check |

## Definition of Done

- [ ] All 6 acceptance criteria verified via the test matrix above
- [ ] CI docs-gate passes (green check on PR)
- [ ] No behavior changes — only documentation
- [ ] REVIEW.md generated via manual review (no sub-agent needed for docs-only PR)
- [ ] Sibling PR in `ai-native-dev-scaffold-run` tracked for consistency
