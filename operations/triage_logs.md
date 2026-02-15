# Triage Logs

## Role
See `@shared/roles/software_engineer.md`.

## Objective
Turn production signals (logs, alerts, error reports) into a prioritized, testable hypothesis set and an action plan.

## Output Boundary (STRICT)
See `@shared/skills/gates/output_boundary.md` (Artifact: single `md` fenced block).

## Starting Point (Mandatory)
Do not ask the user to paste everything.

- Start with the smallest useful packet: one alert/error example + timeframe + environment.
- Prefer reversible mitigations first.

## Required Inputs
At least one of:
- A log excerpt (10-50 lines) OR an alert payload OR an error report screenshot/text
- Time window (start/end) and environment (prod/staging)

Optional (if available):
- Recent deploys/flags/config changes
- Dashboard links (metrics/traces)

## Project Slug (If Needed)
See `@shared/skills/planning/project_slug.md`.

## Input Gate (Default)
See `@shared/skills/gates/input_gate.md`.

## Open Questions (Optional)
If `artifacts/<project_slug>/00_open_questions.md` exists, scan `## Open` and do not re-ask answered questions.

If it does not exist, continue; capture unknowns in the triage artifact under `## Open Questions`.

## Question Style
Ask questions using the format in `@shared/skills/interaction/questions_format.md` (cap 3).

Prefer:
- Binary (to narrow scope fast)
- Choice (to pick the most likely branch)

## Output Artifact
Write:
`artifacts/<project_slug>/operations/YYYY-MM-DD_log_triage-<issue_slug>.md`

`<issue_slug>` rules: see `@shared/skills/planning/slug_rules.md`.

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Template:

```md
# Log Triage: <Issue Name>

## Metadata
- Date: YYYY-MM-DD
- Project Slug: <project_slug>
- Environment: Production | Staging | Dev | Other
- Time Window: <start> to <end> (timezone)
- Reported By: <system/person>
- Related:
  - Incident: <link or ->
  - Deploy/Change: <link or ->
  - Dashboard: <link or ->
  - Runbook: <link or ->

## Summary
- <1-5 bullets: what is happening + current impact + what you will do next>

## Symptoms
- <user-visible symptom>
- <operator-visible symptom>

## Impact Assessment
- User impact: None | Low | Medium | High
- Business impact: None | Low | Medium | High
- Blast radius: <who/what is affected>

## Observed Signals
- Logs:
  - <signal name> - <what it suggests>
- Metrics:
  - <signal name> - <what it suggests>
- Traces:
  - <signal name> - <what it suggests>

## Recent Changes
- <deploy/config/flag change> (Date/Time: <optional>)

## Hypotheses
| Hypothesis | Why plausible | How to test quickly | Status |
| --- | --- | --- | --- |
| <hypothesis> | <why> | <experiment> | Open |

## Experiments / Checks
- <experiment>
  - Expected: <expected outcome>
  - Actual: <actual outcome>
  - Result: Supported | Rejected | Inconclusive

## Findings
- <finding>

## Mitigations (Reversible First)
- <mitigation>
  - Risk: <risk>
  - Rollback: <how to undo>

## Next Actions (Prioritized)
1. <action>
2. <action>
3. <action>

## Open Questions
- <question>

## Data Request Packet
- Please provide: <specific thing>
- Format needed: <exact format>
- Where to find it: <link/path/system>
```
