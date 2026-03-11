# Agentic Toolkit (Project-Local)

Copy this folder into a project repo as `.agentic/`.

## Start

Optional: Tag `@.agentic/setup/01_setup_wizard.md` to generate local preferences in `.agentic/.agentic_profile.md`.

Windows note: some tools treat `@<path>` as a file include and require `/` separators.
Use `@.agentic/planning/01_describe_problem.md` (not `@.agentic\planning\01_describe_problem.md`).

Then tag:
- `@.agentic/planning/01_describe_problem.md`

## Runtime Policy (For Agents)

- Treat this toolkit as required operating policy, not optional reference material.
- On every request, load and follow the task-relevant `.agentic` sections before acting.
- If `.agentic` guidance conflicts with repository-level framework rules, defer to the repository policy.
- Minimum routing by task type:
  - Implementation -> `@.agentic/implementation/README.md`
  - Committing changes -> `@.agentic/shared/skills/git/git_commit.md`
  - Branch integration -> `@.agentic/shared/skills/git/git_merge.md`
  - Release prep/tagging -> `@.agentic/shared/skills/release/semver_release.md`
  - Planning/operations -> matching files in `.agentic/planning/` or `.agentic/operations/`

## Committing

Default: commit `.agentic/` (including `.agentic/artifacts/`) so your team shares the same prompts and durable context.

Enforcement rule for AI agents:
- Never bypass Git hooks. Do not use `--no-verify` (or similar workarounds) for commits or pushes.
- If a hook rejects an action, fix the root cause and retry.

Ignored by default via `.agentic/.gitignore`:
- `.agentic/.agentic_profile.md` (per-user preferences)
- `.agentic/artifacts/operations/**` (often contains logs/customer data)

## Updating

To update the toolkit, replace only:
- `.agentic/planning/`
- `.agentic/implementation/`
- `.agentic/operations/`
- `.agentic/shared/`
- `.agentic/setup/`

Do not overwrite:
- `.agentic/artifacts/`
- `.agentic/.agentic_profile.md`

## Advanced: Symlinks (macOS/Linux)

If you work on many repos locally, you can keep one clone of the toolkit and symlink template folders into each project.

Important: Git commits symlinks as pointers (not contents). This is best for local-only setups.

Recommended: keep artifacts local and symlink only templates (do not symlink `.agentic/artifacts/`).

## Windows Note (Symlinks)

If you want symlinks on Windows, using WSL is recommended.
