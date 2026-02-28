# Pick Feature

## Role
See `@.agentic/shared/roles/product_manager.md`.

## Objective
Help the user pick the best next feature/story to implement from the backlog.

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/output_boundary.md`.
Override: no artifact for this step.

## Required Inputs
- `.agentic/artifacts/product_requirements.md`
- `.agentic/artifacts/decision_log.md`
- `.agentic/artifacts/product_backlog.md`
- `.agentic/artifacts/open_questions.md`

## Starting Point (Mandatory)
Do not ask the user to pick perfectly.

- Present a short shortlist.
- Prefer smallest end-user-visible value with low risk and clear acceptance criteria.
- Treat `.agentic/artifacts/product_backlog.md` as a living document with buckets (e.g. `Now / Next`, `Later`, `Inbox (untriaged)`, `In product (shipped)`).

## Open Questions Gate (Mandatory)
Before selecting, check `.agentic/artifacts/open_questions.md`.

If any unchecked `[Blocking]` item affects backlog selection or core scope, stop and ask for an answer.

## Questions (Mandatory)
Ask using `@.agentic/shared/skills/interaction/questions_format.md`:

Ask a short batch (max 3) tailored to the current backlog + PRD context.

Use these as *themes*, not hard-coded questions:
- Outcome to optimize for (helps choose between competing stories)
- Sequencing/prerequisite constraints (ordering dependencies; not timelines)
- Preferred shape of the first increment (thin vertical slice vs foundation-first)

Guidelines:
- Prefer **Choice mode** when you can offer 3-5 mutually-exclusive options that match the backlog's real branches.
- Do not copy/paste a fixed option list; derive options from the user's backlog language.
- Always include "Write your own answer" and "Can't answer / N/A" in Choice mode.

Example (Choice mode; rewrite options to match this backlog):

1) What outcome should we optimize for with the next feature?
A) <option derived from backlog>
B) <option derived from backlog>
C) <option derived from backlog>
D) Write your own answer
E) Can't answer / N/A

Before you present the shortlist:

- Scan `Inbox (untriaged)` in `.agentic/artifacts/product_backlog.md`.
- Promote 0-2 items into `Now / Next` if they clearly match what the user cares about right now; otherwise move them to `Later` or leave them in the inbox if too vague.
- If the backlog feels stale or the inbox is growing, recommend tagging **@.agentic/implementation/06_triage_backlog.md**.

Then ask the user to choose a single story/feature to implement next (a story ID or a short name).

After the user chooses, instruct them to tag:

> **@.agentic/implementation/02_plan_feature.md**
