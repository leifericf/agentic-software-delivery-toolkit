# Execute Plan

## Role
See `@.agentic/shared/roles/software_engineer.md`.

## Objective
Execute the task plan one step at a time on a new local git feature branch, committing each logically separated chunk.

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/output_boundary.md`.
Override: no new artifacts; update repo files directly. Keep `.agentic/artifacts/product_backlog.md` up to date as you go. When done and automation is green, you may output a short validation script (2-6 steps).

## Required Inputs
- `.agentic/artifacts/tasks/plan-<feature_slug>.md`
- `.agentic/artifacts/open_questions.md`
- `.agentic/artifacts/decision_log.md`
- `.agentic/artifacts/technical_design.md`
- `.agentic/artifacts/product_backlog.md`
- Repo codebase (existing, or bootstrapped as part of the plan)

## Starting Point (Mandatory)
Do not implement everything at once.

- Work chunk-by-chunk.
- Keep changes small and verifiable.

## Automatic Preflight (Embedded)
Before you create a feature branch or start coding:
- Confirm you are starting from a clean, green trunk (`main`). If trunk is not green, stop and fix/triage first.
- Sync latest `main` locally.
- If the repo has a fast default check (tests/lint), run it once to confirm baseline.

## Open Questions Gate (Mandatory)
See `@.agentic/shared/skills/gates/open_questions_gate.md` (Blockers: any `[Blocking]` item affecting the chunk you are about to do).

## Git Rules
- Create a new local feature branch before making changes.
- Commit after each chunk (or meaningful sub-chunk), with a message that explains intent.
- Follow `@.agentic/shared/skills/git/git_commit.md`.
- Do not push unless explicitly asked.

## Task Hygiene
- As you complete tasks, check them off in `.agentic/artifacts/tasks/plan-<feature_slug>.md`.
- If the plan needs adjustment, update the task file and call it out to the user.

## Backlog Hygiene (Mandatory)

Keep the backlog a living document:

- Capture out-of-scope ideas immediately: if the user or you mention a future feature that is not required to finish the current plan, add it under `Inbox (untriaged)` in `.agentic/artifacts/product_backlog.md`.
- Do not expand the current feature's scope unless the user explicitly changes `## Executable Specification (Gherkin)` in the plan.
- When the feature is done and automation is green, move the implemented backlog item from `Now / Next` to `In product (shipped)`.
- If you discover net-new feature work that is truly out of scope for this plan, capture it in the backlog (`Inbox (untriaged)` or reprioritize into `Now / Next`/`Later`).
- Do not add bug reports to the backlog. Fix bugs relevant to the feature immediately unless the user explicitly suppresses the fix; if suppressed, capture it as a follow-up task in `.agentic/artifacts/tasks/plan-<feature_slug>.md`.

## Automation (Folded In)
Run the project's standard commands during/after execution (format, lint, test, and build if present).

Respect the plan's embedded gates:
- Observability: if the plan's `## Observability (Minimum Viable)` is not `N/A`, implement it as part of the relevant chunk (do not defer until the end).
- Testing tiers: follow the plan's `## Testing Strategy (Tier 0/1/2)` and keep Tier 0 green; run Tier 1 when applicable.
- Data/migrations: if the plan includes `## Data & Migrations`, implement safely and include rollback considerations.
- Cleanup: satisfy `@.agentic/shared/skills/implementation/cleanup_gate.md` before declaring done.

If the plan includes `## Executable Specification (Gherkin)`, make it executable:

- Materialize the Gherkin into `features/<feature_slug>.feature` (unless the repo already has an established convention).
- Use the most idiomatic BDD runner for the repo's language/test stack (or the existing one), and wire it into the repo's standard automation.
- Treat "automation is green" as including the BDD suite.

- Prefer running fast checks per chunk, then the full suite at the end.
- Fix issues with the smallest safe change.
- If automation reveals uncovered behavior, add tests.

## Automatic Reconcile & Cleanup (Embedded)
Before you say the feature is done:
- Check off completed tasks in `.agentic/artifacts/tasks/plan-<feature_slug>.md`.
- Ensure the plan's `## Cleanup Before Merge` is satisfied (remove temporary flags/debug logs/spike artifacts).
- If the plan's `## Rollout & Verify` is not `N/A` and the change is shipping, optionally tag `.agentic/operations/assess_production_risk.md` and follow its rollout/monitoring/rollback structure.
- Keep `.agentic/artifacts/product_backlog.md` consistent:
  - When accepted and automation is green, move the implemented backlog item to `In product (shipped)`.
  - Capture net-new ideas under `Inbox (untriaged)`.
- If decisions changed, append row(s) to `.agentic/artifacts/decision_log.md`.

Then ask:

> "Implementation done and automation is green. Please validate with the script above. What (if anything) didn't work? Include repro steps."

If the user wants a dedicated pass for automation or validation, they can optionally tag:

- **@.agentic/implementation/05_run_quality_gate.md**
- **@.agentic/implementation/06_validate_with_user.md**
