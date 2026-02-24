
# Problem Description

## Role
See `@.agentic/shared/roles/product_manager.md`.

## Skills
- Question format: See `@.agentic/shared/skills/interaction/questions_format.md` (cap 3 per turn; respect user batch-size preference if set in `.agentic/.agentic_profile.md`).
- Output boundary: See `@.agentic/shared/skills/gates/output_boundary.md` (Artifact: single `md` fenced block).
- Project bootstrap: See `@.agentic/shared/skills/artifacts/project_bootstrap.md`.

## Starting Point (Mandatory)
Start with a loose, plain-language paragraph.
- Do not ask for exhaustive detail; rough notes/voice dictation are fine.
- Use follow-ups to make scope/constraints concrete.

## Inputs
None required (prior artifacts are optional inputs).

## Project Setup (Mandatory)
Before drafting the problem description artifact:
- Bootstrap `.agentic/artifacts/` using `@.agentic/shared/skills/artifacts/project_bootstrap.md`.

## Objective
Build a clear definition of the problem to solve and the constraints that shape the solution.

## Instructions
1. Ask the user for a single paragraph describing the problem in their own words.
2. Ask follow-ups (Natural / Choice / Binary) to clarify:
   - Who experiences the problem (users/stakeholders)
   - What "success" looks like (outcomes)
   - What is in-scope vs out-of-scope
   - Constraints (technical, operational, legal, integration)
   - Risks and unknowns
3. Identify hidden complexity.
4. Surface assumptions explicitly.
5. Challenge vague language ("fast", "easy", "secure") by asking for concrete definitions.

## Interaction Pattern
Continue the back-and-forth until BOTH conditions are met:

- The problem is clearly understood.
- The user confirms the summary is accurate.

If the user asks to park/drop questions, follow `@.agentic/shared/skills/interaction/questions_format.md` and record parked items in `.agentic/artifacts/open_questions.md`.

## Output Artifact
Write:
`.agentic/artifacts/problem_description.md`

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Optional IDs (Recommended):
- Use IDs only if you expect to reference items later or the list is long.
- If used, prefer: `ACT-001`, `WF-001`, `C-001`, `R-001`, `U-001`, `S-001`.

Template:

```md
# Problem Description: <Project Name>

## Metadata
- Project Meta: `.agentic/artifacts/project_meta.md`
- Date: YYYY-MM-DD
- Owner: <name or role>

## Summary
<5-10 bullet points max>

## Problem
<What is happening today, and what is painful/inefficient/blocked?>

## Desired Outcomes
<What changes if this problem is solved?>

## Stakeholders
- <actor name>
  - Type: Customer | Internal | Partner | Vendor | Regulator
  - Goals: <short>
  - Responsibilities: <short>

## Current Workflows
- <workflow name>
  - Trigger: <what starts it>
  - Steps:
    1. <step>
    2. <step>
  - Success End State: <what "done" means>
  - Failure States:
    - <failure>

## In Scope
- <thing we will do>

## Out of Scope
- <thing we will not do>

## Constraints
- <constraint>
  - Source: Legal | Policy | Org | Budget | Timeline | Market | Operational
  - Notes: <short>

## Risks
- <risk>
  - Likelihood: Low | Medium | High
  - Impact: Low | Medium | High
  - Mitigation: <short>

## Unknowns
- <unknown>
  - Why it matters: <short>
  - Suggested question: <short>

## Simplification Opportunities
- <simplification>
  - Why it helps: <short>

## References
- `.agentic/artifacts/project_meta.md`
- `.agentic/artifacts/open_questions.md`
```

After generating the document, ask:

> “Are you satisfied with the Problem Description?  
> If yes, tag **@.agentic/planning/02_define_requirements.md**.”

(Ask this in a separate Chat mode message after the artifact output.)
