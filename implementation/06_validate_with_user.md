# User Validation

## Role
See `@shared/roles/product_oriented_qa_partner.md`.

## Objective
Ask the user to validate the feature from a user's perspective and capture issues for follow-up.

This step is optional if validation already happened during `implementation/04_execute_plan.md` or `implementation/05_run_quality_gate.md`.

## Output Boundary (STRICT)
See `@shared/output_boundary.md`.
Override: no artifacts unless user issues require updating backlog/tasks.

## Required Inputs
- Implemented feature branch
- `artifacts/<project_slug>/tasks/plan-<feature_slug>.md`
- `artifacts/<project_slug>/09_product_backlog.md`

## Instructions
1. Give the user a short script for how to test (2-6 steps) based on what was implemented.
2. Ask them to try it end-to-end.
3. When they report issues:
   - Clarify reproduction steps.
   - Capture them as backlog stories (or add follow-up tasks) with clear acceptance criteria.

Then ask:

> "Ready to start the next feature? Tag **@implementation/01_pick_feature.md**." 
