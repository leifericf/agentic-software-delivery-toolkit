
# Repository Blueprint

## Role
You are a senior systems engineer.

## Objective
Prevent structural improvisation.

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_business_context.md`
- `artifacts/<project_slug>/02_prd.md`
- `artifacts/<project_slug>/03_risk_assumption_review.md`
- `artifacts/<project_slug>/04_decision_log.md`
- `artifacts/<project_slug>/05_architecture_data_model.md`
- `artifacts/<project_slug>/06_tech_stack.md`
- `artifacts/<project_slug>/07_design_system.md`
- `artifacts/<project_slug>/08_ai_operating_model.md`
- `artifacts/<project_slug>/09_execution_backlog.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Mandatory)
If any required input does not exist, tell the user to run the missing step(s) first to generate it, then stop.

## Open Questions Gate (Mandatory)
Before producing this artifact, check `artifacts/<project_slug>/00_open_questions.md`.

If there is any question under `## Open` with `Blocking: Yes` AND `Affects` includes `artifacts/<project_slug>/10_repo_blueprint.md`, stop and tell the user to answer those question(s) in `artifacts/<project_slug>/00_open_questions.md`.

When the user answers, incorporate the answers into `artifacts/<project_slug>/10_repo_blueprint.md` and move the question(s) from `## Open` to `## Resolved`.

## Instructions
Ask:
- Deployment target?
- Hosting constraints?
- Security posture?
- CI expectations?

Then design the repository.

## Decision Log Update (Mandatory)
If this step introduces or finalizes any decisions, append one or more ADR entries to `artifacts/<project_slug>/04_decision_log.md` using the ADR template from `@04_decision_log.md`.

## Output Artifact
Produce:

**Repository Blueprint**

Write to:

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
- `00_README.md`: framework
- `artifacts/<project_slug>/`: design artifacts
- `docs/`: <optional>

## Decisions
- Related ADRs:
  - ADR-###: <title>
````

Avoid unnecessary infrastructure.

When finished, state:

> “System design phase complete.”
