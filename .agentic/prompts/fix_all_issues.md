# Prompt: Fix All Issues

## Role
Primary: `@.agentic/shared/roles/software_engineer.md`
Guardrails: `@.agentic/shared/roles/quality_engineer.md`

## Objective
Run a coordinated issue-remediation pass across all issue tracks and reduce release risk:
- Security issues
- Bugs
- UX/UI issues

This prompt is the single entry point for fixing issues at scale.

## Hard Rules
- Reuse the dedicated single-track fix workflow; do not duplicate lower-level fixing rules here:
  - `@.agentic/prompts/fix_issues_by_type.md`
- Follow repository-level policy (for example `AGENTS.md`).
- Follow `@.agentic/shared/skills/git/git_commit.md` (Conventional Commits, no amend unless explicitly requested, no push unless explicitly asked).
- Keep issue-type boundaries strict:
  - Security -> `.agentic/artifacts/security_issue_list.md`
  - Bugs -> `.agentic/artifacts/bug_list.md`
  - UX/UI -> `.agentic/artifacts/ux_ui_issue_list.md`
- One issue per commit. No mixed unrelated fixes in the same commit.

## Output Boundary
- You may change repo code/tests/docs and issue artifacts.
- Keep issue artifacts living and current by removing fixed rows in the same commit as each fix.
- Provide concise progress updates in chat.

## Fix Order (Default)
Use this default unless the user explicitly overrides:
1. Security issues
2. Bugs
3. UX/UI issues

Within each track, follow the ordering defined in `@.agentic/prompts/fix_issues_by_type.md`:
- Severity: `Blocker -> Very High -> High -> Normal -> Minor`
- Priority: `Very High -> High -> Medium -> Low -> Very Low`

## Procedure (Orchestration)
1. Confirm remediation scope:
   - all open issues vs selected tracks/areas
   - release target and timeline (if provided)
2. For each track in the selected order, run the dedicated fixer:
   - `@.agentic/prompts/fix_issues_by_type.md`
   - Choose the corresponding type (`security`, `bugs`, or `ux_ui`)
3. Continue until one of these stop conditions:
   - all selected issue lists are clear, or
   - remaining items are explicitly marked with data requests (`NEEDS_*`) and cannot be safely fixed yet, or
   - user requests stop/defer
4. After each fixed issue:
   - Ensure prevention was added/updated when feasible.
   - Ensure the issue row was removed in the same commit.
5. At track boundaries (security -> bugs -> UX/UI), provide a short checkpoint:
   - fixed count
   - remaining count by severity
   - blockers/data needed

## Completion Gate
When selected tracks are complete:
- Run the repo's standard full check suite (formatter/linter/tests/build) and fix failures.
- Re-run `@.agentic/prompts/find_all_issues.md` for a final release-readiness decision.

## Required Final Chat Summary
Return:
- What was fixed by track (security/bugs/UX/UI)
- Commits created (sha + short message)
- Remaining issues by track + severity
- Explicit unresolved data requests (`NEEDS_REPRO` / `NEEDS_VALIDATION` / `NEEDS_EVIDENCE`)
- Recommended release status: `GO | GO WITH RISKS | NO-GO`
