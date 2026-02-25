# Skill: Rollout and post-deploy verification

## Purpose
Ensure features that ship to production have a minimal rollout and verification plan, without introducing a new mandatory workflow step.

## Applicability
If the feature will be deployed or rolled out to real users, this applies. Otherwise, mark the plan section as `N/A`.

## Planning Checklist (Keep Short)
- Rollout strategy: feature flag | canary | staged | all-at-once | other
- Guardrails: what triggers a pause/rollback
- Verification: the one "smoke" path to confirm post-deploy
- Signals to watch: 1-3 key signals (logs/metrics/alerts)

## Optional Risk Assessment
If the change has meaningful production risk, use:
- `.agentic/operations/assess_production_risk.md`
