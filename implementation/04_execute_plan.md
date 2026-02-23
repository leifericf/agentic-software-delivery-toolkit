# Execute Plan

## Role
See `@shared/roles/software_engineer.md`.

## Objective
Execute the task plan one step at a time on a new local git feature branch, committing each logically separated chunk.

## Output Boundary (STRICT)
See `@shared/skills/gates/output_boundary.md`.
Override: no new artifacts; update repo files directly. Keep `artifacts/<project_slug>/product_backlog.md` up to date as you go. When done and automation is green, you may output a short validation script (2-6 steps).

## Required Inputs
- `artifacts/<project_slug>/tasks/plan-<feature_slug>.md`
- `artifacts/<project_slug>/open_questions.md`
- `artifacts/<project_slug>/decision_log.md`
- `artifacts/<project_slug>/technical_design.md`
- `artifacts/<project_slug>/product_backlog.md`
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

## Backlog Hygiene (Mandatory)

Keep the backlog a living document:

- Capture out-of-scope ideas immediately: if the user or you mention a future feature that is not required to finish the current plan, add it under `Inbox (untriaged)` in `artifacts/<project_slug>/product_backlog.md`.
- Do not expand the current feature's scope unless the user explicitly changes `## Executable Specification (Gherkin)` in the plan.
- When the feature is done and automation is green, move the implemented backlog item from `Now / Next` to `In product (shipped)`.
- If you discover net-new feature work that is truly out of scope for this plan, capture it in the backlog (`Inbox (untriaged)` or reprioritize into `Now / Next`/`Later`).
- Do not add bug reports to the backlog. Fix bugs relevant to the feature immediately unless the user explicitly suppresses the fix; if suppressed, capture it as a follow-up task in `artifacts/<project_slug>/tasks/plan-<feature_slug>.md`.

## Automation (Folded In)
Run the project's standard commands during/after execution (format, lint, test, and build if present).

If the plan includes `## Executable Specification (Gherkin)`, make it executable:

- Materialize the Gherkin into `features/<feature_slug>.feature` (unless the repo already has an established convention).
- Use the most idiomatic BDD runner for the repo's language/test stack (or the existing one), and wire it into the repo's standard automation.
- Treat "automation is green" as including the BDD suite.

- Prefer running fast checks per chunk, then the full suite at the end.
- Fix issues with the smallest safe change.
- If automation reveals uncovered behavior, add tests.

Then ask:

> "Implementation done and automation is green. Please validate with the script above. What (if anything) didn't work? Include repro steps."

If the user wants a dedicated pass for automation or validation, they can optionally tag:

- **@implementation/05_run_quality_gate.md**
- **@implementation/06_validate_with_user.md**
