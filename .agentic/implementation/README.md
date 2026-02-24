# Implementation Workflow

These templates pick up after `.agentic/planning/06_create_product_backlog.md`.

If present, the agent should apply your `.agentic/.agentic_profile.md` preferences during implementation.

They are designed for an incremental delivery loop driven by `.agentic/artifacts/product_backlog.md`, with tasks, tests, and commit boundaries made explicit.

If you adopt BDD, the executable specification (Gherkin) for the selected backlog item is written during feature planning and made runnable/green during execution.

## Steps

Lean loop (default):

1. `.agentic/implementation/01_pick_feature.md` - Pick the right next feature/story
2. `.agentic/implementation/02_plan_feature.md` - Create slices + task list (single plan file)
3. `.agentic/implementation/04_execute_plan.md` - Implement incrementally; run automation; hand off for user validation

Optional steps (use when needed):

- `.agentic/implementation/03_review_plan.md` - Extra plan clarification when risk/ambiguity is high
- `.agentic/implementation/05_run_quality_gate.md` - Dedicated automation run/fix pass
- `.agentic/implementation/06_validate_with_user.md` - Dedicated user validation + issue capture pass
- `.agentic/implementation/07_triage_backlog.md` - Triage + reprioritize the backlog (incl. inbox cleanup)

## Shared Rules

- The agent keeps `.agentic/artifacts/open_questions.md` and `.agentic/artifacts/decision_log.md` up to date.
- The agent keeps `.agentic/artifacts/product_backlog.md` up to date (capture new ideas in `Inbox (untriaged)` and move shipped items to `In product (shipped)`).
- If requirements change during implementation, update the relevant artifacts and add a decision log row.
- Planning includes a short functional elicitation gate before task decomposition (see `.agentic/implementation/02_plan_feature.md`).
- When present, treat the plan's `## Executable Specification (Gherkin)` as the feature-level acceptance contract.
