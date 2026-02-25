# Agentic Software Delivery Toolkit

Prompt-driven planning + delivery workflows you can copy into a repo as plain text.

Goal: help you turn a fuzzy idea into shipped software by giving agents a clear workflow, durable context, and reusable templates.

## Goals

- Make decisions and constraints explicit early.
- Deliver incrementally (small, testable chunks).
- Keep context durable across sessions (committed artifacts).
- Stay model/tool agnostic (text files you control).

## What You Get

- A project-local `.agentic/` bundle you copy into an existing repo.
- A planning workflow in `.agentic/planning/` that produces durable artifacts.
- An implementation workflow in `.agentic/implementation/` that executes in small chunks.
- Operations templates in `.agentic/operations/` for incident response, log triage, risk assessment, and retros.
- A consistent artifact set written to `.agentic/artifacts/`.
- Reusable roles + skills in `.agentic/shared/`.

## Install (Copy Into Your Repo)

This repo is a distribution source. You should not run the workflows here.

Assumption: one project per repo (artifacts live in `.agentic/artifacts/`).

1. Copy `.agentic/` into the root of your project repo.
2. Commit `.agentic/` (templates + durable artifacts live here; operations artifacts under `.agentic/artifacts/operations/` are ignored by default).

Default ignores: `.agentic/.gitignore` keeps `.agentic/.agentic_profile.md` local and ignores `.agentic/artifacts/operations/**` by default.

## Start

1. (Optional) Tag `@.agentic/setup/01_setup_wizard.md` to create `.agentic/.agentic_profile.md` (local preferences; gitignored by default).
2. Tag `@.agentic/planning/01_describe_problem.md` in your agent chat (or copy/paste its contents).
3. Proceed in order through `@.agentic/planning/06_create_product_backlog.md`.
4. Tag `@.agentic/implementation/01_pick_feature.md` to start delivery (after planning is complete).

Windows note: some tools treat `@<path>` as a file include and require `/` separators.
Use `@.agentic/planning/01_describe_problem.md` (not `@.agentic\planning\01_describe_problem.md`).

Note: the agent tracks open questions in `.agentic/artifacts/open_questions.md` and captures decisions in `.agentic/artifacts/decision_log.md`.

Note: the agent keeps `.agentic/artifacts/product_backlog.md` up to date as a living document.

You do not need to front-load detail: start Step 01 with a loose paragraph; the agent will pull specifics through questions.

To customize: rename steps, tweak questions, and delete anything you don't use.

## Advanced: Symlinks (macOS/Linux)

If you work on many repos locally, you can keep one clone of this toolkit and symlink the template folders into each project.

Important: Git commits symlinks as pointers (not the target contents). If you commit the symlink, teammates will usually get a broken link. Use this mode for local-only setups; teams should copy + commit `.agentic/`.

Recommended: keep artifacts local and symlink only templates (do not symlink `.agentic/artifacts/`).

Windows note (symlinks): if you want to use symlinks, using WSL is recommended.
