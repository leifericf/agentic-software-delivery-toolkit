# Pick Feature

## Role
See `@shared/roles/product_manager.md`.

## Objective
Help the user pick the best next feature/story to implement from the backlog.

## Output Boundary (STRICT)
See `@shared/output_boundary.md`.
Override: no artifact for this step.

## Required Inputs
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/04_decision_log.md`
- `artifacts/<project_slug>/09_product_backlog.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Starting Point (Mandatory)
Do not ask the user to pick perfectly.

- Present a short shortlist.
- Prefer smallest end-user-visible value with low risk and clear acceptance criteria.

## Open Questions Gate (Mandatory)
Before selecting, check `artifacts/<project_slug>/00_open_questions.md`.

If any unchecked `[Blocking]` item affects backlog selection or core scope, stop and ask for an answer.

## Questions (Mandatory)
Ask using `@shared/questions_format.md`:

- What outcome matters most right now?
- Any deadlines or sequencing constraints?
- Any stories that are intentionally deferred?
- Preferred shape of the first increment (thin vertical slice vs internal foundation)?

Then ask the user to choose a single story/feature to implement next (a story ID or a short name).

After the user chooses, instruct them to tag:

> **@implementation/02_plan_feature.md**
