
# Risk & Assumption Review

## Role
See `@shared/roles/quality_engineer.md`.

## Objective
Expose hidden risks BEFORE architecture begins.

## Starting Point (Mandatory)
Do not ask the user to enumerate risks exhaustively.

- Pull likely risks/assumptions from existing artifacts.
- Use targeted questions to confirm/reject/refine.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Default)
See `@shared/input_gate.md`.

## Open Questions Gate (Mandatory)
See `@shared/open_questions_gate.md` (Affects: `03_risk_assumption_review.md`).

## Instructions
Analyze everything produced so far.

Identify:
- Missing requirements
- Contradictions
- Scope creep
- Over-engineering risks
- Dangerous assumptions
- Organizational risks

## Question Style
Ask questions using the format in `@shared/questions_format.md`.

Prefer:
- Binary
- Choice

Avoid open-ended prompts unless necessary.

## Interaction Pattern
Continue until uncertainty is low.

## Output Artifact
Write:
`artifacts/<project_slug>/03_risk_assumption_review.md`

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Optional IDs (Recommended):
- Use IDs only if you expect to reference items later or the list is long.
- If used, prefer: `T-001`, `R-001`, `A-001`, `S-001`.

Template:

```md
# Risk & Assumption Review: <Project Name>

## Metadata
- Date: YYYY-MM-DD
- Reviewed Artifacts:
  - `artifacts/<project_slug>/01_problem_description.md`
  - `artifacts/<project_slug>/02_product_requirements.md`
- Open Questions:
  - `artifacts/<project_slug>/00_open_questions.md`

## Confirmed Truths
- <statement>
  - Evidence: <what supports this>

## Key Risks
- <risk>
  - Category: Product | Technical | Data | Security | Legal | Operational | Org
  - Likelihood: Low | Medium | High
  - Impact: Low | Medium | High
  - Mitigation: <short>
  - Owner: <role>
  - Related:
    - Artifacts: <optional list>
    - Open questions: <optional list or ->

## Dangerous Assumptions
- <assumption>
  - Why dangerous: <short>
  - How to validate: <short>
  - If false, what breaks: <short>

## Scope Creep Watchlist
- <potential creep>

## Over-Engineering Traps
- <trap>
  - Simplest safe alternative: <short>

## Recommended Simplifications
- <simplification>
  - Tradeoff: <what we lose>
  - Why acceptable: <short>
```

Then ask:

> “Ready to lock decisions?  
> If yes, tag **@planning/04_design_ux_guide.md**.”

(Ask this in a separate Chat mode message after the artifact output.)
