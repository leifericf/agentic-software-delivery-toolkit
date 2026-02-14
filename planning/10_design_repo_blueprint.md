
# Repository Blueprint

## Role
See `@shared/roles/solution_architect.md`.

## Objective
Prevent structural improvisation.

## Starting Point (Mandatory)
Do not require the user to specify a full repo design up front.

- Start from rough constraints (deployment target, CI, security posture).
- Converge on a repo structure that matches the plan.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/03_risk_assumption_review.md`
- `artifacts/<project_slug>/04_decision_log.md`
- `artifacts/<project_slug>/05_architecture_data_model.md`
- `artifacts/<project_slug>/06_tech_stack.md`
- `artifacts/<project_slug>/07_ux_design_guide.md` (if applicable; see `@planning/07_design_ux_guide.md`)
- `artifacts/<project_slug>/08_ai_operating_model.md`
- `artifacts/<project_slug>/09_product_backlog.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Default)
See `@shared/input_gate.md`.

Exception:
- `artifacts/<project_slug>/07_ux_design_guide.md` may be missing only if a decision log row in `artifacts/<project_slug>/04_decision_log.md` documents that Step 07 was intentionally skipped due to no user-facing interface.

## Open Questions Gate (Mandatory)
See `@shared/open_questions_gate.md` (Affects: `10_repo_blueprint.md`).

## Instructions
Ask (via `@shared/questions_format.md`) about deployment target, hosting constraints, security posture, and CI expectations. Then design the repo.

## Decision Log Update (Mandatory)
See `@shared/decision_log_update.md`.

## Output Artifact
Write:
`artifacts/<project_slug>/10_repo_blueprint.md`

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Template:

````md
# Repository Blueprint: <Project Name>

## Metadata
- Date: YYYY-MM-DD
- Target: <deployment target>

## Repository Structure
```text
<tree>
```

## Dependency Strategy
- Policy: <short>
- Monorepo vs polyrepo: <choice>

## Environment Model
- Environments: Local | Dev | Staging | Prod
- Configuration sources: <.env/secret manager/etc>
- Required environment variables:
  - `VAR_NAME`: <purpose>

## Containerization
- Approach: Docker | None | Other
- Notes: <short>

## CI Outline
- Lint: <command>
- Typecheck: <command>
- Test: <command>
- Build: <command>
- Security checks: <optional>

## Command Surface
- `dev`: <what it does>
- `test`: <what it does>
- `lint`: <what it does>
- `build`: <what it does>
- `format`: <optional>

## Documentation Structure
- `README.md`: toolkit
- `artifacts/<project_slug>/`: design artifacts
- `docs/`: <optional>

## Decisions
- Related decision log rows (optional):
  - YYYY-MM-DD: <decision>
````

Avoid unnecessary infrastructure.

After producing the artifact (in a separate Chat mode message), state:

> “System design phase complete.”
