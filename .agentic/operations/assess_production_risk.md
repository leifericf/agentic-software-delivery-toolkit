# Assess Production Risk

## Role
See `@.agentic/shared/roles/solution_architect.md`.

## Objective
Assess production risk for a proposed change and produce a concrete go/no-go decision framework (rollout, monitoring, rollback).

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/output_boundary.md` (Artifact: single `md` fenced block).

## Starting Point (Mandatory)
Start with a plain-language description of the change and the user-visible behavior it affects.

## Required Inputs
At least one of:
- PR/commit link or diff summary
- Release notes / change description
- Feature flag / config change description

Optional:
- Prior incidents related to this area
- Known SLOs and alert thresholds

## Input Gate (Default)
See `@.agentic/shared/skills/gates/input_gate.md`.

## Open Questions (Optional)
If `.agentic/artifacts/open_questions.md` exists, scan `## Open` and incorporate any answered items relevant to this change.

If it does not exist, continue; capture unknowns in the risk assessment under `## Open Questions`.

## Question Style
Ask questions using the format in `@.agentic/shared/skills/interaction/questions_format.md` (cap 3).

Prefer:
- Choice (select rollout strategy / blast radius)
- Binary (confirm non-negotiables)

## Output Artifact
Write:
`.agentic/artifacts/operations/YYYY-MM-DD_production_risk_assessment-<change_slug>.md`

`<change_slug>` rules: see `@.agentic/shared/skills/planning/slug_rules.md`.

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Template:

```md
# Production Risk Assessment: <Change Name>

## Metadata
- Date: YYYY-MM-DD
- Owner: <name or role>
- Change slug: <change_slug>
- Related:
  - PR/Diff: <link or ->
  - Release ticket: <link or ->
  - Runbook: <link or ->

## Change Summary
- User-visible behavior change: <what changes>
- Systems/components touched: <list>
- Data shape changes (if any): <what changes>

## Blast Radius
- Who/what can be affected: <users/tenants/regions>
- Worst-case impact: <what could go wrong>

## Dependencies
- External/internal dependencies: <list>
- Failure behavior expectations:
  - <dependency> down -> <expected behavior>

## Rollout Plan
- Strategy: All-at-once | Staged | Canary | Feature flag | Other
- Steps:
  1. <step>
  2. <step>
- Guardrails:
  - <guardrail>

## Monitoring Plan
- Key signals to watch:
  - <signal> - <threshold / what indicates trouble>
- Where to watch:
  - <dashboard/link>

## Rollback Plan
- Rollback trigger(s): <what causes rollback>
- Rollback steps:
  1. <step>
  2. <step>
- Expected recovery time: <estimate>

## Risk Register
| Risk | Likelihood | Impact | Mitigation | Detection | Owner |
| --- | --- | --- | --- | --- | --- |
| <risk> | Low/Medium/High | Low/Medium/High | <mitigation> | <how we detect> | <role> |

## Go / No-Go Criteria
- Go if:
  - <criterion>
- No-go / pause if:
  - <criterion>

## Open Questions
- <question>

## Decision
- Current stance: Go | Go with conditions | No-go (pending)
- Conditions (if any):
  - <condition>
```
