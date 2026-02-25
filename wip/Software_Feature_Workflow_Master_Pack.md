# Software Feature Development Workflow -- Master Pack

Version: 1.0.0\
Generated: 2026-02-25\
Audience: Solo Developer + AI Agents + Trunk-Based Development

------------------------------------------------------------------------

# Table of Contents

1.  [Full Detailed Workflow](#full-detailed-workflow)
2.  [AI-Agent Optimized Protocol](#ai-agent-optimized-protocol)
3.  [Execution Checklist](#execution-checklist)
4.  [Usage Guidance & Cross-Reference
    Notes](#usage-guidance--cross-reference-notes)

------------------------------------------------------------------------

# Full Detailed Workflow

This section describes the complete lifecycle of a feature, including
architecture, testing, observability, cleanup, and deployment.

## Phase 0 -- Clean Baseline

Ensure trunk is green and stable before starting.

## Phase 1 -- Feature Selection

Select highest-priority backlog item and confirm scope.

## Phase 2 -- Requirement Clarification (BDD)

Convert to executable acceptance criteria.

## Phase 3 -- Architectural & Integration Fit

Minimize structural changes. Decide compatibility strategy.

## Phase 4 -- Observability Planning

Define logging, metrics, failure modes.

## Phase 5 -- Decomposition & Dependency Mapping

Identify components and dependencies.

## Phase 6 -- Implementation Planning

Define vertical slices, migrations, feature flags.

## Phase 7 -- Optional Spike

Time-box risky exploration. Remove or formalize results.

## Phase 8 -- Testing Strategy

Tier 0: Unit + deterministic fakes\
Tier 1: Container integration\
Tier 2: Sandbox / third-party (retry + quarantine)

## Phase 9 -- Schema & Data Handling

Up migrations required. Down migrations preferred if possible.

## Phase 10 -- TDD Implementation

Write failing tests first. Keep Tier 0 & 1 green.

## Phase 11 -- Real Data Wiring

Implement domain logic and persistence.

## Phase 12 -- User Validation

Dogfood and/or beta testing.

## Phase 13 -- Integration & Scale Testing

Validate real-world behavior and edge cases.

## Phase 14 -- Review & Debt Capture

AI review + human checklist. Capture trade-offs.

## Phase 15 -- Documentation & Backlog Sync

Move feature to Done. Update changelog and minimal docs.

## Phase 16 -- Cleanup & Simplification

Remove temporary flags, debug code, transitional artifacts.

## Phase 17 -- Merge to Trunk

Small PR. CI green. Delete branch.

## Phase 18 -- Deployment & Verification

Deploy, verify logs/metrics, confirm no regression.

------------------------------------------------------------------------

# AI-Agent Optimized Protocol

Use this section when instructing autonomous coding agents.

## Operating Rules

-   Small vertical slices
-   Trunk always releasable
-   Deterministic test doubles only
-   Observability required
-   Remove temporary artifacts before merge

## Execution Sequence

1.  Select feature\
2.  Clarify BDD specs\
3.  Architecture & compatibility check\
4.  Observability planning\
5.  Decompose & slice\
6.  Define test tiers\
7.  Implement via TDD\
8.  Wire real integrations\
9.  Validate UX\
10. Review & capture debt\
11. Sync documentation\
12. Cleanup\
13. Merge\
14. Deploy & verify

------------------------------------------------------------------------

# Execution Checklist

Use this section during active implementation.

## Selection

☐ Backlog item selected\
☐ Scope clarified

## Requirements

☐ BDD scenarios written

## Architecture

☐ Compatibility decision made\
☐ Integration boundaries identified

## Observability

☐ Logs defined\
☐ Metrics defined

## Planning

☐ Components mapped\
☐ Vertical slices defined\
☐ Migration plan created

## Testing

☐ Tier 0 tests written\
☐ Tier 1 integration tests written\
☐ Sandbox strategy defined

## Implementation

☐ Tests failing first\
☐ Code implemented\
☐ Logging added\
☐ Metrics added

## Validation

☐ User testing done\
☐ Integration tests executed

## Review

☐ AI review\
☐ Self review\
☐ Debt items captured

## Documentation

☐ Backlog updated\
☐ Changelog updated if applicable

## Cleanup

☐ Temporary artifacts removed\
☐ .gitignore verified

## Merge

☐ CI green\
☐ Feature branch deleted

## Deploy

☐ Deployment verified\
☐ Logs/metrics healthy

------------------------------------------------------------------------

# Usage Guidance & Cross-Reference Notes

-   Use **Full Workflow** for architectural planning and onboarding.
-   Use **AI-Agent Protocol** when instructing automation.
-   Use **Checklist** during execution.
-   Keep version header updated when modifying this document.
-   Treat each feature as a transaction: isolate → validate → reconcile
    → merge → reset.

------------------------------------------------------------------------

End of Master Pack
