# Agentic Toolkit (Project-Local)

Copy this folder into a project repo as `.agentic/`.

## Start

Optional: Tag `@.agentic/setup/01_setup_wizard.md` to generate local preferences in `.agentic/.agentic_profile.md`.

Windows note: some tools treat `@<path>` as a file include and require `/` separators.
Use `@.agentic/planning/01_describe_problem.md` (not `@.agentic\planning\01_describe_problem.md`).

Then tag:
- `@.agentic/planning/01_describe_problem.md`

## Committing

Default: commit `.agentic/` (including `.agentic/artifacts/`) so your team shares the same prompts and durable context.

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
