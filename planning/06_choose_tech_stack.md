
# Technology Stack

## Role
See `@shared/roles/technical_advisor.md`.

## Objective
Select stable technology aligned with the architecture.

## Starting Point (Mandatory)
Do not ask the user to research or pre-decide everything.

- Collect rough constraints/preferences.
- Propose a short option set; narrow via questions.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/03_risk_assumption_review.md`
- `artifacts/<project_slug>/04_decision_log.md`
- `artifacts/<project_slug>/05_architecture_data_model.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Default)
See `@shared/input_gate.md`.

## Open Questions Gate (Mandatory)
See `@shared/open_questions_gate.md` (Affects: `06_tech_stack.md`).

## Bias
Favor:
- Proven tools
- Large ecosystems
- High training data availability
- Operational simplicity

Avoid trend-driven choices.

## Instructions
Before recommending, ask (via `@shared/questions_format.md`) about:
- Team expertise
- Longevity expectations
- Hosting preferences
- Performance needs
- Operational tolerance

Explain tradeoffs clearly.

## Decision Log Update (Mandatory)
See `@shared/decision_log_update.md`.

## Output Artifact
Write:
`artifacts/<project_slug>/06_tech_stack.md`

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Template:

```md
# Technology Stack: <Project Name>

## Metadata
- Date: YYYY-MM-DD
- Related:
  - Architecture: `artifacts/<project_slug>/05_architecture_data_model.md`
  - Decision Log: `artifacts/<project_slug>/04_decision_log.md`

## Stack Summary
<5-10 bullets max>

## Backend
- Language/Runtime: <choice>
- Web toolkit: <choice>
- API style: REST | GraphQL | RPC
- Background jobs: <choice>

## Frontend
- Approach: SPA | MPA | SSR | Static
- UI toolkit: <choice>
- Styling: <choice>

## Data
- Primary database: <choice>
- Migrations: <choice>
- Search/indexing: <choice or ->
- Caching: <choice or ->

## Infrastructure Posture
- Hosting: <choice>
- Environments: Local | Dev | Staging | Prod
- Deployment style: <choice>

## Observability
- Logging: <choice>
- Metrics: <choice>
- Tracing: <choice or ->

## Dependency Philosophy
- Policy: <short>
- Update cadence: <short>

## Testing Posture
- Unit: <short>
- Integration: <short>
- E2E: <short>

## Decisions
- Related decision log rows (optional):
  - YYYY-MM-DD: <decision>
```

Then ask:

> “Lock this stack?  
> If yes, tag **@planning/07_design_ux_guide.md** (or skip per Step 07 and tag **@planning/08_define_ai_operating_model.md**).”

(Ask this in a separate Chat mode message after the artifact output.)
