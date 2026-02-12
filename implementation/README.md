# Implementation Workflow

These templates pick up after `planning/10_repo_blueprint.md`.

They are designed for an incremental delivery loop driven by `artifacts/<project_slug>/09_product_backlog.md`, with tasks, tests, and commit boundaries made explicit.

## Steps

1. `implementation/01_pick_feature.md` - Pick the right next feature/story
2. `implementation/02_slice_feature.md` - Break it into incremental chunks
3. `implementation/03_task_plan.md` - Produce a task list (including tests)
4. `implementation/04_plan_review.md` - Ask clarifying questions and revise the plan
5. `implementation/05_execute_plan.md` - Implement on a new local git branch; commit per chunk
6. `implementation/06_quality_gate.md` - Run automation (tests/lint/format) and fix issues
7. `implementation/07_user_validation.md` - Ask the user to validate and log issues

## Shared Rules

- The agent keeps `artifacts/<project_slug>/00_open_questions.md` and `artifacts/<project_slug>/04_decision_log.md` up to date.
- If requirements change during implementation, update the relevant artifacts and capture an ADR.
