# Planning Workflow

The planning workflow is a set of interactive templates for turning a loose problem statement into durable artifacts an implementation agent can reliably build from.

Optional: run `@setup/01_setup_wizard.md` first to create `.agentic_profile.md` (interaction + engineering preferences).

Start rough: you do not need to front-load detail. The agent should pull specifics through back-and-forth questions.

## Steps

Run these **in order**:

1. `planning/01_describe_problem.md`
2. `planning/02_define_requirements.md`
3. `planning/03_review_risks_assumptions.md`
4. `planning/04_design_ux_guide.md` (skip only if there are no UI surfaces; the agent records the skip in the decision log)
5. `planning/05_create_technical_design.md`
6. `planning/06_create_product_backlog.md`

After Step 06, planning is complete. To begin delivery, tag `@implementation/01_pick_feature.md`.

Optional: if decisions feel scattered, tag `@shared/log_decisions.md` to reconcile them into `artifacts/<project_slug>/decision_log.md`.

## Standard Artifact Set

Each step produces one primary artifact in `artifacts/<project_slug>/`:

- `artifacts/<project_slug>/project_meta.md`
- `artifacts/<project_slug>/open_questions.md`
- `artifacts/<project_slug>/decision_log.md`
- `artifacts/<project_slug>/problem_description.md`
- `artifacts/<project_slug>/product_requirements.md`
- `artifacts/<project_slug>/risk_assumption_review.md`
- `artifacts/<project_slug>/ux_design_guide.md` (if applicable)
- `artifacts/<project_slug>/technical_design.md`
- `artifacts/<project_slug>/product_backlog.md`

## Shared Rules

- The agent tracks unresolved questions in `artifacts/<project_slug>/open_questions.md`.
- The agent captures decisions (and changes to decisions) in `artifacts/<project_slug>/decision_log.md`.
- The agent treats `artifacts/<project_slug>/product_backlog.md` as a living document (includes `Inbox (untriaged)` and `In product (shipped)`).
