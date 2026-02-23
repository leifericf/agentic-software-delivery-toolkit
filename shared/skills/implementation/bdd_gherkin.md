# Skill: BDD + Gherkin executable specifications

## Purpose
Help the agent write and use an executable specification for a single selected backlog item.

This skill is intentionally implementation-agnostic: use the most idiomatic BDD runner for the repo's language and existing test stack.

## Core Rules
- Treat the Gherkin as the source of truth for feature-level acceptance.
- Prefer business language and user-observable outcomes. Avoid UI mechanics ("click", CSS selectors) unless the product is explicitly UI-only and no better abstraction exists.
- Keep scope thin: 3-7 scenarios is usually enough for the MVI (happy path + must-not-happen + key edge + integration failure/degraded behavior when applicable).
- Make scenarios deterministic:
  - Avoid time-dependent behavior unless time is the subject under test.
  - Avoid non-deterministic data (random ids, ordering) unless asserted properly.
  - Prefer concrete example values.

## Recommended Structure (Gherkin)
- One feature file per implemented backlog item: `features/<feature_slug>.feature`.
- Use `Feature:` and a short narrative.
- Use `Background:` only for truly shared preconditions.
- Use `Rule:` to group business rules when helpful.
- Use `Scenario Outline:` + `Examples:` for input permutations.
- Use `Data tables` for structured inputs/expected outputs.

## Tags (Optional)
- Use tags for targeting suites and work-in-progress behavior:
  - `@smoke` for the minimal end-to-end path.
  - `@slow` for expensive scenarios.
  - Avoid merging `@wip` scenarios that fail on `main`.

## "Good" Scenario Heuristics
- Each scenario describes one behavior, not a list.
- Given = preconditions/state; When = the action/event; Then = the observable result.
- Prefer asserting externally visible state (API response, persisted state, rendered user-facing text) over internal implementation details.
- Include at least one "must never happen" scenario (error, access control, invariant, data loss, double-charge, etc.).

## Making It Executable (Automation)
- If the repo already has a BDD runner, follow its conventions (file location, step definitions, hooks).
- Otherwise, choose the most idiomatic runner for the stack and wire it into the repo's standard automation so that "automation is green" includes the BDD suite.
- Keep step definitions reusable and intention-revealing; avoid one-off steps that bake in incidental details.
