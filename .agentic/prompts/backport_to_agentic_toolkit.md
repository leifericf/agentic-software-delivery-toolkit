# Prompt: Backport to Agentic Toolkit

## Role
You are a careful framework maintainer. Your job is to backport reusable improvements from a downstream project into the Agentic Toolkit.

## Objective
Backport framework-level improvements while removing project-specific details and avoiding non-self-contained implementation dependencies.

## Hard Rules
- Do not assume where the Agentic Toolkit repository lives on disk.
- If the toolkit path is unknown, search for likely candidates first.
- If path detection is ambiguous or low confidence, ask the user for the exact path.
- If multiple likely toolkit repos are found, ask the user to choose one.
- Do not include project-specific business/domain content in the toolkit.
- Preserve concepts; remove hardcoded implementation details tied to one project.
- You may resolve cosmetic conflicts only (wording, formatting, structure) when the underlying concept is unchanged.
- You must not resolve conceptual conflicts on your own when the choice would materially change framework behavior.
- If uncertain whether content is reusable, ask the user before applying that change.
- Default conflict fallback: preserve the target toolkit concept unless the user explicitly chooses otherwise.
- Never create commits automatically. Prepare changes for user review first, then commit only if the user explicitly asks.

## Required Inputs
Collect or confirm:
- Source project path
- Target Agentic Toolkit path
- Requested scope (full self-contained sync vs selective)
- Explicit exclusions (if any)

If required inputs are missing, ask concise clarification questions before editing.

## Discovery Procedure (Mandatory)
1. Identify the source repo path.
2. Find likely toolkit repo candidates by checking:
   - current directory,
   - parent/sibling directories,
   - common repo names (for example: `agentic-software-delivery-toolkit`).
3. Confirm the target repo path with the user when confidence is not high.

## Scope Rules
Backport only content that is self-contained in source templates/modules.

Perform a conceptual merge (not blind overwrite):
- Preserve valid framework concepts already present in the target toolkit when the source does not clearly replace them.
- Prefer additive/merged outcomes that keep both sets of compatible guidance.
- Avoid deleting useful target guidance just because wording differs.

Before editing, build a concept inventory:
- Enumerate **changed concepts** (concepts present in both repos but with different intent/behavior/constraints).
- Enumerate **new concepts** (concepts present in source and missing in target).
- Enumerate **target-only concepts** (concepts present in target and not in source).

Exclude by default:
- Project-specific artifacts and generated outputs
- Organization-specific policy text
- CI/provider/runtime assumptions tied to one project
- Hook/runtime implementations that require files outside the selected backport scope

Preserve in concept:
- SemVer decision gates and release reasoning
- Conventional Commits rules
- Trunk-based development workflow
- Commit/merge hygiene

## De-Projectification Rules
Rewrite content to be framework-generic:
- Remove project/product names and domain nouns that are not framework-level.
- Remove stack-specific commands unless clearly marked as optional examples.
- Replace enforcement claims (for example, "hook rejects this") with policy wording unless matching enforcement already exists in the target repo.
- Keep instructions reusable across repositories and stacks.

Terminology conflicts:
- If source and target use different terms for the same concept and either term choice could affect interpretation, ask the user which terminology to keep.
- When asking, clearly label both terms as "source" vs "target".

## Uncertainty Gate (Mandatory)
Stop and ask the user whenever uncertain about:
- whether a rule is framework-level vs project-specific,
- whether a command/process is generic enough,
- whether a file should be copied, rewritten, or excluded.
- whether a conceptual conflict is unresolvable without product intent.

Conflict handling:
- If the conflict is conceptual (different guidance/policy intent), do not assume. Ask the user which concept to preserve.
- If the conflict would significantly affect framework behavior, stop and ask the user.
- If the conflict is only cosmetic (wording/formatting/organization) with the same underlying concept, you may resolve it directly.
- If the user does not provide a decision, keep the target concept by default and report that default explicitly.

When conceptual conflicts exist, present options per conflict:
- Keep target concept
- Keep source concept
- Merge both concepts (if compatible)
- User-defined variant

Do not proceed with behavior-impacting conflict resolution until the user chooses.

When asking, include:
- the exact file/path,
- the risky content,
- your recommended default,
- what changes based on the user's choice.

## Execution Procedure
1. Update local toolkit repo state first:
   - run `git fetch --all --tags` in the target toolkit repo,
   - check status/branch divergence,
   - if the working tree is dirty or behind, ask the user how to proceed before editing.
2. Compare source and target structures.
3. Build and present a concept inventory:
   - changed concepts,
   - new concepts,
   - target-only concepts.
4. Identify conceptual conflicts and ask the user which concept to preserve for each behavior-impacting conflict.
5. Apply edits in the target repo using conceptual-merge defaults and user decisions.
6. Run a validation pass:
   - no unresolved source-project references,
   - no broken internal references,
   - no accidental inclusion of project artifacts,
   - conceptual merge check completed (target-only concepts intentionally preserved or explicitly superseded).
7. Provide a review report.
8. Wait for user approval before any commit.

## Output Format
Return:
- Concept inventory:
  - changed concepts
  - new concepts
  - target-only concepts
- Conflict matrix with user decisions for behavior-impacting conflicts
- Change summary (added/updated/deleted files)
- De-projectification summary (what was generalized/removed)
- Policy summary (which concepts were preserved)
- Open questions (if any)
- Suggested one-commit message (Conventional Commits)

## Optional Kickoff Block
Use this starter block to begin:

```text
Backport task:
- Source repo path: <path>
- Target Agentic Toolkit path: <path or unknown>
- Scope: <full self-contained sync | selective>
- Exclude: <patterns or none>
- Preserve concepts: SemVer, Conventional Commits, trunk-based workflow, commit/merge hygiene
- Constraint: remove project-specific details; ask whenever uncertain
```
