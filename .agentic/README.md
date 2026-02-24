# Agentic Toolkit (Project-Local)

This directory contains the Agentic workflow prompts/templates and the durable planning/implementation artifacts they produce.

This toolkit is designed to be copied into an existing project repo at: `.agentic/`.

## Start

Optional: tag `@.agentic/setup/01_setup_wizard.md` to generate local preferences at `.agentic/.agentic_profile.md`.

Then start planning:
- `@.agentic/planning/01_describe_problem.md`

## Committing

Default: commit `.agentic/` (including `.agentic/artifacts/`) so your team shares the same prompts and durable context.

Ignored by default via `.agentic/.gitignore`:
- `.agentic/.agentic_profile.md` (per-user preferences)
- `.agentic/artifacts/operations/**` (often contains logs/customer data)

## Updating

To update the toolkit, replace only these directories:
- `.agentic/planning/`
- `.agentic/implementation/`
- `.agentic/operations/`
- `.agentic/shared/`
- `.agentic/setup/`

Do not overwrite:
- `.agentic/artifacts/`
- `.agentic/.agentic_profile.md`

## Advanced: Symlinks (macOS/Linux)

If you work on many repos locally, you can keep one clone of the toolkit and symlink the template folders into each project.

Important: Git commits symlinks as pointers (not the target contents). If you commit the symlink, teammates will usually get a broken link. Use this mode for local-only setups; teams should copy + commit `.agentic/`.

Recommended: keep artifacts local and symlink only templates (do not symlink `.agentic/artifacts/`).

## Windows note (symlinks)

On Windows, symlink behavior depends on your environment and settings. If you want to use symlinks, using WSL is recommended.
