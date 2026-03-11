# Skill: Git commit

## Objective
Create a clean commit that follows Conventional Commits v1.0.0.

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/prompt_output_boundary.md`.

## Safety Rules (Mandatory)
- Do not commit secrets (e.g. `.env`, credentials, API keys).
- Do not amend commits unless the user explicitly requests it.
- Do not run destructive git commands (e.g. `reset --hard`, force push).
- Do not push unless the user explicitly asks.
- Never disable or bypass Git hooks. This includes `--no-verify` and equivalent workarounds.
- If a hook fails, fix the underlying issue and retry. Do not attempt to skip enforcement.
- If a local `commit-msg` hook enforces Conventional Commits and rejects the message, fix the message and retry.

## Inputs
The user provides a goal like: "commit my changes".

## Procedure
1. Inspect changes:
   - `git status`
   - `git diff`
   - `git log -10 --oneline`
2. Decide what should be included in the commit.
   - If there are unrelated changes, call them out and ask whether to include them.
   - If any file likely contains secrets, warn and exclude it.
   - If you are executing a task plan, include the corresponding checkbox updates in `.agentic/artifacts/tasks/plan-<feature_slug>.md` in the SAME commit as the work that completed the task.
3. Draft a Conventional Commit message (header always; body/footers only when needed).
   - Validate header format: `^(feat|fix|docs|style|refactor|perf|test|build|ci|chore|revert)(\([a-z0-9][a-z0-9_-]*\))?(!)?: [^ ].+`.
   - If invalid, rewrite before committing.
4. Stage only the intended files (`git add <paths>`).
5. Create the commit (`git commit -m "<message>"`).
6. Verify success (`git status`) and re-check created subject (`git log -1 --format=%s`) is Conventional Commit-compliant.

## Commit Message Style (STRICT)
Use Conventional Commits v1.0.0:

```
<type>[optional scope][optional !]: <description>

[optional body]

[optional footer(s)]
```

Rules:
- The header MUST start with a `type`: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, `build`, `perf`, `revert`, `style`.
- A `scope` MAY be provided in parentheses (use a short noun for the affected area, e.g. `auth`, `ci`, `git`).
- The `description` MUST follow `: ` and be a short, human-readable summary.
- Breaking changes MUST be indicated with `!` before the `:` and/or a `BREAKING CHANGE:` footer.

Guidance:
- Prefer a single-line header; add a body/footer only when it adds necessary context.
- Avoid over-specific file lists; describe the intent.
- Focus on the "why" rather than the "what" - the diff shows what changed.
- Never include plan-internal identifiers (e.g. chunk IDs like `CH-001`, task IDs like `T-003`) in commit messages.

## Commit Hygiene (Before Trunk Push)
Before merging work into trunk and pushing, review local history and clean it up:

1. **Squash intermediate commits**: collapse `WIP`, `fixup!`, `squash!`, and similar work-in-progress commits into logical commits using `git rebase -i`.
2. **Ensure every commit tells a clear story**: each commit should represent one logical change that can be understood independently.
3. **Reword vague messages**: if any commit subject is unclear, reword it during interactive rebase.
4. **Never push intermediate commits to trunk**.

## Output
Return:
- The commit hash
- The commit message
- A short list of what was committed
