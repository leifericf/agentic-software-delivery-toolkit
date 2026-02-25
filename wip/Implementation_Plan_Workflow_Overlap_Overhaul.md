# Implementation Plan: Workflow Overlap Overhaul (Planning <-> Implementation)

Date: 2026-02-25

## Goal
Fill the workflow gaps identified in `wip/` (observability, test tiering, migrations/data discipline, cleanup-before-merge, baseline/trunk hygiene, deploy/verify hooks) **without** adding manual workflow step files.

Constraints we are honoring:
- Only workflow steps the user triggers manually live as Markdown step files under `.agentic/{planning,implementation,operations,setup}/`.
- “Automatic” steps must be embedded into existing manual steps as gates/checklists.
- Avoid new durable artifacts and avoid overwhelming users; keep cognitive load light.
- Keep the default manual path for implementation: `01_pick_feature -> 02_plan_feature -> 04_execute_plan`.
- Keep `.agentic/implementation/05_run_quality_gate.md` and `.agentic/implementation/06_validate_with_user.md` but demote them in docs as escape hatches (Option A).

Non-goals:
- Introducing a new required manual step for merge/deploy.
- Creating new durable artifact files just for observability/testing/migrations.
- Adding new roles unless absolutely required (we currently believe they are not).

## Deliverables
1) Update existing manual step templates (embedded gates + plan sections):
   - `.agentic/implementation/02_plan_feature.md`
   - `.agentic/implementation/04_execute_plan.md`
   - `.agentic/implementation/README.md`
   - `.agentic/planning/05_create_technical_design.md`

2) Add a small set of internal skills modules (not manually triggered steps):
   - `.agentic/shared/skills/implementation/observability_minimum.md`
   - `.agentic/shared/skills/implementation/testing_tiers.md`
   - `.agentic/shared/skills/implementation/data_migrations.md`
   - `.agentic/shared/skills/implementation/cleanup_gate.md`
   - Optional (only if we decide it’s needed immediately): `.agentic/shared/skills/implementation/rollout_verify.md`

3) Keep durable artifacts unchanged in number; embed new rigor into the existing plan artifact:
   - `.agentic/artifacts/tasks/plan-<feature_slug>.md` gains a few short sections (written by the agent during the manual planning step).

## Step-by-Step Implementation Plan

### Step 0 — Establish Baseline (Repo Hygiene)
1. Confirm current state of templates (for reference while editing):
   - Verify current content of:
     - `.agentic/implementation/02_plan_feature.md`
     - `.agentic/implementation/04_execute_plan.md`
     - `.agentic/implementation/README.md`
     - `.agentic/planning/05_create_technical_design.md`
     - `.agentic/shared/skills/implementation/*`
2. Decide whether we will add the optional skill `rollout_verify.md` now or defer it.
   - Default: add it now, but keep it lightweight and explicitly “N/A” for most features.

Acceptance criteria:
- We are editing only templates and skills, not introducing new manual workflow step files.

### Step 1 — Add Internal Skill Modules (Implementation Helpers)
Create the following files under `.agentic/shared/skills/implementation/`.

1. `.agentic/shared/skills/implementation/observability_minimum.md`
   - Purpose: make Phase 4 (observability planning) consistently happen with minimal overhead.
   - Contents (keep short):
     - Applicability rule (when required vs when `N/A` is acceptable)
     - “Minimum viable observability” checklist:
       - boundary logs (structured), key fields, correlation id guidance, redaction guidance
       - at least one metric/signal for critical flows
       - explicit failure-mode list (3-6 bullets)
     - Output expectation: the plan includes a short observability section and the execution implements it.

2. `.agentic/shared/skills/implementation/testing_tiers.md`
   - Purpose: embed the `wip/` Tier 0/1/2 model into planning and execution.
   - Contents:
     - Tier definitions:
       - Tier 0: unit + deterministic fakes + contracts
       - Tier 1: deterministic integration (containers)
       - Tier 2: sandbox/third-party (retry + quarantine policy guidance)
     - Applicability rules (when Tier 1/2 is required)
     - “Main loop < 5 min” reminder and guidance for controlling flakiness.

3. `.agentic/shared/skills/implementation/data_migrations.md`
   - Purpose: make Phase 9 (schema/data handling) explicit when applicable.
   - Contents:
     - Applicability rule (`N/A` if no schema/data changes)
     - Up migration required; down migration preferred when possible
     - Expand/contract guidance (when changing schema used by live code)
     - Backfill plan guidance (online vs offline, idempotency)
     - Rollback considerations (what happens if migration fails)

4. `.agentic/shared/skills/implementation/cleanup_gate.md`
   - Purpose: enforce Phase 16 (cleanup) without a new manual step.
   - Contents:
     - “Must remove before done” list: debug logs, temporary flags, spike artifacts, dead code, transitional scaffolding
     - “Explicitly keep” rule: if we keep a flag or temp behavior, it must be recorded in decision log and/or backlog.

5. (Optional) `.agentic/shared/skills/implementation/rollout_verify.md`
   - Purpose: provide a minimal plan section and execution hook for Phase 18.
   - Contents:
     - Applicability rule (`N/A` if no production deployment/rollout in scope)
     - Rollout strategy options (flag/canary/staged/all-at-once)
     - Verify checklist: what to check post-deploy (signals, logs/metrics, smoke path)
     - Pointer to `.agentic/operations/assess_production_risk.md` as the heavier optional artifact.

Acceptance criteria:
- Skills are role-agnostic and short.
- Skills do not introduce new manual workflow step files.

### Step 2 — Upgrade `.agentic/implementation/02_plan_feature.md` (Embed Overlap Sections)
Modify `.agentic/implementation/02_plan_feature.md` to ensure the *single plan artifact* carries the missing `wip/` overlap outputs.

Changes:
1. Add references to the new internal skills (do not inline long prose):
   - `observability_minimum.md`
   - `testing_tiers.md`
   - `data_migrations.md`
   - `cleanup_gate.md`
   - `rollout_verify.md` (if added)

2. Extend the “Output Format (Recommended)” plan template for `.agentic/artifacts/tasks/plan-<feature_slug>.md` with these minimal sections (all must be skippable with explicit `N/A`):
   - `## Baseline Gate (Automatic)`
     - e.g., “Start from green trunk; if not green, stop and fix/triage first.”
   - `## Architecture Fit (This Feature)`
     - integration boundaries + compatibility notes specific to this story.
   - `## Observability (Minimum Viable)`
     - logs/metrics/failure modes; redaction note; allow `N/A`.
   - `## Testing Strategy (Tier 0/1/2)`
     - indicate required tiers for this feature.
   - `## Data & Migrations (If Applicable)`
     - migration/backfill/expand-contract/rollback notes; allow `N/A`.
   - `## Rollout & Verify (If Applicable)`
     - small checklist; allow `N/A`; point to ops risk assessment when deploying.
   - `## Cleanup Before Merge` (short checklist)
   - `## Definition of Done (This Feature)`
     - keep tiny: acceptance (gherkin), automation green (tiers), cleanup done, backlog moved to shipped.

3. Ensure the plan template remains readable:
   - Each embedded section is 3–6 bullets.
   - Default stance is: fill automatically; ask only if it would change behavior/acceptance.

4. Update planning rules:
   - Explicitly state that per-feature observability/testing/migration/rollout planning belongs in this plan (implementation planning), not in the global technical design.

Acceptance criteria:
- The plan artifact becomes the “single place” for per-feature overlap concerns.
- Nothing new is required from the user besides triggering the same manual step.

### Step 3 — Upgrade `.agentic/implementation/04_execute_plan.md` (Embedded Automatic Gates)
Modify `.agentic/implementation/04_execute_plan.md` to enforce the “feature transaction” behavior without creating new manual steps.

Changes:
1. Add a clear “Automatic Preflight” section (agent runs it):
   - Verify baseline is clean (main green / sync / fast checks).
   - Create branch (already required) only after baseline passes.

2. Make plan section enforcement explicit:
   - If plan has `Observability`, it must be implemented as part of the relevant chunk (not deferred).
   - If plan requires Tier 1/Tier 2 tests, ensure they are run at the appropriate time.
   - If plan has migrations/backfills, implement them with safety/rollback notes.

3. Add an “Automatic Reconcile & Cleanup” endgame checklist:
   - Check off tasks in the plan file.
   - Ensure cleanup gate is satisfied (no temp artifacts left).
   - Ensure backlog item moved to `In product (shipped)` when accepted.
   - Add decision log row(s) only if decisions changed.

4. Add deploy/verify hooks without adding steps:
   - If `Rollout & Verify` is not `N/A`, instruct to optionally tag `.agentic/operations/assess_production_risk.md`.
   - Keep it as guidance; do not force a new manual step.

Acceptance criteria:
- Execution becomes rigorous by default while remaining “one manual step”.
- “Done” includes cleanup + reconcile, not just “tests pass”.

### Step 4 — Update `.agentic/implementation/README.md` (Option A Demotion)
Modify `.agentic/implementation/README.md` to reduce cognitive load.

Changes:
1. Make the default manual path prominent: `01 -> 02 -> 04`.
2. Mark these as escape hatches (rarely needed):
   - `03_review_plan.md`
   - `05_run_quality_gate.md`
   - `06_validate_with_user.md`
   - `07_triage_backlog.md`
3. Explicitly state that the rigorous “automatic phases” happen inside `02` and `04`:
   - baseline gate, test tiers, observability minimum, migrations, cleanup gate, rollout/verify hook.

Acceptance criteria:
- A new user can follow the default path without feeling forced into extra steps.

### Step 5 — Update `.agentic/planning/05_create_technical_design.md` (Posture vs Per-Feature)
Modify `.agentic/planning/05_create_technical_design.md` to set conventions/posture while avoiding per-feature specifics.

Changes:
1. In `## Observability` and `## Testing Posture` sections, clarify:
   - This doc defines defaults and tool choices.
   - Feature-specific observability/testing tiers are planned in `.agentic/implementation/02_plan_feature.md`.
2. In `## Repository & Delivery Conventions`, add a brief note that:
   - The plan artifact will include per-feature gates (baseline/cleanup/rollout) as needed.

Acceptance criteria:
- Planning remains “pre-coding” and global; implementation planning remains feature-specific.

### Step 6 — Cross-Reference and Consistency Pass
1. Ensure new skills are referenced correctly using the repo convention: `See @.agentic/shared/skills/<path>.md`.
2. Ensure no manual step file instructs the user to trigger a non-existent step.
3. Ensure N/A rules exist so small features do not get burdened.
4. Ensure the “only manual steps are step files” constraint is respected.

Acceptance criteria:
- No new manual workflow steps introduced.
- Embedded gates cover the missing `wip/` phases.

### Step 7 — Verification (Template-Level)
1. Run a quick content scan:
   - Confirm `.agentic/shared/skills/implementation/` now includes the new skills.
   - Confirm `.agentic/implementation/02_plan_feature.md` plan template includes the new sections.
   - Confirm `.agentic/implementation/04_execute_plan.md` includes preflight + cleanup/reconcile guidance.
   - Confirm `.agentic/implementation/README.md` reflects Option A.

Acceptance criteria:
- Edits match agreed behavior and reduce user-facing complexity.

## Notes on Rigor Without Cognitive Load
Implementation rigor is achieved by:
- Embedding “must think about this” items as short plan sections with explicit `N/A` exits.
- Having the agent perform automatic gates in execution without introducing new manual steps.
- Using a few internal skills to keep templates short, consistent, and maintainable.
