# Planning Workflow

Turn a loose problem statement into durable artifacts in `.agentic/artifacts/`.

Optional: Tag `@.agentic/setup/01_setup_wizard.md` first to create `.agentic/.agentic_profile.md`.

Start rough: you do not need to front-load detail. The agent should pull specifics through questions.

Windows note: some tools treat `@<path>` as a file include and require `/` separators.
Use `@.agentic/planning/01_describe_problem.md` (not `@.agentic\planning\01_describe_problem.md`).

## Steps

Run these **in order**:

1. `.agentic/planning/01_describe_problem.md`
2. `.agentic/planning/02_define_requirements.md`
3. `.agentic/planning/03_review_risks_assumptions.md`
4. `.agentic/planning/04_design_ux_guide.md` (skip only if there are no UI surfaces; the agent records the skip in the decision log)
5. `.agentic/planning/05_create_technical_design.md`
6. `.agentic/planning/06_create_product_backlog.md`

After Step 06, planning is complete. To begin delivery, tag `@.agentic/implementation/01_pick_feature.md`.

Optional: if decisions feel scattered, tag `@.agentic/shared/log_decisions.md` to reconcile them into `.agentic/artifacts/decision_log.md`.

## Artifacts

Outputs (one primary artifact per step):

- `.agentic/artifacts/project_meta.md`
- `.agentic/artifacts/open_questions.md`
- `.agentic/artifacts/decision_log.md`
- `.agentic/artifacts/problem_description.md`
- `.agentic/artifacts/product_requirements.md`
- `.agentic/artifacts/risk_assumption_review.md`
- `.agentic/artifacts/ux_design_guide.md` (if applicable)
- `.agentic/artifacts/technical_design.md`
- `.agentic/artifacts/product_backlog.md`

## Shared Rules

- The agent tracks unresolved questions in `.agentic/artifacts/open_questions.md`.
- The agent captures decisions (and changes to decisions) in `.agentic/artifacts/decision_log.md`.
- The agent treats `.agentic/artifacts/product_backlog.md` as a living document (includes `Inbox (untriaged)` and `In product (shipped)`).
