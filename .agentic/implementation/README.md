# Implementation Workflow

These templates pick up after `.agentic/planning/06_create_product_backlog.md`.

If present, the agent should apply your `.agentic/.agentic_profile.md` preferences during implementation.

They are designed for an incremental delivery loop driven by `.agentic/artifacts/product_backlog.md`, with tasks, tests, and commit boundaries made explicit.

If you adopt BDD, the executable specification (Gherkin) for the selected backlog item is written during feature planning and made runnable/green during execution.

## Steps

Default path (use this unless you have a reason not to):

1. `.agentic/implementation/01_pick_feature.md` - Pick the right next feature/story
2. `.agentic/implementation/02_plan_feature.md` - Create a single plan file (slices + tasks + embedded gates)
3. `.agentic/implementation/04_execute_plan.md` - Execute chunk-by-chunk (automation + validation folded in)

Embedded rigor lives inside `02` and `04` (no extra steps): baseline preflight, observability, testing tiers, data/migrations, cleanup gate, and rollout/verify when shipping.

Escape hatches (use only when needed):

- `.agentic/implementation/03_review_plan.md` - Extra plan clarification when risk/ambiguity is high
- `.agentic/implementation/05_run_quality_gate.md` - Dedicated automation run/fix pass (if you want a separate pass)
- `.agentic/implementation/06_validate_with_user.md` - Dedicated user validation + issue capture pass (if you want a separate pass)
- `.agentic/implementation/07_triage_backlog.md` - Triage + reprioritize the backlog (incl. inbox cleanup)

## Shared Rules

- The agent keeps `.agentic/artifacts/open_questions.md` and `.agentic/artifacts/decision_log.md` up to date.
- The agent keeps `.agentic/artifacts/product_backlog.md` up to date (capture new ideas in `Inbox (untriaged)` and move shipped items to `In product (shipped)`).
- If requirements change during implementation, update the relevant artifacts and add a decision log row.
- Planning includes a short functional elicitation gate before task decomposition (see `.agentic/implementation/02_plan_feature.md`).
- When present, treat the plan's `## Executable Specification (Gherkin)` as the feature-level acceptance contract.

## Maintainer Sanity Checks (When Updating Templates)
- `02_plan_feature.md` plan template includes baseline/observability/testing/data/cleanup/rollout sections with `N/A` exits.
- `04_execute_plan.md` enforces preflight + reconcile/cleanup before declaring done.
- Overlap skills exist under `.agentic/shared/skills/implementation/` and are referenced by roles/steps.
- Default path remains `01 -> 02 -> 04`; `05` and `06` stay optional escape hatches.
