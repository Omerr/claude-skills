Perform Code Review for $ARGUMENTS

Carefully review the open PR for the current branch. Follow this iterative process:

1. **Understand the PR**: Use `gh pr view` and `gh pr diff` to understand the full scope of changes.

2. **Break into tasks**: Create a task list tracking your progress through the review.

3. **Iterative review** — perform multiple passes:
   - **Pass 1 — Bug hunting**: Look for potential bugs, logic errors, off-by-one errors, null/undefined handling, race conditions, missing error handling, and security issues.
   - **Pass 2 — Validate findings**: For each issue found, read the surrounding code carefully to confirm whether it is a real problem or a false positive. Remove false positives.
   - **Pass 3 — Code smells**: Look for code smells — duplicated logic, overly complex functions, poor naming, missing abstractions, dead code, inconsistent patterns, and violations of project conventions.
   - **Pass 4 — Additional issues**: With full context of the codebase now loaded, do one more sweep for anything missed — edge cases, integration issues, missing tests, or subtle correctness problems.

4. **Report**: Present a clear summary of confirmed findings, categorized by severity (critical / warning / nit). For each finding, include the file path, line number, and a concise explanation of the issue and suggested fix.
