# User Validation

## Role
See `@shared/roles/quality_engineer.md`.

## Objective
Ask the user to validate the feature from a user's perspective and fix any issues found.

This step is optional if validation already happened during `implementation/04_execute_plan.md` or `implementation/05_run_quality_gate.md`.

## Output Boundary (STRICT)
See `@shared/skills/gates/output_boundary.md`.
Override: no artifacts unless needed to update the task plan or backlog. Ensure the backlog reflects what shipped.

## Required Inputs
- Implemented feature branch
- `artifacts/<project_slug>/tasks/plan-<feature_slug>.md`
- `artifacts/<project_slug>/product_backlog.md`

## Instructions
1. Give the user a short script for how to test (2-6 steps) based on what was implemented.
2. Ask them to try it end-to-end.
3. When they report issues:
   - Clarify reproduction steps.
   - Fix issues relevant to the implemented feature immediately.
   - If an issue appears unrelated to the feature you just implemented, do not switch scope silently; ask the user whether to address it now or defer it.
   - Do not add bug reports to the backlog.
   - If the user explicitly suppresses a fix for now, capture it as a follow-up task in `artifacts/<project_slug>/tasks/plan-<feature_slug>.md`.
4. When they report net-new feature ideas:
   - Capture them under `Inbox (untriaged)` in `artifacts/<project_slug>/product_backlog.md` unless the user explicitly wants them prioritized now.
5. If the feature is accepted as working end-to-end:
   - Ensure the implemented backlog item is moved into `In product (shipped)` in `artifacts/<project_slug>/product_backlog.md`.

Then ask:

> "Ready to start the next feature? Tag **@implementation/01_pick_feature.md**." 
