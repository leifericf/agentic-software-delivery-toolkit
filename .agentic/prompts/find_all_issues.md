# Prompt: Find All Issues

## Role
Primary: `@.agentic/shared/roles/quality_engineer.md`
Secondary: `@.agentic/shared/roles/software_engineer.md`

## Objective
Run a pre-release issue sweep across all issue tracks and keep the living issue artifacts current:
- Bugs
- UX/UI issues
- Security issues

This prompt is the single preflight entry point before release.

## Hard Rules
- Do not fix issues in this prompt unless the user explicitly asks. This prompt is discovery + triage + readiness assessment.
- Do not duplicate lower-level issue logic here; route discovery through `@.agentic/prompts/find_issues_by_type.md`.
- Keep issue boundaries strict (no cross-logging between artifacts).
- Follow repository-level policy (for example `AGENTS.md`) and relevant `@.agentic/` policies.

## Output Boundary
- Update only these living artifacts (create if missing via the dedicated prompts):
  - `.agentic/artifacts/bug_list.md`
  - `.agentic/artifacts/ux_ui_issue_list.md`
  - `.agentic/artifacts/security_issue_list.md`
- Provide a concise release-readiness summary in chat.

## Procedure (Orchestration)
1. Confirm preflight context:
   - target branch/commit
   - release scope (what changed)
   - interface surfaces in scope (web/CLI/mobile/desktop/etc.)
2. Run issue discovery for each track via `@.agentic/prompts/find_issues_by_type.md`:
   - Run once for `bugs`
   - Run once for `ux_ui`
   - Run once for `security`
3. Ensure each artifact is deduplicated and current.
4. Cross-check boundaries:
   - Bug-only findings are in `bug_list.md`
   - UX/UI-only findings are in `ux_ui_issue_list.md`
   - Security-only findings are in `security_issue_list.md`
5. Produce a preflight release-readiness decision with evidence:
   - `GO`
   - `GO WITH RISKS`
   - `NO-GO`

## Readiness Heuristic (Default)
Use this default unless the user provides stricter project policy:

- `NO-GO` when any of the following are true:
  - Any open `Blocker` in any issue list
  - Any open `Very High` security issue
  - Any unresolved issue that can cause data loss, legal/compliance exposure, or unsafe behavior
- `GO WITH RISKS` when no `NO-GO` condition is present, but open `Very High`/`High` non-security issues remain.
- `GO` when remaining open issues are acceptable by team policy and release goals.

## Required Chat Summary Format
Return:
- Release decision: `GO | GO WITH RISKS | NO-GO`
- Counts by track and severity (bugs, UX/UI, security)
- Top 3 release risks (area + summary + why)
- Recommended next action:
  - If `NO-GO`: suggest `@.agentic/prompts/fix_all_issues.md`
  - If `GO WITH RISKS`: list explicit accepted risks
  - If `GO`: list post-release watch items
