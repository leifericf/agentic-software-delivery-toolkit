# Implementation Workflow

These templates pick up after `planning/06_create_product_backlog.md`.

If present, the agent should apply your `.agentic_profile.md` preferences during implementation.

They are designed for an incremental delivery loop driven by `artifacts/<project_slug>/product_backlog.md`, with tasks, tests, and commit boundaries made explicit.

## Steps

Lean loop (default):

1. `implementation/01_pick_feature.md` - Pick the right next feature/story
2. `implementation/02_plan_feature.md` - Create slices + task list (single plan file)
3. `implementation/04_execute_plan.md` - Implement incrementally; run automation; hand off for user validation

Optional steps (use when needed):

- `implementation/03_review_plan.md` - Extra plan clarification when risk/ambiguity is high
- `implementation/05_run_quality_gate.md` - Dedicated automation run/fix pass
- `implementation/06_validate_with_user.md` - Dedicated user validation + issue capture pass
- `implementation/07_triage_backlog.md` - Triage + reprioritize the backlog (incl. inbox cleanup)

## Shared Rules

- The agent keeps `artifacts/<project_slug>/open_questions.md` and `artifacts/<project_slug>/decision_log.md` up to date.
- The agent keeps `artifacts/<project_slug>/product_backlog.md` up to date (capture new ideas in `Inbox (untriaged)` and move shipped items to `In product (shipped)`).
- If requirements change during implementation, update the relevant artifacts and add a decision log row.
- Planning includes a short functional elicitation gate before task decomposition (see `implementation/02_plan_feature.md`).
