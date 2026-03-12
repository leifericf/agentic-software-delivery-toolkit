# Prompt: Fix Issues by Type

## Role
Primary: `@.agentic/shared/roles/software_engineer.md`
Guardrails: `@.agentic/shared/roles/quality_engineer.md`

## Objective
- Start by asking the user which issue type to fix: `bugs`, `ux_ui`, or `security`.
- Load the matching issue list artifact based on that choice.
- Fix one selected issue type at a time.
- Fix issues one at a time, in order of Severity then Priority.
- Create exactly one commit per issue fix.
- Update the selected issue list to remove the fixed issue in the SAME commit as the fix.

## Hard Rules
- Follow repository-level policy (for example `AGENTS.md`).
- Follow `@.agentic/shared/skills/git/git_commit.md` (Conventional Commits required; no amend unless explicitly requested; no secrets; no push unless explicitly asked).
- First action is mandatory: ask exactly one targeted question: `Do you want to fix bugs, UX/UI issues, or security issues?` Do not proceed until answered.
- Do not fix multiple issues in one commit. Do not mix unrelated refactors.
- Keep issue-type boundaries strict:
  - `bugs` -> only `.agentic/artifacts/bug_list.md`
  - `ux_ui` -> only `.agentic/artifacts/ux_ui_issue_list.md`
  - `security` -> only `.agentic/artifacts/security_issue_list.md`

## Issue Type Routing (Mandatory)
After the user answers, set:

- If `bugs`:
  - Artifact: `.agentic/artifacts/bug_list.md`
  - Prevention focus: automated regression coverage

- If `ux_ui`:
  - Artifact: `.agentic/artifacts/ux_ui_issue_list.md`
  - Prevention focus: UX guardrails (tests/checks/manual scenarios/design rules)

- If `security`:
  - Artifact: `.agentic/artifacts/security_issue_list.md`
  - Prevention focus: security controls, regression checks, and hardening guardrails

## Shared Severity and Priority Scales
Use the same values for bugs, UX/UI issues, and security issues.

Severity (highest to lowest):
- `Blocker`: core flow unusable/unsafe; no practical workaround.
- `Very High`: severe impact; workaround is risky/costly.
- `High`: major degradation; workaround exists but is painful.
- `Normal`: moderate impact; tasks still completable.
- `Minor`: small impact/polish issue.

Priority (highest to lowest):
- `Very High`: fix immediately.
- `High`: fix in the next cycle.
- `Medium`: schedule soon.
- `Low`: safe to defer.
- `Very Low`: backlog polish/cleanup.

Fix complexity:
- `Trivial`: very small, low-risk change.
- `Easy`: straightforward localized change.
- `Challenging`: moderate complexity across files/surfaces.
- `Difficult`: high complexity with broad impact/risk.
- `Very Difficult`: system-level or high-uncertainty effort.

## Issue List Artifacts
- Open bugs: `.agentic/artifacts/bug_list.md`
- Open UX/UI issues: `.agentic/artifacts/ux_ui_issue_list.md`
- Open security issues: `.agentic/artifacts/security_issue_list.md`
- Shared thread (align only where it is genuinely useful):
  - `severity | priority | fix_complexity | category | area | summary`
  - Use issue-type-specific columns for the rest.

## Output Boundary
- You may change repo code/tests and the selected issue-list artifact only.
- Chat output: concise progress notes (which issue, what changed, what to run).

## Preflight (Mandatory)
1. Ensure you are starting from a green trunk baseline (typically `main`). If trunk isn't green, stop and triage baseline first.
2. Work on a dedicated local branch unless already on an appropriate fix branch.

## Execution Loop (Repeat)
1. Read the selected issue artifact.
2. Pick the next issue by strict ordering:
   - Severity: `Blocker -> Very High -> High -> Normal -> Minor`
   - Priority: `Very High -> High -> Medium -> Low -> Very Low`
3. Validate the issue:
   - Bugs: confirm using listed `repro` and tighten it if needed.
   - UX/UI: confirm the issue signal from `reasoning` and observed interface behavior.
   - Security: confirm the issue from `threat_scenario` + `evidence` and tighten impact/exploitability details.
   - If evidence is weak, keep the row and update the issue with a concrete data request:
     - Bugs: add `NEEDS_REPRO:` in `notes`
     - UX/UI: add `NEEDS_VALIDATION:` in `reasoning`
     - Security: add `NEEDS_EVIDENCE:` in `evidence`
   - Stop for that issue if validation is insufficient (do not guess a fix).
4. Gap check (Mandatory, before the fix):
   - Bugs: determine why automation missed it (no test, wrong tier, missing assertion, flake, coverage gap).
   - UX/UI: determine why quality review missed it (missing heuristic pass, no scenario coverage, weak copy review, missing accessibility check, etc.).
   - Security: determine why security controls/review missed it (missing guard, missing test/scanner coverage, policy/config gap, threat-model gap, alerting blind spot, etc.).
   - Record the gap before removing the row:
     - Bugs: in `notes`
     - UX/UI: in `reasoning`
     - Security: in `evidence`
   - Decide the smallest prevention change that would have caught it earlier.
5. Implement with prevention:
   - Implement the fix.
   - Add/adjust the smallest useful prevention coverage in the same commit:
     - Bugs: regression tests when feasible (prefer red->green).
     - UX/UI: relevant UI tests/accessibility checks/manual scenario updates/design guardrails when feasible.
     - Security: relevant security tests/checks/policies/alerts and hardening docs when feasible.
   - Run the smallest relevant verification for the issue.
6. Update the selected issue list (Mandatory, same commit):
   - Remove the fixed issue row from the selected artifact.
7. Commit (Mandatory):
   - Stage only the fix + prevention updates + selected issue list update.
   - Create one Conventional Commit for this issue (typically `fix(<area>): <short description>`).
   - Do not include plan-internal identifiers in the commit message.

## Completion
- When all open issues for the selected type are resolved (or explicitly marked with data requests), run the repo's standard full check suite and fix failures.
- Report:
  - Issues fixed (by `area` + `summary`)
  - Commands to verify
  - Remaining `NEEDS_REPRO` / `NEEDS_VALIDATION` / `NEEDS_EVIDENCE` items + exact data needed

## Issue List Formats

### `.agentic/artifacts/bug_list.md`
Table header (must exist):

```md
| severity | priority | fix_complexity | category | area | summary | repro | notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
```

Allowed scale values:
- `severity`: `Blocker|Very High|High|Normal|Minor`
- `priority`: `Very High|High|Medium|Low|Very Low`
- `fix_complexity`: `Trivial|Easy|Challenging|Difficult|Very Difficult`

### `.agentic/artifacts/ux_ui_issue_list.md`
Table header:

```md
| severity | priority | fix_complexity | category | area | summary | reasoning | suggested_improvement |
| --- | --- | --- | --- | --- | --- | --- | --- |
```

Allowed scale values:
- `severity`: `Blocker|Very High|High|Normal|Minor`
- `priority`: `Very High|High|Medium|Low|Very Low`
- `fix_complexity`: `Trivial|Easy|Challenging|Difficult|Very Difficult`

### `.agentic/artifacts/security_issue_list.md`
Table header:

```md
| severity | priority | fix_complexity | category | area | summary | threat_scenario | evidence | suggested_mitigation |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
```

Allowed scale values:
- `severity`: `Blocker|Very High|High|Normal|Minor`
- `priority`: `Very High|High|Medium|Low|Very Low`
- `fix_complexity`: `Trivial|Easy|Challenging|Difficult|Very Difficult`
