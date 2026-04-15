# RESEARCH: Reposition scaffold as Walk stage of Crawl/Walk/Run

**Linear**: [DAY-46](https://linear.app/epistemicme/issue/DAY-46)
**Predecessor**: DAY-32 (AI-Native PR Workflow Slide Deck v1 for an enterprise software company stakeholders)

## Requirements Analysis

DAY-32 shipped a Walk/Run maturity framing to an enterprise software company engineering directors. Feedback: the framing collapses the real 7-stage Clarity-API lifecycle into a fictional "3-command loop" and assumes teams already have a context foundation (`docs/.context/`, MCP registries, credential hygiene). In reality, missing context engineering is the #1 reason enterprise AI pilots fail. MIT NANDA 2025: 95% of enterprise AI pilots stall with no measurable P&L impact; root cause is the "learning gap" (missing organizational context), not model quality.

The v2 deck reframes the maturity model as **Crawl → Walk → Run**, dimensioned across **People / Process / Tools**. This PR repositions the `ai-native-dev-scaffold-run` as the **Walk** stage so the example repo matches the deck's claims.

## Current State Analysis

The scaffold master already has:
- `CLAUDE.md` describing a "3-command loop" (`/start-pr → /execute-pr → /review-pr`) which does not match Clarity-API's real 5-stage lifecycle
- `docs/.context/` with ARCHITECTURE-TAXONOMY, CURRENT_SPRINT, KNOWN_ISSUES, ROADMAP, ACTIVE_PRS, RECENT_DECISIONS
- `.github/workflows/pr-docs-gate.yml` enforcing RESEARCH/TEST-STRATEGY/IMPLEMENTATION-PLAN per PR
- `scripts/pr_docs_check.py` gate logic
- Example archived PR, USER-GUIDE.md

What's missing:
- `docs/.context/MCP_SERVERS.md` — the tool registry half of the Crawl foundation
- Credential policy section in CLAUDE.md
- Any explicit "You Are Here" positioning on the Crawl/Walk/Run staircase
- Correct 5-stage lifecycle naming (current docs reference `/execute-pr` which does not exist in Clarity-API)

## Implementation Gap Analysis

| Gap | Impact | Fix |
|---|---|---|
| No MCP_SERVERS.md | Users have no pattern for declaring tool access per repo | Create standalone file in `docs/.context/` with Linear/Playwright/GitHub entries + Context Declaration template |
| No credential policy | Users wire up secrets ad-hoc | Add 5-point abstract policy section to CLAUDE.md (vendor-agnostic) |
| "3-command loop" framing | Contradicts real Clarity-API 5-stage lifecycle; an enterprise software company directors will click through and see the mismatch | Rewrite CLAUDE.md lifecycle section and README title to use real stages |
| No staircase positioning | Users don't understand this is one stage of three | Add "You Are Here" table to top of README and CLAUDE.md linking to Crawl and Run scaffolds |

## Dependencies and Risks

- **Dependency**: DAY-46 v2 deck revision (in progress)
- **Dependency**: `ai-native-dev-scaffold-sprint` (Run) parallel PR for consistency
- **Dependency**: `ai-native-dev-scaffold-walk` repo creation (new — tracked in DAY-46)
- **Risk**: Existing users of the scaffold may expect the 3-command framing — mitigated by keeping command names intact; only docs change, not behavior
- **Risk**: Directors may ask about the credential policy's vendor implementation — the policy deliberately stays vendor-agnostic to avoid prescribing 1Password/Vault/etc.

## Open Questions

None — scope is narrow and doc-only.
