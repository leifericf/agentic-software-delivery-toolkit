# Feature Plan (Slices + Tasks)

## Role
See `@shared/roles/software_engineer.md`.

## Objective
Produce one plan that includes (1) incremental chunks and (2) a task list (incl. tests + automation). This replaces the old two-step flow.

Lock functional requirements in plain language before decomposing into tasks.

## Operating Rules
- Prefer user-facing language in questions.
- Avoid exposing technical decisions to the user unless unavoidable.
- If you must ask about a technical choice, translate it into a user-visible tradeoff.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Required Inputs
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/00_decision_log.md`
- `artifacts/<project_slug>/04_ux_design_guide.md` (if applicable)
- `artifacts/<project_slug>/05_technical_design.md`
- `artifacts/<project_slug>/06_product_backlog.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Starting Point (Mandatory)
Do not require exhaustive design.

- Draft slices and tasks directly from the artifacts.
- Ask only what is needed to avoid wrong assumptions.
- Aim for 2-6 chunks; each chunk independently testable.
- When you select a story from the backlog to implement, define its Conditions of Done in this plan (3-7 short, testable bullets).
- Conditions of Done must be user-observable. Include at least:
  - One happy-path outcome
  - One "must never happen"
  - One edge-case behavior
  - One integration/dependency outcome when applicable

## Functional Elicitation Gate (Mandatory)
Before you draft chunks/tasks, ensure the plan includes a crisp functional snapshot of the story.

1. Read the backlog item being implemented and scan the PRD for relevant requirements.
2. Check `artifacts/<project_slug>/00_open_questions.md` and incorporate any resolved answers.
3. If functional requirements are missing or ambiguous, ask a short question batch using:
   - `@shared/questions_format.md`
   - `@shared/functional_elicitation.md` (question order + "good enough to start" checklist)

Do not proceed to planning tasks until you can write the `## Functional Snapshot` section (below) in plain language.

## Open Questions Gate (Mandatory)
See `@shared/open_questions_gate.md` (Blockers: any `[Blocking]` item affecting this feature).

## Output Artifact
Write:
`artifacts/<project_slug>/tasks/plan-<feature_slug>.md`

## Output Format (Recommended)
Use this structure (adjust as needed). Prefer clarity over ceremony.

```md
# Plan: <Feature Name>

## Metadata
- Date: YYYY-MM-DD
- Backlog item: <epic/story name>
- Feature slug: <feature_slug>
- Related:
  - PRD: `artifacts/<project_slug>/02_product_requirements.md`
  - Technical design: `artifacts/<project_slug>/05_technical_design.md`
  - Decision log: `artifacts/<project_slug>/00_decision_log.md`

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

## Conditions of Done
- <short, testable, user-observable condition>
- <short, testable, user-observable condition>
- <short, testable, user-observable condition>

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
- Each chunk should (a) deliver user value, (b) be testable, and (c) reduce risk.
- Plan only the next chunk in full detail; keep later chunks lighter.

## Assumptions (User-Facing)
- <assumption made to proceed>

## Validation Script (Draft)
1. <step>
2. <step>
3. <step>

## Tasks
- [ ] Create and checkout a new branch (e.g. `feature/<feature_slug>`)

- [ ] Implement: <chunk name>
  - [ ] <task>
  - [ ] <task>
  - [ ] Tests: <what to add>

- [ ] Quality gate
  - [ ] Run formatters
  - [ ] Run linters
  - [ ] Run tests

## Open Questions
- <any non-blocking questions to capture or ->
```

Then ask:

> "If anything feels ambiguous or risky, tag **@implementation/03_review_plan.md**. Otherwise tag **@implementation/04_execute_plan.md** to start implementation."
