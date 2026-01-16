# Context Update

Update the living context files after significant work.

## When to Use

Run this after:
- Completing a PR
- Making a significant decision
- Changing project direction
- At the end of a work session

Example usage: `/project:context-update`

## Instructions

1. **Review recent changes**:
   - Check git log for recent commits
   - Review any open PR paper trails

2. **Update ACTIVE_PRS.md**:
   - Add any new PRs started
   - Update status of in-progress PRs
   - Move merged PRs to "Recently Merged"

3. **Update RECENT_DECISIONS.md**:
   - Add any new ADRs created
   - Update status of pending decisions
   - Keep only last 10 decisions in quick reference

4. **Review for staleness**:
   - Flag any context that seems outdated
   - Suggest cleanup if needed

5. **Report summary** of updates made
