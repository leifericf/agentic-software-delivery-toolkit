# Skill: Git commit

## Objective
Create a clean commit that matches this repository's existing commit message style.

## Output Boundary (STRICT)
See `@shared/skills/gates/prompt_output_boundary.md`.

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
3. Draft a one-line commit message that matches the repo style.
4. Stage only the intended files (`git add <paths>`).
5. Create the commit (`git commit -m "<message>"`).
6. Verify success (`git status`).

## Commit Message Style (STRICT)
- One line only.
- Sentence case, imperative mood (e.g. "Add ...", "Fix ...", "Move ...").
- Short and sweet.
- No trailing period.
- Avoid over-specific file lists; describe the intent.

## Output
Return:
- The commit hash
- The commit message
- A short list of what was committed
