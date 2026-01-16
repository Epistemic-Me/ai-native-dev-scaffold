---
description: Generate comprehensive PR descriptions
---

# Generate PR Description

You are tasked with generating a comprehensive pull request description.

## Steps to follow:

1. **Identify the PR to describe:**
   - Check if the current branch has an associated PR: `gh pr view --json url,number,title,state 2>/dev/null`
   - If no PR exists for the current branch, list open PRs: `gh pr list --limit 10 --json number,title,headRefName,author`
   - Ask the user which PR they want to describe

2. **Check for existing PR paper trail:**
   - Look for `docs/prs/*-PR-{number}-*/` folder
   - If it exists, read RESEARCH.md, PLAN.md, and IMPLEMENTATION.md
   - Use this context to enrich the PR description

3. **Gather comprehensive PR information:**
   - Get the full PR diff: `gh pr diff {number}`
   - Get commit history: `gh pr view {number} --json commits`
   - Review the base branch: `gh pr view {number} --json baseRefName`
   - Get PR metadata: `gh pr view {number} --json url,title,number,state`

4. **Analyze the changes thoroughly:**
   - Read through the entire diff carefully
   - For context, read any files that are referenced but not shown in the diff
   - Understand the purpose and impact of each change
   - Identify user-facing changes vs internal implementation details
   - Look for breaking changes or migration requirements

5. **Handle verification requirements:**
   - For each verification step:
     - If it's a command you can run (like tests, linting), run it
     - If it passes, mark the checkbox as checked: `- [x]`
     - If it fails, keep it unchecked and note what failed
     - If it requires manual testing, leave unchecked and note for user
   - Document any verification steps you couldn't complete

6. **Generate the description:**
   Use this template:

   ```markdown
   ## Summary

   [2-3 sentence summary of what this PR does and why]

   ## Changes

   ### [Category 1]
   - Change description
   - Another change

   ### [Category 2]
   - Change description

   ## How to Test

   1. [Step-by-step testing instructions]
   2. [Another step]

   ## Verification

   - [x] Tests pass: `npm test`
   - [x] Linting passes: `npm run lint`
   - [ ] Manual testing: [describe what needs testing]

   ## Screenshots (if applicable)

   [Add screenshots for UI changes]

   ## Breaking Changes

   [List any breaking changes, or "None"]

   ## Related

   - Related issue: #[number]
   - Paper trail: `docs/prs/{path}/`
   ```

7. **Update the PR:**
   - Update the PR description directly: `gh pr edit {number} --body-file /tmp/pr_description.md`
   - Confirm the update was successful
   - If any verification steps remain unchecked, remind the user to complete them before merging

## Important notes:
- Be thorough but concise - descriptions should be scannable
- Focus on the "why" as much as the "what"
- Include any breaking changes or migration notes prominently
- If the PR touches multiple components, organize the description accordingly
- Always attempt to run verification commands when possible
- Clearly communicate which verification steps need manual testing
