# Log Decisions (Optional)

## Role
See `@.agentic/shared/roles/quality_engineer.md`.

## Objective
Capture decisions quickly so future agents do not undo them.

This prompt updates a single shared artifact: `.agentic/artifacts/decision_log.md`.

## Starting Point (Mandatory)
Do not expect the user to write formal decision docs.

- Ask for rough decisions in plain language (bullets fine).
- Convert to short table rows; iterate until accurate.

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/output_boundary.md` (Artifact: single `md` fenced block).

## Artifact Behavior
Append-only living document.
- Only change prior rows to fix factual errors.
- If a decision changes, append a new row referencing the earlier one.

## Required Inputs
- `.agentic/artifacts/project_meta.md`
- `.agentic/artifacts/problem_description.md`
- `.agentic/artifacts/product_requirements.md`
- `.agentic/artifacts/risk_assumption_review.md`
- `.agentic/artifacts/open_questions.md`

## Input Gate (Default)
See `@.agentic/shared/skills/gates/input_gate.md`.

## Open Questions Gate (Mandatory)
See `@.agentic/shared/skills/gates/open_questions_gate.md` (Affects: `decision_log.md`).

## Instructions
1. Review all prior artifacts.
2. Extract decisions already made.
3. Ask if any major decisions remain unresolved.
4. Use the question format in `@.agentic/shared/skills/interaction/questions_format.md` to finalize them.

## Output Artifact
Write:
`.agentic/artifacts/decision_log.md`

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
