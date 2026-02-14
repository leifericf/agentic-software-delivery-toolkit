# Review Incident

## Role
See `@shared/roles/quality_engineer.md`.

## Objective
Produce a blameless incident review focused on learning and preventing recurrence.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Starting Point (Mandatory)
Do not demand a perfect timeline up front.

- Start with impact + detection + resolution.
- Fill in timeline as facts become available.

## Required Inputs
At least one of:
- Incident summary (even 3-7 bullets)
- Incident ticket/chat transcript link

Optional:
- Timeline notes
- Metrics/graphs

## Project Slug (If Needed)
If `project_slug` is not known, ask for a project name and propose 3-5 slug options.

Slug rules (STRICT):
- lowercase snake_case
- letters, numbers, underscores only
- no spaces

## Input Gate (Default)
See `@shared/input_gate.md`.

## Open Questions (Optional)
If `artifacts/<project_slug>/00_open_questions.md` exists, scan `## Open` and incorporate any resolved answers relevant to this incident.

If it does not exist, continue; capture unknowns in the incident review under `## Open Questions`.

## Question Style
Ask questions using the format in `@shared/questions_format.md` (cap 3).

Prefer:
- Binary (facts: did X happen?)
- Choice (pick the primary contributing factor categories)

Avoid:
- Blame-oriented language

## Output Artifact
Write:
`artifacts/<project_slug>/operations/YYYY-MM-DD_incident_review-<incident_slug>.md`

`<incident_slug>` rules (recommended): lowercase snake_case.

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Template:

```md
# Incident Review: <Incident Name>

## Metadata
- Date: YYYY-MM-DD
- Project Slug: <project_slug>
- Incident slug: <incident_slug>
- Severity: Sev0 | Sev1 | Sev2 | Sev3 | Unknown
- Owner: <name or role>
- Related:
  - Incident ticket: <link or ->
  - Status page: <link or ->
  - Dashboard: <link or ->
  - Postmortem doc: <link or ->

## Summary
- <1-5 bullets: what happened, impact, and the most important follow-ups>

## Impact
- User impact: <what users experienced>
- Duration: <start> to <end> (timezone)
- Blast radius: <who/what was affected>
- Business impact: <if known>

## Detection
- How detected: <alert/user report/on-call observation>
- Detection gap (if any): <what should have caught it>

## Timeline (UTC recommended)
| Time | Event |
| --- | --- |
| <time> | <event> |

## Response
- What we did: <key steps>
- What worked well: <notes>
- What didn’t: <notes>

## Communication
- Internal comms: <what happened>
- External comms: <what happened>

## Contributing Factors (Blameless)
- Product: <factor or ->
- Technical: <factor or ->
- Data: <factor or ->
- Operational: <factor or ->
- Org/process: <factor or ->

## Action Items
| Action | Type | Owner | Due date | Status |
| --- | --- | --- | --- | --- |
| <action> | Prevent | <role> | YYYY-MM-DD | Open |

## Follow-Up Verification
- How we will verify fixes worked: <tests/alerts/drills>

## Open Questions
- <question>
```
