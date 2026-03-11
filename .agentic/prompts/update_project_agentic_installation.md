# Prompt: Update Project Agentic Installation

## Role
You are a careful framework maintainer. Your job is to update a project's installed `.agentic/` toolkit content from the canonical Agentic Toolkit repository.

## Objective
Sync reusable toolkit modules into a project while preserving project-local artifacts, local preferences, and any explicitly excluded files.

## Hard Rules
- Do not assume where the project repository lives on disk.
- Do not assume where the canonical toolkit repository lives on disk.
- Accept a remote toolkit source (GitHub URL + ref) when no local toolkit clone exists.
- If a local toolkit clone exists, update that clone from GitHub first before using it as source.
- If either path is unknown, search for likely candidates first.
- If path detection is ambiguous or low confidence, ask the user for exact paths.
- If multiple likely candidates are found, ask the user to choose.
- Never overwrite project-local durable context by default:
  - `.agentic/artifacts/`
  - `.agentic/.agentic_profile.md`
- Never overwrite project-specific policy/docs unless explicitly requested.
- Do not include generated outputs, logs, or environment-specific files from either repo.
- Preserve existing project behavior on conceptual conflicts unless the user explicitly chooses otherwise.
- Never create commits automatically. Prepare changes for review first; commit only if the user explicitly asks.

## Required Inputs
Collect or confirm:
- Source toolkit: local repo path **or** remote repo URL + ref (branch/tag/commit)
- Target project repo path (project installation to update)
- Requested scope (`full template sync` or `selective`)
- Explicit exclusions (if any)

If required inputs are missing, ask concise clarification questions before editing.

## Discovery Procedure (Mandatory)
1. Identify likely project repo path.
2. Identify likely toolkit repo path by checking current directory, parent/siblings, and common names (e.g. `agentic-software-delivery-toolkit`).
3. If no confident local toolkit path is found, ask for a remote source (e.g. GitHub URL + ref).
4. Confirm chosen source/target with the user when confidence is not high.

## Source Resolution Strategy (Mandatory)
Use this order:
1. **Preferred**: Existing local toolkit clone
   - Update it first (`git fetch --all --tags`, then align to requested/default ref).
   - Use the updated local clone as source.
2. **Fallback**: Remote toolkit source
   - Fetch/clone the requested ref into a temporary directory.
   - Use that temporary snapshot as source.
   - Remove temporary clone/snapshot after update work is complete.

## Remote Source Fallback (When Toolkit Is Not Cloned)
If a local toolkit clone is unavailable, use a temporary source snapshot:
- Fetch from GitHub using a specific ref (tag preferred for reproducibility).
- Materialize snapshot in a temporary directory and treat it as read-only source.
- Do not create commits in the temporary source.
- Clean up temporary clone/snapshot after completion.
- Record source provenance in the review report:
  - repo URL,
  - ref requested,
  - resolved commit SHA (if available).

## Scope Rules
Default sync targets (safe template paths):
- `.agentic/planning/`
- `.agentic/implementation/`
- `.agentic/operations/`
- `.agentic/shared/`
- `.agentic/setup/`
- `.agentic/prompts/` (only prompt templates intended for toolkit distribution)
- `.agentic/README.md`

Default preserve targets (do not overwrite unless explicitly requested):
- `.agentic/artifacts/`
- `.agentic/.agentic_profile.md`
- Any project-only docs/policies outside `.agentic/`

Perform a conceptual merge (not blind overwrite):
- Preserve valid project-local additions that are not in conflict.
- Prefer additive outcomes when both versions provide compatible guidance.
- Avoid deleting useful project guidance just because wording differs.

Before editing, build a concept inventory:
- Enumerate **changed concepts** (present in both, but with different behavior/intent).
- Enumerate **new concepts** (present in toolkit, missing in project copy).
- Enumerate **project-only concepts** (present in project copy, missing in toolkit).

## Conflict and Uncertainty Gate (Mandatory)
Stop and ask the user when uncertain about:
- whether a file is project-local and should be preserved,
- whether a conceptual conflict would change project behavior,
- whether a project-only customization should be retained or replaced.

Conflict handling:
- Conceptual conflict: do not assume; ask the user to choose.
- Cosmetic conflict with same meaning: resolve directly.
- If the user does not choose, keep the project's current concept by default and report that default explicitly.

When asking, include:
- exact file/path,
- risky content,
- recommended default,
- what changes based on the choice.

## Execution Procedure
1. Update local project repo state first:
   - Run `git fetch --all --tags` in the target project repo.
   - Check status/branch divergence.
   - If working tree is dirty or behind, ask the user how to proceed before editing.
2. Resolve toolkit source:
   - If local clone exists, update it from GitHub and use it.
   - Otherwise fetch/clone a remote snapshot to a temporary directory and use it.
3. Compare toolkit `.agentic/` and project `.agentic/` structure.
4. Build and present concept inventory:
   - changed concepts,
   - new concepts,
   - project-only concepts.
5. Identify conceptual conflicts and ask for user decisions on behavior-impacting conflicts.
6. Apply updates in the project repo using conceptual merge defaults and user decisions.
7. Run a validation pass:
   - no broken internal `@.agentic/...` references,
   - no accidental overwrite of `.agentic/artifacts/` or `.agentic/.agentic_profile.md`,
   - no toolkit-external implementation dependencies introduced,
   - conceptual merge check completed.
8. Provide a review report.
9. Wait for user approval before any commit.

## Output Format
Return:
- Concept inventory:
  - changed concepts
  - new concepts
  - project-only concepts
- Conflict matrix with user decisions for behavior-impacting conflicts
- Change summary (added/updated/deleted files)
- Preservation summary (what was intentionally kept project-local)
- Validation summary
- Source provenance (local path or remote URL/ref/SHA)
- Open questions (if any)
- Suggested one-commit message (Conventional Commits)

## Optional Kickoff Block
Use this starter block to begin:

```text
Project toolkit update task:
- Source toolkit: <local path or remote URL>
- Source ref: <tag|branch|commit or default branch>
- Target project repo path: <path or unknown>
- Scope: <full template sync | selective>
- Exclude: <patterns or none>
- Preserve by default: .agentic/artifacts/, .agentic/.agentic_profile.md, project-only policies
- Constraint: ask whenever uncertain about behavior-impacting conflicts
```
