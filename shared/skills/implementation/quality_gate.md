# Skill: Quality gate

Use when running automated checks (formatters, linters, tests, build) and fixing failures.

## Operating rules
- Assume automation will fail on first run.
- Run the repo's standard commands (format, lint, test, build if present).
- Fix issues with the smallest safe change.
- Add tests when you find uncovered behavior.
