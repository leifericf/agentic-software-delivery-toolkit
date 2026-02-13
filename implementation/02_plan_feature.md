# Feature Plan (Slices + Tasks)

## Role
You are a delivery-focused technical lead.

## Objective
Produce one plan that includes (1) incremental chunks and (2) a task list (incl. tests + automation). This replaces the old two-step flow.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Required Inputs
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/04_decision_log.md`
- `artifacts/<project_slug>/05_architecture_data_model.md`
- `artifacts/<project_slug>/06_tech_stack.md`
- `artifacts/<project_slug>/07_ux_design_guide.md` (if applicable)
- `artifacts/<project_slug>/08_ai_operating_model.md`
- `artifacts/<project_slug>/09_product_backlog.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Starting Point (Mandatory)
Do not require exhaustive design.

- Draft slices and tasks directly from the artifacts.
- Ask only what is needed to avoid wrong assumptions.
- Aim for 2-6 chunks; each chunk independently testable.
- When you select a story from the backlog to implement, define its Conditions of Done in this plan (3-7 short, testable bullets).

## Open Questions Gate (Mandatory)
See `@shared/open_questions_gate.md` (Blockers: any `[Blocking]` item affecting this feature).

## Output Artifact
Write:
`artifacts/<project_slug>/tasks/plan-<feature_slug>.md`

## Output Format (Recommended)
Use this structure (adjust as needed). Prefer clarity over ceremony.

```md
# Plan: <Feature Name>

## Metadata
- Date: YYYY-MM-DD
- Backlog item: <epic/story name>
- Feature slug: <feature_slug>
- Related:
  - PRD: `artifacts/<project_slug>/02_product_requirements.md`
  - Architecture: `artifacts/<project_slug>/05_architecture_data_model.md`
  - Tech stack: `artifacts/<project_slug>/06_tech_stack.md`
  - Decision log: `artifacts/<project_slug>/04_decision_log.md`

## Context
- Intended outcome: <short>

## Conditions of Done
- <short, testable condition>
- <short, testable condition>
- <short, testable condition>

## Chunks
- <chunk name> (optional: `CH-001: <chunk name>`)
  - User value: <short>
  - Scope: <short>
  - Ship criteria: <short, testable>
  - Rollout notes: <flags/migrations/backfill or ->

## Relevant Files (Expected)
- `<path>` - <why>

## Notes
- Include unit/integration tests where appropriate.
- Include any migrations, backfills, or feature flags explicitly.
- Prefer small, reviewable commits that map to chunks.

## Tasks
- [ ] Create and checkout a new branch (e.g. `feature/<feature_slug>`)

- [ ] Implement: <chunk name>
  - [ ] <task>
  - [ ] <task>
  - [ ] Tests: <what to add>

- [ ] Quality gate
  - [ ] Run formatters
  - [ ] Run linters
  - [ ] Run tests

## Open Questions
- <any non-blocking questions to capture or ->
```

Then ask:

> "If anything feels ambiguous or risky, tag **@implementation/04_review_plan.md**. Otherwise tag **@implementation/05_execute_plan.md** to start implementation."
