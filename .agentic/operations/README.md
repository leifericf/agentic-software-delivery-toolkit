# Operations Templates

Free-standing templates for post-development and production work.

These are not sequential steps. Pick the template you need.

## How To Use

- Tag one of the files below in your agent chat (or copy/paste its contents).
- Artifacts are written under: `.agentic/artifacts/operations/`.

## Templates

- `.agentic/operations/triage_logs.md` - turn noisy logs/alerts into a concrete next action list
- `.agentic/operations/assess_production_risk.md` - pre-deploy / pre-rollout risk assessment with go/no-go criteria
- `.agentic/operations/review_incident.md` - incident review (blameless retro) with action items
- `.agentic/operations/analyze_root_cause.md` - root cause analysis with preventative controls

## Artifact Naming (Recommended)

To avoid collisions and keep things sortable, prefix artifacts with a date:

- `YYYY-MM-DD_log_triage-<issue_slug>.md`
- `YYYY-MM-DD_production_risk_assessment-<change_slug>.md`
- `YYYY-MM-DD_incident_review-<incident_slug>.md`
- `YYYY-MM-DD_root_cause_analysis-<incident_slug>.md`

Slug rules (recommended):
See `@.agentic/shared/skills/planning/slug_rules.md`.
