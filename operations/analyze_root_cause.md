# Analyze Root Cause

## Role
See `@shared/roles/solution_architect.md`.

## Objective
Produce a rigorous root cause analysis that explains the causal chain and the controls that will prevent recurrence.

## Output Boundary (STRICT)
See `@shared/skills/gates/output_boundary.md` (Artifact: single `md` fenced block).

## Starting Point (Mandatory)
Anchor on one precise failure mode.

- Prefer a minimal, falsifiable problem statement.
- If multiple failures occurred, pick one primary incident and link the rest.

## Required Inputs
At least one of:
- A completed or partial incident review
- Repro notes (even rough)
- Links to logs/metrics/traces relevant to the failure

## Project Slug (If Needed)
See `@shared/skills/planning/project_slug.md`.

## Input Gate (Default)
See `@shared/skills/gates/input_gate.md`.

## Open Questions (Optional)
If `artifacts/<project_slug>/open_questions.md` exists, scan `## Open` and incorporate any resolved answers relevant to this RCA.

If it does not exist, continue; capture unknowns in the RCA under `## Open Questions`.

## Question Style
Ask questions using the format in `@shared/skills/interaction/questions_format.md` (cap 3).

Prefer:
- Binary (to validate each causal link)
- Choice (to select the most plausible causal chain branch)

## Output Artifact
Write:
`artifacts/<project_slug>/operations/YYYY-MM-DD_root_cause_analysis-<incident_slug>.md`

`<incident_slug>` rules: see `@shared/skills/planning/slug_rules.md`.

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Template:

```md
# Root Cause Analysis: <Incident Name>

## Metadata
- Date: YYYY-MM-DD
- Project Slug: <project_slug>
- Incident slug: <incident_slug>
- Owner: <name or role>
- Related:
  - Incident review: <link or ->
  - PR/Fix: <link or ->
  - Dashboard: <link or ->

## Problem Statement
<1-3 sentences describing the precise failure mode>

## Customer Impact
- What users experienced: <short>
- Duration: <start> to <end> (timezone)
- Blast radius: <who/what>

## Causal Chain
1. <event/cause>
2. <event/cause>
3. <event/cause>

## Five Whys (Optional)
1. Why did <problem> happen? <answer>
2. Why did <answer> happen? <answer>
3. Why did <answer> happen? <answer>
4. Why did <answer> happen? <answer>
5. Why did <answer> happen? <answer>

## Technical Deep Dive
- Component(s): <list>
- Data involved: <what data/shape>
- Failure mode details: <what exactly broke>
- Why this wasn’t caught earlier:
  - Tests: <gap>
  - Monitoring: <gap>
  - Process: <gap>

## Reproduction Notes
- Preconditions: <what must be true>
- Steps:
  1. <step>
  2. <step>
- Expected vs actual:
  - Expected: <expected>
  - Actual: <actual>

## Fix Summary
- Immediate fix: <what changed>
- Follow-up hardening: <what remains>

## Preventative Controls
| Control | Type | What it prevents | How we verify | Owner |
| --- | --- | --- | --- | --- |
| <control> | Test/Monitoring/Process/Architecture | <prevents> | <verification> | <role> |

## Residual Risk
- What could still go wrong: <short>
- Why acceptable: <short>

## Open Questions
- <question>
```
