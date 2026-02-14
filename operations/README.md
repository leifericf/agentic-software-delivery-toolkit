# Operations Templates

Free-standing templates for post-development and production work.

These are not sequential steps. Pick the template you need.

## How To Use

- Tag one of the files below in your agent chat (or copy/paste its contents).
- If you have a `project_slug`, artifacts are written under: `artifacts/<project_slug>/operations/`.
- If you do not have a `project_slug`, the template will ask for one.

## Templates

- `operations/triage_logs.md` - turn noisy logs/alerts into a concrete next action list
- `operations/assess_production_risk.md` - pre-deploy / pre-rollout risk assessment with go/no-go criteria
- `operations/review_incident.md` - incident review (blameless retro) with action items
- `operations/analyze_root_cause.md` - root cause analysis with preventative controls

## Artifact Naming (Recommended)

To avoid collisions and keep things sortable, prefix artifacts with a date:

- `YYYY-MM-DD_log_triage-<issue_slug>.md`
- `YYYY-MM-DD_production_risk_assessment-<change_slug>.md`
- `YYYY-MM-DD_incident_review-<incident_slug>.md`
- `YYYY-MM-DD_root_cause_analysis-<incident_slug>.md`

Slug rules (recommended):
- lowercase snake_case
- letters, numbers, underscores only
