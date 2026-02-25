# Skill: Data changes and migrations

## Purpose
Plan and execute schema/data changes safely, with minimal production risk.

## Applicability
If the feature changes schema, stored data shape, or requires backfill, this skill applies. Otherwise, mark the plan section as `N/A`.

## Planning Checklist (Keep Short)
- Migration type: schema only | backfill | expand/contract | other
- Up migration: required
- Down migration: preferred when safe and feasible (if not, state why)
- Expand/contract (when old and new code may run concurrently):
  - Expand first (add new columns/tables/fields)
  - Ship compatible code
  - Contract later (remove old columns/paths)
- Backfill plan (if needed):
  - Online vs offline
  - Idempotency and restartability
  - Rollback behavior if partially applied
- Rollback plan: what we do if migration fails or deploy is reverted

## Execution Expectations
- Implement migrations in the repo's established mechanism.
- Keep changes reversible where possible.
- Include tests that cover the new data behavior (Tier 0 and Tier 1 when applicable).
