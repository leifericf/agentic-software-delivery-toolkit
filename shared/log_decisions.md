# Log Decisions (Optional)

## Role
See `@shared/roles/quality_engineer.md`.

## Objective
Capture decisions quickly so future agents do not undo them.

This prompt updates a single shared artifact: `artifacts/<project_slug>/00_decision_log.md`.

## Starting Point (Mandatory)
Do not expect the user to write formal decision docs.

- Ask for rough decisions in plain language (bullets fine).
- Convert to short table rows; iterate until accurate.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Artifact Behavior
Append-only living document.
- Only change prior rows to fix factual errors.
- If a decision changes, append a new row referencing the earlier one.

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/03_risk_assumption_review.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Default)
See `@shared/input_gate.md`.

## Open Questions Gate (Mandatory)
See `@shared/open_questions_gate.md` (Affects: `00_decision_log.md`).

## Instructions
1. Review all prior artifacts.
2. Extract decisions already made.
3. Ask if any major decisions remain unresolved.
4. Use the question format in `@shared/questions_format.md` to finalize them.

## Output Artifact
Write:
`artifacts/<project_slug>/00_decision_log.md`

File format (STRICT):

```md
# Decision Log

| Date | Decision | Why | Tradeoff |
| --- | --- | --- | --- |
| YYYY-MM-DD | <decision> | <why> | <tradeoff> |
```

Then ask:

> "Decisions captured correctly? Continue the workflow."

(Ask this in a separate Chat mode message after the artifact output.)
