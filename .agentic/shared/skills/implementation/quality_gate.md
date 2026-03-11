# Skill: Quality gate

Use when running automated checks (formatters, linters, tests, build) and fixing failures.

## Operating rules
- Assume automation will fail on first run.
- Run the repo's standard commands (format, lint, test, build if present).
- If a BDD suite is configured (e.g., Gherkin `*.feature` specs), include it in the standard automation run.
- If the repo has an E2E/journey suite, include it in the standard automation run when relevant to the changed behavior.
- When functional changes alter behavior covered by existing E2E tests, update those tests in the same feature work.
- When user-visible behavior changes, update maintained manual scenario artifacts in the same feature work (and regenerate derived validation outputs when used by the project).
- Fix issues with the smallest safe change.
- Add tests when you find uncovered behavior.
- For bug fixes: identify why existing automation did not catch the issue, then add/adjust tests to prevent recurrence.
