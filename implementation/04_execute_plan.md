# Execute Plan

## Role
See `@shared/roles/software_engineer.md`.

## Objective
Execute the task plan one step at a time on a new local git feature branch, committing each logically separated chunk.

## Output Boundary (STRICT)
See `@shared/skills/gates/output_boundary.md`.
Override: no artifacts; update repo files directly. When done and automation is green, you may output a short validation script (2-6 steps).

## Required Inputs
- `artifacts/<project_slug>/tasks/plan-<feature_slug>.md`
- `artifacts/<project_slug>/00_open_questions.md`
- `artifacts/<project_slug>/00_decision_log.md`
- `artifacts/<project_slug>/05_technical_design.md`
- Repo codebase (existing, or bootstrapped as part of the plan)

## Starting Point (Mandatory)
Do not implement everything at once.

- Work chunk-by-chunk.
- Keep changes small and verifiable.

## Open Questions Gate (Mandatory)
See `@shared/skills/gates/open_questions_gate.md` (Blockers: any `[Blocking]` item affecting the chunk you are about to do).

## Git Rules
- Create a new local feature branch before making changes.
- Commit after each chunk (or meaningful sub-chunk), with a message that explains intent.
- Follow `@shared/skills/git/git_commit.md`.
- Do not push unless explicitly asked.

## Task Hygiene
- As you complete tasks, check them off in `artifacts/<project_slug>/tasks/plan-<feature_slug>.md`.
- If the plan needs adjustment, update the task file and call it out to the user.

## Automation (Folded In)
Run the project's standard commands during/after execution (format, lint, test, and build if present).

- Prefer running fast checks per chunk, then the full suite at the end.
- Fix issues with the smallest safe change.
- If automation reveals uncovered behavior, add tests.

Then ask:

> "Implementation done and automation is green. Please validate with the script above. What (if anything) didn't work? Include repro steps."

If the user wants a dedicated pass for automation or validation, they can optionally tag:

- **@implementation/05_run_quality_gate.md**
- **@implementation/06_validate_with_user.md**
