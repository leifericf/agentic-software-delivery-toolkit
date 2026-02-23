# Pick Feature

## Role
See `@shared/roles/product_manager.md`.

## Objective
Help the user pick the best next feature/story to implement from the backlog.

## Output Boundary (STRICT)
See `@shared/skills/gates/output_boundary.md`.
Override: no artifact for this step.

## Required Inputs
- `artifacts/<project_slug>/product_requirements.md`
- `artifacts/<project_slug>/decision_log.md`
- `artifacts/<project_slug>/product_backlog.md`
- `artifacts/<project_slug>/open_questions.md`

## Starting Point (Mandatory)
Do not ask the user to pick perfectly.

- Present a short shortlist.
- Prefer smallest end-user-visible value with low risk and clear acceptance criteria.
- Treat `artifacts/<project_slug>/product_backlog.md` as a living document with buckets (e.g. `Now / Next`, `Later`, `Inbox (untriaged)`, `In product (shipped)`).

## Open Questions Gate (Mandatory)
Before selecting, check `artifacts/<project_slug>/open_questions.md`.

If any unchecked `[Blocking]` item affects backlog selection or core scope, stop and ask for an answer.

## Questions (Mandatory)
Ask using `@shared/skills/interaction/questions_format.md`:

- What outcome matters most right now?
- Any deadlines or sequencing constraints?
- Any stories that are intentionally deferred?
- Preferred shape of the first increment (thin vertical slice vs internal foundation)?

Before you present the shortlist:

- Scan `Inbox (untriaged)` in `artifacts/<project_slug>/product_backlog.md`.
- Promote 0-2 items into `Now / Next` if they clearly match what the user cares about right now; otherwise move them to `Later` or leave them in the inbox if too vague.
- If the backlog feels stale or the inbox is growing, recommend tagging **@implementation/07_triage_backlog.md**.

Then ask the user to choose a single story/feature to implement next (a story ID or a short name).

After the user chooses, instruct them to tag:

> **@implementation/02_plan_feature.md**
