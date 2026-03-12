# User Validation

## Role
See `@.agentic/shared/roles/quality_engineer.md`.

## Objective
Ask the user to validate the feature from a user's perspective and fix any issues found.

This step is optional if validation already happened during `.agentic/implementation/04_execute_plan.md`.

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/output_boundary.md`.
Override: no artifacts unless needed to update the task plan or backlog. Ensure the backlog reflects what shipped.

## Required Inputs
- Implemented feature branch
- `.agentic/artifacts/tasks/plan-<feature_slug>.md`
- `.agentic/artifacts/product_backlog.md`
- `.agentic/artifacts/bug_list.md`
- `.agentic/artifacts/ux_ui_issue_list.md`
- `.agentic/artifacts/security_issue_list.md`
- Manual scenario artifacts if present (e.g. `docs/qa/manual-test-scenarios.json` and `docs/qa/<gitsha>-manual-test-scenarios.xlsx`)

## Instructions
1. Give the user a concrete validation script for what changed:
   - Prefer referencing/updating the project's maintained manual scenario artifact when available.
   - If no maintained artifact exists yet, provide a focused 2-6 step script and note it should be promoted into a maintained artifact.
2. Ask them to try it end-to-end.
3. When they report issues:
   - Clarify reproduction steps.
   - Fix issues relevant to the implemented feature immediately.
   - If an issue appears unrelated to the feature you just implemented, do not switch scope silently; ask the user whether to address it now or defer it.
   - Do not add issue reports (bugs/UX/UI/security) to the backlog.
   - If deferred, log the issue in the correct living artifact:
     - Bugs -> `.agentic/artifacts/bug_list.md`
     - UX/UI -> `.agentic/artifacts/ux_ui_issue_list.md`
     - Security -> `.agentic/artifacts/security_issue_list.md`
   - If the user explicitly suppresses a fix for now, capture it as a follow-up task in `.agentic/artifacts/tasks/plan-<feature_slug>.md`.
4. When they report net-new feature ideas:
   - Capture them under `Inbox (untriaged)` in `.agentic/artifacts/product_backlog.md` unless the user explicitly wants them prioritized now.
5. If the feature is accepted as working end-to-end:
   - Ensure the implemented backlog item is moved into `In product (shipped)` in `.agentic/artifacts/product_backlog.md`.
6. Keep manual scenarios current:
   - If user-visible behavior changed, ensure the maintained scenario source artifact is updated in the same feature work.
   - If new functionality shipped, ensure at least one net-new scenario is added for it.

Then ask:

> "Ready to start the next feature? Tag **@.agentic/implementation/01_pick_feature.md**." 
