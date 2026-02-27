# Feature Plan (Slices + Tasks)

## Role
See `@.agentic/shared/roles/software_engineer.md`.

## Objective
Produce one plan that includes (1) incremental chunks and (2) a task list (incl. tests + automation).

Lock functional requirements in plain language before decomposing into tasks.

## Operating Rules
- Prefer user-facing language in questions.
- Avoid exposing technical decisions to the user unless unavoidable.
- If you must ask about a technical choice, translate it into a user-visible tradeoff.

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/output_boundary.md` (Artifact: single `md` fenced block).

## Required Inputs
- `.agentic/artifacts/product_requirements.md`
- `.agentic/artifacts/decision_log.md`
- `.agentic/artifacts/ux_design_guide.md` (if applicable)
- `.agentic/artifacts/technical_design.md`
- `.agentic/artifacts/product_backlog.md`
- `.agentic/artifacts/open_questions.md`

## Starting Point (Mandatory)
Do not require exhaustive design.

- Draft slices and tasks directly from the artifacts.
- Ask only what is needed to avoid wrong assumptions.
- Aim for 2-6 chunks; each chunk independently testable.
- When you select a story from the backlog to implement, write an executable specification in Gherkin for that story.
  - See `@.agentic/shared/skills/implementation/bdd_gherkin.md`.
  - Target: 3-7 scenarios for the MVI.
  - Scenarios must be user-observable and testable.
  - Include at least:
    - One happy-path outcome
    - One "must never happen"
    - One key edge-case behavior
    - One integration/dependency failure or degraded behavior when applicable

Embedded overlap gates (keep lightweight; `N/A` is allowed when truly not applicable):
- Observability: See `@.agentic/shared/skills/implementation/observability_minimum.md`.
- Testing tiers: See `@.agentic/shared/skills/implementation/testing_tiers.md`.
- Data/migrations: See `@.agentic/shared/skills/implementation/data_migrations.md`.
- Cleanup gate: See `@.agentic/shared/skills/implementation/cleanup_gate.md`.
- Rollout/verify (if shipping): See `@.agentic/shared/skills/implementation/rollout_verify.md`.

Backlog hygiene (during planning):
- If unrelated "later" ideas come up while discussing the feature, capture them as short items under `Inbox (untriaged)` in `.agentic/artifacts/product_backlog.md`.
- Do not expand the current feature's scope unless the user explicitly changes what "done" means (the executable specification).

## Functional Elicitation Gate (Mandatory)
Before you draft chunks/tasks, ensure the plan includes a crisp functional snapshot of the story.

1. Read the backlog item being implemented and scan the PRD for relevant requirements.
2. Check `.agentic/artifacts/open_questions.md` and incorporate any resolved answers.
3. If functional requirements are missing or ambiguous, ask a short question batch using:
   - `@.agentic/shared/skills/interaction/questions_format.md`
   - `@.agentic/shared/skills/implementation/functional_elicitation.md` (question order + "good enough to start" checklist)

Do not proceed to planning tasks until you can write the `## Functional Snapshot` section (below) in plain language.

Do not proceed to task decomposition until you can write the `## Executable Specification (Gherkin)` section (below) with unambiguous scenarios.

## Open Questions Gate (Mandatory)
See `@.agentic/shared/skills/gates/open_questions_gate.md` (Blockers: any `[Blocking]` item affecting this feature).

## Output Artifact
Write:
`.agentic/artifacts/tasks/plan-<feature_slug>.md`

## Output Format (Recommended)
Use this structure (adjust as needed). Prefer clarity over ceremony.

```md
# Plan: <Feature Name>

## Metadata
- Date: YYYY-MM-DD
- Backlog item: <epic/story name>
- Feature slug: <feature_slug>
- Related:
  - PRD: `.agentic/artifacts/product_requirements.md`
  - Technical design: `.agentic/artifacts/technical_design.md`
  - Decision log: `.agentic/artifacts/decision_log.md`

## Context
- Intended outcome: <short>

## Functional Snapshot
- Problem: <1-2 sentences>
- Target user: <who + context>
- Success criteria (observable):
  - <outcome>
- Primary user flow:
  1. <step>
  2. <step>
- Alternate flows (optional):
  - <alt flow>
- Must never happen:
  - <unacceptable outcome>
- Key edge cases:
  - <edge case> -> <expected behavior>
- Business rules:
  - <rule>
- Integrations (if any):
  - <system> - <what data moves / what the user expects>
  - Failure behavior: <what happens when the dependency is down>
- Non-functional requirements (user/business expectations):
  - Privacy/Security: <expectation>
  - Performance: <expectation>
  - Reliability: <expectation>
- Minimal viable increment (MVI): <smallest valuable version>
- Deferred:
  - <explicitly not in this feature>

## Executable Specification (Gherkin)

```gherkin
Feature: <short capability name>
  <1-2 sentence narrative of value>

  Scenario: <happy path>
    Given <precondition>
    When <action>
    Then <observable outcome>

  Scenario: <must never happen>
    Given <precondition>
    When <action>
    Then <unacceptable outcome is prevented and user sees expected behavior>

  Scenario: <key edge case>
    Given <precondition>
    When <action>
    Then <expected behavior>
```

## Baseline Gate (Automatic)
- Start from a clean, green trunk (`main`). If trunk is not green, stop and fix/triage first.
- Sync latest `main` before branching.

## Architecture Fit (This Feature)
- Touch points: <key components/boundaries this story affects>
- Compatibility notes: <what must remain backward-compatible and why>

## Observability (Minimum Viable)
- Applicability: Required | N/A (Reason: <one line>)
- Failure modes (3-6):
  - <failure mode> -> <expected degraded behavior>
- Logs (structured): <what events + key fields; confirm no sensitive data>
- Signals/metrics: <1-3 key signals to watch>

## Testing Strategy (Tier 0/1/2)
- Tier 0 (required): <what will be covered by unit/contract tests>
- Tier 1 (if applicable): <what needs deterministic integration testing>
- Tier 2 (if applicable): <what requires sandbox/third-party validation>

## Data & Migrations (If Applicable)
- Applicability: N/A | Schema only | Backfill | Expand/contract
- Up migration: <yes + approach>
- Down migration: <yes/no + why>
- Backfill plan (if any): <idempotent/restartable notes>
- Rollback considerations: <what happens if deploy/migration is reverted>

## Rollout & Verify (If Applicable)
- Applicability: Required | N/A (Reason: <one line>)
- Strategy: Feature flag | Canary | Staged | All-at-once
- Verify (smoke path): <2-6 steps>
- Signals to watch: <1-3>
- Optional: risk assessment artifact: `.agentic/operations/assess_production_risk.md`

## Cleanup Before Merge
- Remove: <temporary flags/debug logs/spike code/transitional scaffolding>
- If anything temporary remains: <decision log row + follow-up backlog item>

## Definition of Done (This Feature)
- `## Executable Specification (Gherkin)` is runnable and green (when present)
- Tier 0 is green; Tier 1 is green when applicable
- Observability requirements implemented (or explicitly `N/A`)
- Cleanup gate satisfied
- Backlog updated (move shipped item to `In product (shipped)` when accepted)

## Chunks
- <chunk name> (optional: `CH-001: <chunk name>`)
  - User value: <short>
  - Scope: <short>
  - Ship criteria: <short, testable>
  - Rollout notes: <flags/migrations/backfill or ->

## Relevant Files (Expected)
- `<path>` - <why>

## Notes
- Include unit/integration tests where appropriate.
- Include any migrations, backfills, or feature flags explicitly.
- Prefer small, reviewable commits that map to chunks.
- Write tasks so execution can be "commit-per-task": each leaf checkbox should be completable in a single commit, and execution will check it off in the same commit as the change.
- Each chunk should (a) deliver user value, (b) be testable, and (c) reduce risk.
- Plan only the next chunk in full detail; keep later chunks lighter.
- The executable specification is the feature-level acceptance contract; implementation should make it runnable (BDD suite) and green.

## Assumptions (User-Facing)
- <assumption made to proceed>

## Validation Script (Draft)
1. <step>
2. <step>
3. <step>

## Tasks
- [ ] T-001 Create and checkout a new branch (e.g. `feature/<feature_slug>`)

- [ ] Implement: <chunk name>
  - [ ] T-010 <leaf task that can be finished in one commit>
  - [ ] T-011 <leaf task that can be finished in one commit>
  - [ ] T-012 Tests: <what to add>

- [ ] Quality gate
  - [ ] T-900 Run formatters
  - [ ] T-901 Run linters
  - [ ] T-902 Run tests

## Open Questions
- <any non-blocking questions to capture or ->
```

Then ask:

> "If anything feels ambiguous or risky, tag **@.agentic/implementation/03_review_plan.md**. Otherwise tag **@.agentic/implementation/04_execute_plan.md** to start implementation."
