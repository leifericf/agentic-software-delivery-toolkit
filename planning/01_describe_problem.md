
# Problem Description

## Role
See `@shared/roles/product_manager.md`.

## Operating Mode
- Interactive discovery. No tech yet.
- Ask questions via `@shared/questions_format.md` (cap 3 per turn; respect user batch-size preference if set in `.agentic_profile.md`).

## Starting Point (Mandatory)
Start with a loose, plain-language paragraph.
- Do not ask for exhaustive detail; rough notes/voice dictation are fine.
- Use follow-ups to make scope/constraints concrete.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Inputs
None required (prior artifacts are optional inputs).

## Open Questions File (Mandatory)
After `project_slug` is locked, ensure `artifacts/<project_slug>/00_open_questions.md` exists.

If it does not exist, initialize it with this minimal valid structure:

```md
# Open Questions

## Open

- [ ] [Blocking] [Affects: <artifact_filename>.md] <question> (Answer: TBD)
- [ ] [Affects: <artifact_filename>.md] <question> (Answer: TBD)

## Resolved

- [x] [Affects: <artifact_filename>.md] <question> (Answer: <answer>) (Date: YYYY-MM-DD)
```

Notes:
- Use `[Blocking]` only when you truly cannot proceed without the answer.
- `Affects` should list artifact filenames (e.g. `02_product_requirements.md`, `05_architecture_data_model.md`).

If any clarification questions come up during this step, add them as unchecked items under `## Open`.

## Project Slug + Artifact Bootstrapping (Mandatory)
1) Ask for a human-friendly project name.
2) Suggest a derived `project_slug` and have the user choose.

Slug rules (STRICT):
- lowercase snake_case
- letters, numbers, underscores only
- no spaces

Slug selection (MANDATORY):
- Provide 3-5 slug options using the format in `@shared/questions_format.md`.
- Include an option for a custom slug.
- Validate the chosen/custom slug against the slug rules.

Then initialize the artifacts directory and shared files:

1. Create: `artifacts/<project_slug>/`
2. Create: `artifacts/<project_slug>/00_project_meta.md` with this minimal valid structure (fill in Project Name and Project Slug):

```md
# Project Meta

## Identity
- Project Name: <Project Name>
- Project Slug: <project_slug>

## Ownership
- Owner: <name or role>

## Dates
- Started: YYYY-MM-DD

## Links
- Repository: <optional>
- Docs: <optional>

## Notes
- <optional>
```

3. Create: `artifacts/<project_slug>/00_open_questions.md` if it does not already exist (see structure above)
4. Create: `artifacts/<project_slug>/04_decision_log.md` with this minimal valid structure:

```md
# Decision Log

| Date | Decision | Why | Tradeoff |
| --- | --- | --- | --- |
| YYYY-MM-DD | <decision> | <why> | <tradeoff> |
```

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

If the user asks to park/drop questions, follow `@shared/questions_format.md` and record parked items in `artifacts/<project_slug>/00_open_questions.md`.

## Output Artifact
Write:
`artifacts/<project_slug>/01_problem_description.md`

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Optional IDs (Recommended):
- Use IDs only if you expect to reference items later or the list is long.
- If used, prefer: `ACT-001`, `WF-001`, `C-001`, `R-001`, `U-001`, `S-001`.

Template:

```md
# Problem Description: <Project Name>

## Metadata
- Project Meta: `artifacts/<project_slug>/00_project_meta.md`
- Project Slug: <project_slug>
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
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/00_open_questions.md`
```

After generating the document, ask:

> “Are you satisfied with the Problem Description?  
> If yes, tag **@planning/02_define_requirements.md**.”

(Ask this in a separate Chat mode message after the artifact output.)
