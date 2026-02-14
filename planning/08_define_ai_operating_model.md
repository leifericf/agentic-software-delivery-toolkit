
# AI Operating Model

## Role
See `@shared/roles/solution_architect.md`.

## Objective
Create guardrails BEFORE AI writes code.

## Starting Point (Mandatory)
Do not require the user to define a full policy up front.

- Start from rough preferences (tools, autonomy, risk tolerance).
- Turn them into enforceable rules.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/03_risk_assumption_review.md`
- `artifacts/<project_slug>/04_decision_log.md`
- `artifacts/<project_slug>/05_architecture_data_model.md`
- `artifacts/<project_slug>/06_tech_stack.md`
- `artifacts/<project_slug>/07_ux_design_guide.md` (if applicable; see `@planning/07_design_ux_guide.md`)
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Default)
See `@shared/input_gate.md`.

Exception:
- `artifacts/<project_slug>/07_ux_design_guide.md` may be missing only if a decision log row in `artifacts/<project_slug>/04_decision_log.md` documents that Step 07 was intentionally skipped due to no user-facing interface.

## Open Questions Gate (Mandatory)
See `@shared/open_questions_gate.md` (Affects: `08_ai_operating_model.md`).

## Instructions
Ask (via `@shared/questions_format.md`) about tools, autonomy level, and risk tolerance. Then define the guardrails.

## Decision Log Update (Mandatory)
See `@shared/decision_log_update.md`.

## Output Artifact
Write to:

`artifacts/<project_slug>/08_ai_operating_model.md`

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Template:

```md
# AI Operating Model: <Project Name>

## Metadata
- Date: YYYY-MM-DD
- Owner: <name or role>

## Tools
- Allowed tools:
  - <tool>
- Disallowed tools:
  - <tool>

## Autonomy Model
- Default mode: Advisory | Pair | Autonomous
- Allowed actions without asking:
  - <action>
- Actions that require explicit approval:
  - <action>

## AI Constitution
- <principle>

## File Editing Rules
- Allowed directories: <paths>
- Forbidden files/patterns: <patterns>
- Edit approach: Small diffs | Large diffs

## Boundary Enforcement
- What the AI must not do: <bullets>
- Escalation triggers: <bullets>

## Complexity Limits
- Maximum services/components before re-justification: <number>
- Default to: Monolith | Modular monolith | Services

## AI Definition of Done
- <check>

## Prompt Templates
### Implementation Task
<template text>

### Code Review
<template text>

### Debugging
<template text>
```

Goal: prevent over-engineering.

Then ask:

> “AI guardrails ready?  
> If yes, tag **@planning/09_create_product_backlog.md**.”

(Ask this in a separate Chat mode message after the artifact output.)
