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

## Flakiness Policy (Keep Practical)
- Prefer determinism; do not accept flaky tests on the default green path.
- For Tier 2 only: allow retry and quarantine, but do not block the fast loop.

## Time Budget
Target the default local/CI loop to stay under ~5 minutes:
- Run Tier 0 frequently (per chunk)
- Run Tier 1 when integration-affecting chunks land
- Run Tier 2 on demand or on a slower schedule
