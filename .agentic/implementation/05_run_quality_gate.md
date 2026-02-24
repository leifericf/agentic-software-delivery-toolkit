# Quality Gate

## Role
See `@.agentic/shared/roles/quality_engineer.md`.

## Objective
Run automated checks (tests, linters, formatters) and fix failures.

This step is optional if you already run automation during `.agentic/implementation/04_execute_plan.md`.

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/output_boundary.md`.
Override: no artifacts; run commands and change code as needed.

## Required Inputs
- Repo codebase
- `.agentic/artifacts/tasks/plan-<feature_slug>.md`

## Starting Point (Mandatory)
Assume automation will fail on first run.

- Run the repo's standard commands (format, lint, test, build if present).
- If a BDD suite is present/configured, run it as part of automation.
- Fix issues with the smallest safe change.
- Add tests when you find uncovered behavior.

See `@.agentic/shared/skills/implementation/quality_gate.md`.

## Output
- A clean run of the project's automated checks.

Then ask:

> "Automation is green. Please validate end-to-end (2-6 steps). What (if anything) didn't work? Include repro steps." 

If the user prefers a dedicated validation pass, they can optionally tag **@.agentic/implementation/06_validate_with_user.md**.
