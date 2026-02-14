
# Product Backlog

## Role
See `@shared/roles/product_delivery_strategist.md`.

## Objective
Translate architecture into executable work.

## Starting Point (Mandatory)
Do not ask the user to pre-write a detailed backlog.

- Draft a simple hierarchy from existing artifacts.
- Iterate to confirm priority, sequencing, and scope.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `text` fenced block).

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
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Default)
See `@shared/input_gate.md`.

Exception:
- `artifacts/<project_slug>/07_ux_design_guide.md` may be missing only if a decision log row in `artifacts/<project_slug>/04_decision_log.md` documents that Step 07 was intentionally skipped due to no user-facing interface.

## Open Questions Gate (Mandatory)
See `@shared/open_questions_gate.md` (Affects: `09_product_backlog.md`).

## Instructions
1. Review all artifacts.
2. Ask via `@shared/questions_format.md`.
3. Check for missing capabilities.
4. Validate priority assumptions.

If anything is blocked by missing information, add an unchecked `[Blocking]` item under `## Open` in `artifacts/<project_slug>/00_open_questions.md` and stop.

If producing the backlog requires making new decisions, stop and capture them as decision log row(s) in `artifacts/<project_slug>/04_decision_log.md` first.

## Output Format (STRICT)
The generated backlog must be human-readable AND consistently structured.

Keep it simple:
- Flat list of high-level items.
- Under each: flat list of lower-level items.
- No IDs; no special fields/blocks.
- No Conditions of Done here (add later when the item is selected for implementation).
- Priority is order (higher = higher priority).

Ordering rules:
- Each high-level item appears once.
- Each high-level item is followed immediately by its indented lower-level items.
- Do not interleave lower-level items across different high-level items.

Format (STRICT):
- Output exactly one markdown list.
- High-level items are top-level list items.
- Lower-level items are indented two spaces under their parent item.
- No prose before/after the list.

Example (format only):

```text
- Account onboarding
  - Email signup
  - Email verification
  - Password reset

- Billing
  - Add payment method
  - View invoices
```

Write:
`artifacts/<project_slug>/09_product_backlog.md`

Then ask:

> “Backlog locked?  
> If yes, tag **@planning/10_design_repo_blueprint.md**.”

(Ask this in a separate Chat mode message after the artifact output.)
