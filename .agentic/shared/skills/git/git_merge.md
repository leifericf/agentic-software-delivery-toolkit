# Skill: Git merge (Trunk-Based Development)

## Objective
Integrate a local feature branch into trunk safely with linear history.

This toolkit assumes **trunk-based development**. All work is integrated into trunk (`master`/`main`). Local branches are allowed for development but should not be published to remote unless your project policy explicitly allows it.

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/prompt_output_boundary.md`.

## Safety Rules (Mandatory)
- Do not run destructive git commands (e.g. `reset --hard`, force push).
- Never disable or bypass Git hooks. This includes `--no-verify` and equivalent workarounds.
- If a hook fails, fix the underlying issue and retry. Do not attempt to skip enforcement.
- Do not push unless the user explicitly asks.
- **Never** use `git merge --no-ff`. Merge commits are forbidden on trunk in this workflow.
- **Always** prefer rebase to produce linear history.
- Only delete the local feature branch after a successful merge into trunk.
- When deleting, use `git branch -d` (not `-D`).
- Always verify you are back on trunk after the merge.

## Inputs
The user provides a goal like: "merge my feature branch" and may specify the branch name.

## Procedure
1. Inspect context:
   - `git status`
   - `git branch --show-current`
   - `git branch --list`
2. Ensure a clean working tree.
   - If there are uncommitted changes, stop and ask whether to commit/stash them first.
3. Identify trunk branch name (`main` or `master`) from repository state.
4. **Clean up commits before merging** (mandatory):
   - Review branch commits: `git log <trunk_branch>..<feature_branch> --oneline`
   - Squash intermediate commits (`WIP`, `fixup!`, `squash!`) into logical commits using `git rebase -i`.
   - Ensure every remaining commit follows Conventional Commits v1.0.0.
5. Rebase the feature branch onto trunk:
   - `git rebase <trunk_branch>`
   - If there are conflicts, stop and tell the user exactly what needs resolving (do not auto-resolve).
6. Switch to trunk:
   - `git checkout <trunk_branch>`
7. Update trunk locally:
   - `git pull --ff-only`
8. Fast-forward merge the feature branch:
   - `git merge --ff-only <feature_branch>`
   - If fast-forward is not possible, rebase again.
9. Verify merge success:
   - `git status`
   - Confirm the merge completed cleanly with linear history.
10. Delete the local feature branch (only after success):
   - `git branch -d <feature_branch>`
11. Verify you are on trunk:
   - `git branch --show-current`

## Push Policy
- **Never** push feature branches to the remote unless the project explicitly allows it.
- Only push trunk (`master`/`main`) and tags.
- Only push when the user explicitly asks.

## Output
Return:
- The merged branch name
- Confirmation that fast-forward merge was used (no merge commit)
- Whether the local feature branch was deleted
- The current branch (must be trunk)
