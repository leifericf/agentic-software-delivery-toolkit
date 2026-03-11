# Skill: Testing tiers (Tier 0/1/2)

## Purpose
Keep the main development loop fast and deterministic while still validating real integrations when needed.

## Tiers
- Tier 0 (Fast): unit tests + deterministic fakes + contract tests
- Tier 1 (Deterministic integration): containerized or local deterministic dependencies (DB/queue/cache)
- Tier 2 (Sandbox / third-party): external dependencies; use retry + quarantine policy for flakiness

## Applicability (Rules of Thumb)
- Tier 0 is required for all user-visible behavior changes.
- Tier 1 is required when you touch persistence, migrations, background jobs, or critical integration boundaries.
- Tier 2 is required only when correctness depends on third-party behavior that cannot be simulated deterministically.

## E2E / Journey Tests (Cross-Tier)
When the product has multi-step user flows and an E2E/journey suite exists (or is feasible):
- Recommend journey tests alongside unit and BDD acceptance tests for user-visible changes.
- Use journey tests to validate cross-page flow, authentication boundaries, and end-to-end outcomes.
- Treat E2E failures as release-blocking for covered flows.
- When functional changes alter behavior covered by existing E2E tests, update those tests in the same feature work.

## Manual UAT Scripts (Release Safety)
When the team uses manual user testing/UAT:
- Maintain a versioned manual scenario source artifact in-repo (for example `docs/qa/manual-test-scenarios.json`) plus generated validation outputs if your project uses them.
- For user-visible behavior changes, update affected scenarios in the same feature work.
- For net-new functionality, add at least one new scenario.
- For high-risk flows (auth, payments, irreversible actions), include at least one happy path and one degraded/safety path.
- Keep scripts concrete: preconditions, steps, expected outcomes, and evidence capture fields.
- Do not treat manual scenarios as a replacement for automated tests.

## Flakiness Policy (Keep Practical)
- Prefer determinism; do not accept flaky tests on the default green path.
- For Tier 2 only: allow retry and quarantine, but do not block the fast loop.

## Time Budget
Target the default local/CI loop to stay under ~5 minutes:
- Run Tier 0 frequently (per chunk)
- Run Tier 1 when integration-affecting chunks land
- Run Tier 2 on demand or on a slower schedule
