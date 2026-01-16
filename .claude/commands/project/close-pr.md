# Close PR

Complete PR documentation and update related docs after merge.

## Arguments

The user should provide:
- PR number (e.g., "142")

Example usage: `/project:close-pr 142`

## Instructions

1. **Find the PR folder** in `docs/prs/` matching the PR number

2. **Update IMPLEMENTATION.md**:
   - Ensure "Summary" section is filled
   - Ensure "Key Changes" documents what was built
   - Ensure "Testing Done" has checked items
   - Ensure "Learnings" sections are filled
   - Set "PR Merged" date to today
   - Change "Status" from "In Progress" to "Complete"

3. **Review for completeness**:
   - RESEARCH.md should have problem statement and chosen option
   - PLAN.md should have scope and implementation order
   - IMPLEMENTATION.md should have summary and learnings
   - Flag any incomplete sections to the user

4. **Update ACTIVE_PRS.md**:
   - Move PR from "Open PRs" to "Recently Merged" table
   - Include merge date and paper trail link

5. **Check for decisions**:
   - Review RESEARCH.md and PLAN.md for significant decisions
   - If architectural decisions were made, ask user if ADR should be created
   - If yes, run the decision flow

6. **Report summary** of all updates made
