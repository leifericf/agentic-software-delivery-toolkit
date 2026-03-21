# Prompt: Find Bugs

## Role
Primary: `@.agentic/shared/roles/quality_engineer.md`
Secondary: `@.agentic/shared/roles/software_engineer.md`

## Objective
- Look for bugs.
- Categorize each bug.
- Assign severity, priority, and fix complexity consistently.
- Create and maintain a durable bug list artifact separate from the product backlog.
- Keep the bug list as a living document as new bugs are discovered.
- Keep bug detection strictly separate from UX/UI and security issue evaluation.

## Hard Rules
- Do not add bugs to `.agentic/artifacts/product_backlog.md`. Bugs live in `.agentic/artifacts/bug_list.md`.
- Do not fix bugs in this prompt. This prompt is for discovery + documentation only.
- Prefer evidence-based entries (repro steps, failing tests, logs, screenshots, stack traces). If evidence is missing, explicitly record what is needed.
- Follow repository-level policy (for example `AGENTS.md`) and relevant `@.agentic/` policies when choosing checks and phrasing.
- Do not log UX/UI, visual polish, or accessibility findings in `.agentic/artifacts/bug_list.md`; route those to `@.agentic/prompts/find_ux_ui_issues.md` and `.agentic/artifacts/ux_ui_issue_list.md`.
- Do not log security/privacy vulnerabilities in `.agentic/artifacts/bug_list.md`; route those to `@.agentic/prompts/find_security_issues.md` and `.agentic/artifacts/security_issue_list.md`.

## Deterministic Discovery Protocol (Default)
- Freeze context: include reviewed commit SHA in recap.
- Run discovery in fixed phases:
  1) Baseline signals (compile/test/checks)
  2) Systematic code sweep
  3) Targeted search probes
  4) Gap-focused second pass (saturation)
- Use the same scan order each run:
  - config/runtime policy -> routing/entrypoints/middleware -> business logic/contexts -> UI/controllers/views/components -> asset/build logic.
- Saturation gate (mandatory): perform a second pass focused on high-risk areas and previously missed patterns; only stop when pass 2 yields no clear net-new bug candidates.

## Output Boundary
- Update (or create) exactly one artifact: `.agentic/artifacts/bug_list.md`.
- Optional: a brief chat recap (3-8 bullets) of what changed.

## Bug Definition (Working)
A bug is any defect that causes the product to deviate from intended behavior or quality standards, including:
- Functional correctness
- Data integrity/loss
- Availability/stability
- Reliability/consistency (flaky/racy)
- Performance
- Compatibility/localization

## Severity (Shared Scale)
Use exactly one value:

Blocker
- Core flow is unusable or unsafe; no practical workaround.

Very High
- Severe user/business impact; workaround is risky, costly, or unrealistic.

High
- Important flow is significantly degraded; workaround exists but is painful.

Normal
- Noticeable but limited impact; users can usually complete work with manageable friction.

Minor
- Small impact or edge-case issue with low risk.

### Severity Escalators
- Silent incorrectness (wrong-but-plausible)
- Irreversible effects
- Money movement or legal/compliance exposure

## Priority (Shared Scale)
Use exactly one value:

Very High
- Fix immediately; blocks delivery or causes major user harm.

High
- Fix in the next cycle; strong user/business impact.

Medium
- Schedule soon; meaningful but not urgent.

Low
- Safe to defer; limited impact.

Very Low
- Backlog polish/cleanup; defer until convenient.

## Fix Complexity (Shared Scale)
Use exactly one value:

Trivial
- Very small, low-risk change; usually a few lines.

Easy
- Straightforward, localized change with clear behavior.

Challenging
- Moderate complexity across multiple files or with nuanced behavior.

Difficult
- High complexity, broad impact, or significant risk/coordination.

Very Difficult
- System-level or high-uncertainty change requiring major design/refactor.

## Categories
Use exactly one primary category:
- Data Integrity/Loss
- Money/Billing/Legal
- Availability/Stability
- Core Functional Correctness
- Reliability/Consistency
- Performance
- Compatibility/Localization
- Observability/Operator Experience

## Procedure (Discovery Loop)
1. Ensure `.agentic/artifacts/bug_list.md` exists. If missing, create it from the template below.
2. Collect bug signals (prefer non-mutating checks first). Use checks that exist in this repo; examples:
   - format checks
   - lint/static analysis
   - compilation/build
   - unit/integration tests
3. Review code (mandatory): do a repo-wide review pass in addition to automation.
   - Scope: application code, configuration that affects runtime behavior, and user-facing surfaces.
   - Method: combine systematic skimming + targeted searches.
     - Systematic: start with entrypoints (routing/controllers/handlers/CLI commands), then data access, then integrations, then user-facing UI.
     - Targeted searches: look for TODO/FIXME, exceptions/panics, error swallowing, missing timeouts, retry loops, non-idempotent side effects, transaction boundaries, authorization checks, and external HTTP calls.
   - Goal: surface evidence-based defects, not style nits; prefer bugs with concrete repro/evidence or a clear, testable hypothesis.
4. Run pass-2 saturation (mandatory):
    - Re-scan highest-risk modules (auth/session, checkout/order flows, external integrations, background jobs, data writes, parsing boundaries).
    - Re-check prior open bugs to find adjacent variants/regressions.
    - If pass 2 finds net-new issues, include them and mark that saturation produced net-new findings in recap.
5. For each bug found:
   - Duplicate check (mandatory): before adding, search the bug list for a similar `summary`, same `area`, and/or matching key terms in `repro`/`notes`. If it already exists, update the existing row instead of adding a new one.
   - Add a new entry (or update an existing one).
   - Assign Category, Severity, Priority, and Fix Complexity.
   - Keep the bug line terse; put the most useful details in `repro` and `notes`.
   - If evidence is missing, set `notes` to a concrete data request.
6. Keep it living:
   - Deduplicate similar reports.
   - Tighten repro steps as you learn more.
   - When a bug is later fixed, it must be removed from `.agentic/artifacts/bug_list.md` in the same commit as the fix (see `@.agentic/prompts/fix_issues_by_type.md`).

## Required Recap (when chat recap is provided)
Include:
- commit SHA reviewed
- baseline checks run
- scope covered (major folders/surfaces)
- whether pass-2 saturation found net-new bug issues
- count of rows added vs updated

## Artifact Template: `.agentic/artifacts/bug_list.md`
If the file does not exist, create it with exactly this table header:

```md
| severity | priority | fix_complexity | category | area | summary | repro | notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
```

## One Row Per Bug (Markdown Table)
Each open bug is one table row with:
- `severity`: `Blocker|Very High|High|Normal|Minor`
- `priority`: `Very High|High|Medium|Low|Very Low`
- `fix_complexity`: `Trivial|Easy|Challenging|Difficult|Very Difficult`
- `category`: one of the Categories listed above
- `area`: short subsystem/page/module hint
- `summary`: short human-readable title
- `repro`: shortest useful repro (keep it compact)
- `notes`: evidence links, missing data request, or key context

Ordering rule in the file:
- Keep rows sorted by `severity` then `priority` using this order:
  - Severity: `Blocker -> Very High -> High -> Normal -> Minor`
  - Priority: `Very High -> High -> Medium -> Low -> Very Low`
