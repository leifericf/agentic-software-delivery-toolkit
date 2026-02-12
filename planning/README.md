# Planning Workflow

The planning workflow is a set of interactive templates for turning a loose problem statement into durable artifacts an implementation agent can reliably build from.

Start rough: you do not need to front-load detail. The agent should pull specifics through back-and-forth questions.

## Steps

Run these **in order**:

1. `planning/01_describe_problem.md`
2. `planning/02_define_requirements.md`
3. `planning/03_review_risks_assumptions.md`
4. `planning/04_log_decisions.md`
5. `planning/05_design_architecture_data_model.md`
6. `planning/06_choose_tech_stack.md`
7. `planning/07_design_ux_guide.md` (skip only if there are no UI surfaces; the agent records the skip in the decision log)
8. `planning/08_define_ai_operating_model.md`
9. `planning/09_create_product_backlog.md`
10. `planning/10_design_repo_blueprint.md`

## Standard Artifact Set

Each step produces one primary artifact in `artifacts/<project_slug>/`:

- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/00_open_questions.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/03_risk_assumption_review.md`
- `artifacts/<project_slug>/04_decision_log.md`
- `artifacts/<project_slug>/05_architecture_data_model.md`
- `artifacts/<project_slug>/06_tech_stack.md`
- `artifacts/<project_slug>/07_ux_design_guide.md`
- `artifacts/<project_slug>/08_ai_operating_model.md`
- `artifacts/<project_slug>/09_product_backlog.md`
- `artifacts/<project_slug>/10_repo_blueprint.md`

## Shared Rules

- The agent tracks unresolved questions in `artifacts/<project_slug>/00_open_questions.md`.
- The agent captures decisions (and changes to decisions) in `artifacts/<project_slug>/04_decision_log.md`.
