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
- Do not disable hooks (no `--no-verify`) unless the user explicitly asks.

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
4. Stage only the intended files (`git add <paths>`).
5. Create the commit (`git commit -m "<message>"`).
6. Verify success (`git status`).

## Commit Message Style (STRICT)
Use Conventional Commits v1.0.0:

```
<type>[optional scope][optional !]: <description>

[optional body]

[optional footer(s)]
```

Rules:
- The header MUST start with a `type` (e.g. `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`, `build`, `perf`, `revert`).
- A `scope` MAY be provided in parentheses (use a short noun for the affected area, e.g. `agentic`, `implementation`, `git`).
- The `description` MUST follow `: ` and be a short, human-readable summary.
- Breaking changes MUST be indicated with `!` before the `:` and/or a `BREAKING CHANGE:` footer.

Guidance:
- Prefer a single-line header; add a body/footer only when it adds necessary context.
- Avoid over-specific file lists; describe the intent.

## Output
Return:
- The commit hash
- The commit message
- A short list of what was committed
