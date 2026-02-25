# Skill: Cleanup gate (before done)

## Purpose
Prevent entropy: ensure temporary implementation artifacts do not ship by accident.

## Required Cleanup (Before Declaring "Done")
- Remove temporary flags or keep them intentionally with a follow-up plan
- Remove debug logs and one-off diagnostics
- Remove spike/prototype code that is not part of the final solution
- Remove dead code paths and transitional scaffolding that is no longer needed
- Remove or resolve TODOs introduced during the feature (or explicitly track them)

## If Something Temporary Must Remain
If you intentionally keep a flag, transitional behavior, or deferred cleanup:
- Record it as a conscious tradeoff (decision log) and/or a backlog follow-up item.
- Ensure the feature is still safe and understandable with the temporary element present.
