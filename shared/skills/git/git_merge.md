# Skill: Git merge

## Objective
Merge a local feature branch into `main` safely and cleanly.

## Output Boundary (STRICT)
See `@shared/skills/gates/prompt_output_boundary.md`.

## Safety Rules (Mandatory)
- Do not run destructive git commands (e.g. `reset --hard`, force push).
- Do not disable hooks (no `--no-verify`) unless the user explicitly asks.
- Do not push unless the user explicitly asks.
- Never use `git merge --no-ff` unless the user explicitly requests it.
- Only delete the local feature branch after a successful merge into `main`.
- When deleting, use `git branch -d` (not `-D`).
- Always verify you are back on `main` after the merge.

## Inputs
The user provides a goal like: "merge my feature branch" and may specify the branch name.

## Procedure
1. Inspect context:
   - `git status`
   - `git branch --show-current`
   - `git branch --list`
2. Ensure a clean working tree.
   - If there are uncommitted changes, stop and ask whether to commit/stash them first.
3. Switch to `main`:
   - `git checkout main`
4. Update `main` locally (no surprises):
   - `git pull --ff-only`
5. Merge the feature branch into `main`:
   - Default: `git merge <feature_branch>`
   - Only if the user explicitly requests a merge commit: `git merge --no-ff <feature_branch>`
   - If there are conflicts, stop and tell the user exactly what needs resolving (do not auto-resolve).
6. Verify merge success:
   - `git status`
   - Confirm the merge completed and there is no in-progress merge.
7. Delete the local feature branch (only after success):
   - `git branch -d <feature_branch>`
8. Verify you are on `main`:
   - `git branch --show-current`

## Output
Return:
- The merged branch name
- Whether `--no-ff` was used
- Whether the local feature branch was deleted
- The current branch (must be `main`)
