# Prompt: Find Issues by Type

## Role
Primary: `@.agentic/shared/roles/quality_engineer.md`
Secondary: `@.agentic/shared/roles/software_engineer.md`

## Objective
Run issue discovery for one selected issue type:
- `bugs`
- `ux_ui`
- `security`

Use this as the single-track discovery entry point.

## Hard Rules
- Reuse dedicated track prompts; do not duplicate lower-level logic here:
  - `bugs` -> `@.agentic/prompts/find_bugs.md`
  - `ux_ui` -> `@.agentic/prompts/find_ux_ui_issues.md`
  - `security` -> `@.agentic/prompts/find_security_issues.md`
- First action is mandatory: ask exactly one targeted question:
  - `Do you want to find bugs, UX/UI issues, or security issues?`
- Keep issue-type boundaries strict (no cross-logging between artifacts).
- Follow repository-level policy (for example `AGENTS.md`) and relevant `@.agentic/` policies.

## Output Boundary
- Update exactly one selected living artifact:
  - Bugs -> `.agentic/artifacts/bug_list.md`
  - UX/UI -> `.agentic/artifacts/ux_ui_issue_list.md`
  - Security -> `.agentic/artifacts/security_issue_list.md`
- Optional: brief chat recap (3-8 bullets) of what changed.

## Issue Type Routing (Mandatory)
After the user answers, run the corresponding dedicated discovery prompt:

- `bugs` -> `@.agentic/prompts/find_bugs.md`
- `ux_ui` -> `@.agentic/prompts/find_ux_ui_issues.md`
- `security` -> `@.agentic/prompts/find_security_issues.md`

## Completion
Return:
- Selected issue type
- Artifact updated
- Count of new or updated rows
- Any unresolved data-request markers (`NEEDS_REPRO` / `NEEDS_VALIDATION` / `NEEDS_EVIDENCE`)
