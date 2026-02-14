# Plan Review

## Role
See `@shared/roles/quality_engineer.md`.

## Objective
Ask clarifying questions about the implementation plan and revise it based on the user's answers.

The default review lens is functional correctness (user-facing acceptance). Technical risk questions are allowed only when they translate into user-visible behavior or change cost.

This step is optional. Use it when the task plan has unclear acceptance criteria, risky migrations, external dependencies, or any decision that would be expensive to change later.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Required Inputs
- `artifacts/<project_slug>/tasks/plan-<feature_slug>.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Starting Point (Mandatory)
Assume the plan has missing details.

- Ask only questions that change implementation or acceptance criteria.
- Keep the loop short.

## Question Style
- Prefer plain language a non-technical product owner can answer.
- Avoid technical design debates.
- If a technical detail is unavoidable, ask about the user-visible tradeoff.
- Use `@shared/questions_format.md`.

## Instructions
1. Read the plan and treat `## Functional Snapshot` and `## Conditions of Done` as the source of truth.
2. Check `artifacts/<project_slug>/00_open_questions.md` and do not re-ask already-answered questions.
3. Ask the smallest set of questions needed to remove ambiguity, using the order in `@shared/functional_elicitation.md`.
4. Focus on gaps that will cause rework:
   - Success criteria not observable/testable
   - User flow ambiguity
   - Missing "must never happen" / unacceptable behavior
   - Unstated edge-case behavior
   - Business rules that could be interpreted multiple ways
   - Integration expectations, especially failure/degraded behavior
   - MVI vs deferred scope unclear
5. If answers imply new decisions, instruct the user that the agent will add decision log row(s) during execution.
6. Revise the task plan accordingly.

Then ask:

> "Plan locked. Tag **@implementation/04_execute_plan.md** to implement it." 
