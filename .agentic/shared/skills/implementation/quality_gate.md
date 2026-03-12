# Skill: Quality gate

Use when running automated checks (formatters, linters, tests, build) and fixing failures.

## Operating rules
- Assume automation will fail on first run.
- Run the repo's standard commands (format, lint, test, build if present).
- If a BDD suite is configured (e.g., Gherkin `*.feature` specs), include it in the standard automation run.
- If the repo has an E2E/journey test suite, include it in the standard automation run.
- When functional changes alter behavior covered by existing E2E tests, update those tests in the same feature work (not deferred).
- When user-visible behavior changes, verify the maintained manual scenario source artifact is updated in the same feature work and any derived validation sheet is regenerated.
- Fix issues with the smallest safe change.
- Add tests when you find uncovered behavior.
- For bug fixes: start by identifying why existing automation did not catch it, then add/adjust tests to prevent recurrence.
- While investigating failures or scanning code for other reasons, stay alert for unrelated issues; log them as one-line rows in the correct living artifact (do not add them to the product backlog):
  - Bugs -> `.agentic/artifacts/bug_list.md`
  - UX/UI -> `.agentic/artifacts/ux_ui_issue_list.md`
  - Security -> `.agentic/artifacts/security_issue_list.md`
  - Duplicate check (mandatory): before adding a new row, scan for an existing similar issue; update the existing row instead of duplicating.
  - Issues related to the change you are making should be fixed immediately rather than deferred.
