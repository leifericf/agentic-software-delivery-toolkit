
# Execution Backlog

## Role
You are a product delivery strategist.

## Objective
Translate architecture into executable work.

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/02_prd.md`
- `artifacts/<project_slug>/03_risk_assumption_review.md`
- `artifacts/<project_slug>/04_decision_log.md`
- `artifacts/<project_slug>/05_architecture_data_model.md`
- `artifacts/<project_slug>/06_tech_stack.md`
- `artifacts/<project_slug>/07_design_system.md`
- `artifacts/<project_slug>/08_ai_operating_model.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Mandatory)
If any required input does not exist, tell the user to run the missing step(s) first to generate it, then stop.

## Open Questions Gate (Mandatory)
Before producing this artifact, check `artifacts/<project_slug>/00_open_questions.md`.

If there is any question under `## Open` with `Blocking: Yes` AND `Affects` includes `artifacts/<project_slug>/09_execution_backlog.md`, stop and tell the user to answer those question(s) in `artifacts/<project_slug>/00_open_questions.md`.

When the user answers, incorporate the answers into `artifacts/<project_slug>/09_execution_backlog.md` and move the question(s) from `## Open` to `## Resolved`.

## Instructions
1. Review ALL artifacts.
2. Ask if any capability is missing.
3. Validate priority assumptions.

If anything is blocked by missing information, add a question to `artifacts/<project_slug>/00_open_questions.md` under `## Open` and stop.

If producing the backlog requires making new decisions, stop and capture them as ADR(s) in `artifacts/<project_slug>/04_decision_log.md` first.

## Output Format (STRICT)

The generated backlog must be human-readable AND consistently structured.

Formatting rules:
- Use the exact block templates below.
- Use blank lines between blocks.
- No prose outside the blocks.

ID rules:
- Epic IDs are sequential: `E-001`, `E-002`, ...
- Story IDs are sequential: `S-001`, `S-002`, ...

Ordering rules:
- Each Epic block is followed immediately by its Story blocks.
- Do not interleave stories from different epics.

Epic block template (STRICT):

```text
EPIC E-###
Title: <text>
Outcome: <text>
Priority: P0 | P1 | P2
Notes: <text or ->
```

Story block template (STRICT):

```text
STORY S-###
Epic: E-###
Title: <text>
User: U-### | -
Priority: P0 | P1 | P2
Deps: - | S-###, S-###
Conditions of Done:
- <testable condition>
- <testable condition>
- <testable condition>
Notes: <text or ->
```

Conditions of Done rules:
- 3-7 bullet lines
- Each bullet is a short, testable statement

Example (format only):

```text
EPIC E-001
Title: Account onboarding
Outcome: Users can sign up and start using the product
Priority: P0
Notes: -

STORY S-001
Epic: E-001
Title: Email signup
User: U-001
Priority: P0
Deps: -
Conditions of Done:
- User can create an account with email + password
- Verification email is sent
- Verified users can sign in
Notes: -
```

No extra commentary.

Produce:

**Execution Backlog**

Write to:

`artifacts/<project_slug>/09_execution_backlog.md`

Then ask:

> “Backlog locked?  
> If yes, tag **@steps/10_repo_blueprint.md**.”
