
# Product Requirements Document

## Role
See `@shared/roles/product_manager.md`.

## Objective
Define WHAT must be built — not HOW.

## Starting Point (Mandatory)
Do not require front-loaded detail.
- Start rough (paragraph or a few bullets), then iterate to make scope/requirements/AC concrete.

## Operating Rules
- No tech stack discussion.
- No architecture.
- No timelines.
- No estimates.

## Output Boundary (STRICT)
See `@shared/skills/gates/output_boundary.md` (Artifact: single `md` fenced block).

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Default)
See `@shared/skills/gates/input_gate.md`.

## Open Questions Gate (Mandatory)
See `@shared/skills/gates/open_questions_gate.md` (Affects: `02_product_requirements.md`).

## Instructions
1. Review the Problem Description first.
2. Ask clarification questions where ambiguity exists.
3. Ask questions using the format in `@shared/skills/interaction/questions_format.md`.
4. Identify contradictions.
5. Highlight assumptions.

When you identify unclear requirements, add them to `artifacts/<project_slug>/00_open_questions.md` under `## Open`.

Do not include an "Open Questions" section in the PRD.

## Interaction Pattern
Iterate until scope is crisp and easy to remember.

## Output Artifact
Write:
`artifacts/<project_slug>/02_product_requirements.md`

## Output Format (STRICT)
The generated PRD must use this exact Markdown structure and headings, in this order.

Optional IDs (Recommended):
- Use IDs only if you expect to reference items later or the doc is large.
- If used, prefer: `G-001`, `U-001`, `FR-001`, `NFR-001`, `WF-001`, `A-001`.

Template:

```md
# PRD: <Product/Project Name>

## Metadata
- Version: 0.1
- Date: YYYY-MM-DD
- Owner: <name or role>

## Problem Statement
<1-3 paragraphs>

## Goals
- <goal>

## Non-Goals
- <explicitly out of scope>

## Users
- <user type> (Primary | Secondary | Internal)

## Scope
<1-2 paragraphs>

## Functional Requirements
- <title>
  - Description: <1-3 sentences>
  - Priority: Must | Should | Could
  - Acceptance Criteria:
    - <criterion>
    - <criterion>

## Non-Functional Requirements
- <title>
  - Target: <measurable target when possible>
  - Priority: Must | Should | Could

## Workflows
- <workflow name>
  - Trigger: <what starts it>
  - Steps:
    1. <step>
    2. <step>
  - Success End State: <what "done" means>
  - Failure States:
    - <failure>

## Success Criteria
- <metric or observable outcome>

## Assumptions
- <assumption>

```

Produce a production-grade PRD using the template above.

Then ask:

> “Does the PRD reflect what should be built?  
> If yes, tag **@planning/03_review_risks_assumptions.md**.”

(Ask this in a separate Chat mode message after the artifact output.)
