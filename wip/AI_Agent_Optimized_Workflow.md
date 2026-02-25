# AI-Agent Optimized Feature Implementation Protocol

## Purpose

This document provides a direct instruction-style workflow for AI agents
operating in a trunk-based development environment.

The goal is to implement features safely, incrementally, and with
minimal entropy.

------------------------------------------------------------------------

# Core Operating Principles

-   Work in small vertical slices.
-   Keep trunk releasable at all times.
-   Prefer deterministic test doubles over mocking frameworks.
-   Do not introduce architectural complexity unless justified.
-   Remove all temporary artifacts before merge.
-   Observability is mandatory for critical flows.

------------------------------------------------------------------------

# Step-by-Step Execution Protocol

## 1. Select Feature

-   Pull highest-priority backlog item.
-   Confirm scope and value hypothesis.

OUTPUT: Confirmed feature scope.

------------------------------------------------------------------------

## 2. Clarify Requirements

-   Convert feature into BDD-style scenarios.
-   Ensure acceptance criteria are explicit and testable.

OUTPUT: Executable acceptance criteria.

------------------------------------------------------------------------

## 3. Architecture & Compatibility Check

-   Evaluate architectural impact.
-   Minimize structural changes.
-   Decide on backward compatibility.
-   Identify integration boundaries.

OUTPUT: Architecture decision + compatibility plan.

------------------------------------------------------------------------

## 4. Observability Planning

-   Identify failure modes.
-   Define required logs (structured).
-   Define metrics (latency, error rate if relevant).
-   Ensure no sensitive data is logged.

OUTPUT: Observability requirements added to implementation plan.

------------------------------------------------------------------------

## 5. Decompose & Plan

-   Identify conceptual components.
-   Map dependencies.
-   Define vertical slices.
-   Include migrations if required.
-   Define feature flag strategy if needed.

OUTPUT: Ordered implementation slices.

------------------------------------------------------------------------

## 6. Testing Structure

Implement three-tier testing:

Tier 0: - Unit tests - Deterministic fakes - Contract tests

Tier 1: - Deterministic integration tests (containers)

Tier 2: - Sandbox/third-party tests (retry + quarantine)

Ensure main loop \< 5 minutes.

------------------------------------------------------------------------

## 7. Implement via TDD

-   Write failing tests first.
-   Implement incrementally.
-   Add logging at boundaries.
-   Add metrics for integration points.
-   Keep Tier 0 + Tier 1 green at all times.

OUTPUT: Passing deterministic tests.

------------------------------------------------------------------------

## 8. Integration & Real Data Wiring

-   Replace fakes with real persistence/integrations.
-   Implement retries, timeouts, idempotency where required.

OUTPUT: Fully functional feature.

------------------------------------------------------------------------

## 9. Validate at User Level

-   Dogfood feature.
-   Validate UX.
-   Fix discovered defects.

OUTPUT: User-level validated feature.

------------------------------------------------------------------------

## 10. Review & Debt Capture

-   Run AI review.
-   Perform human review checklist.
-   Identify trade-offs.
-   Add new backlog items if necessary.

OUTPUT: Clean, reviewed implementation.

------------------------------------------------------------------------

## 11. Documentation & State Sync

-   Move feature to Done.
-   Update changelog if applicable.
-   Update minimal README if needed.

OUTPUT: Organizational alignment.

------------------------------------------------------------------------

## 12. Cleanup

-   Remove debug logs.
-   Remove spike code.
-   Remove temporary flags.
-   Remove transitional artifacts.
-   Verify `.gitignore`.

OUTPUT: Simplified system.

------------------------------------------------------------------------

## 13. Merge to Trunk

-   Ensure Tier 0 + Tier 1 tests green.
-   Merge small PR.
-   Delete feature branch.

OUTPUT: Clean trunk state.

------------------------------------------------------------------------

## 14. Deploy & Verify

-   Deploy (continuous or flagged).
-   Verify logs and metrics.
-   Confirm no regressions.

OUTPUT: Operational feature.

------------------------------------------------------------------------

End of AI-Agent Protocol
