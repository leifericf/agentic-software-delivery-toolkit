
# Agentic Software Delivery Toolkit

Prompt-driven workflows and reusable prompt templates for planning and building software with LLM-powered agents.

The planning workflow is intentionally **pre-coding**: it helps you elicit constraints, make decisions explicit, and produce durable artifacts before you generate (or modify) a codebase.

The implementation workflow then uses those artifacts to pick a feature, plan the work, and deliver incrementally.

These templates emerged from many hours of experimentation across different LLMs and platforms and are intended to be mostly model-agnostic. Treat them as a starting point: fork this repo and adapt whatever you need as you learn what works for your team and project.

Core motivation: LLMs and "AI platforms" each ship their own conventions for defining agent behavior (roles, skills, system rules, tool policies). That creates a soft lock-in: your hard-earned patterns end up trapped in platform-specific features. This toolkit aims to sidestep that by keeping the core workflow and behavior in plain, portable, text-based prompts and artifacts you control. You can still layer on platform features if you want, but the intent is that your toolkit stays reusable across models and platforms (including future systems where the primary interface is text or audio).

## Goals

Main goal: help you reliably turn a fuzzy idea into shipped software by giving agents a clear workflow, durable context, and reusable templates that reduce repetition and cost.

Sub-goals:

- Make constraints and decisions explicit early (so you backtrack less).
- Support incremental delivery: small, reviewable changes with clear next steps.
- Produce reusable artifacts that persist across sessions and tools.
- Provide templates for commonly performed tasks so you don't have to repeat yourself.
- Codify hard-won software development experience into reusable workflows that guide agents toward higher quality output.
- Lower the barrier to entry for vibe coding, especially for non-technical builders.
- Optimize token usage (especially output tokens) to use models more economically.
- Stay model-agnostic and easy to fork, remix, and extend.

## What You Get

- A project-local `.agentic/` bundle you copy into an existing repo.
- A step-by-step planning sequence in `.agentic/planning/` (interactive templates).
- An implementation workflow in `.agentic/implementation/` for picking a feature, planning tasks, and delivering incrementally.
- Operations templates in `.agentic/operations/` for incident response, log triage, risk assessment, and retros.
- A consistent artifact set written to `.agentic/artifacts/`.
- Reusable roles + skills in `.agentic/shared/`.

## Install (Copy Into Your Repo)

This repo is a distribution source. You should not run the workflows here.

Assumption: one project per repo (artifacts live in `.agentic/artifacts/`).

1. Copy `.agentic/` into the root of your project repo.
2. Commit `.agentic/` (templates + durable artifacts live here).

Default ignores: `.agentic/.gitignore` keeps `.agentic/.agentic_profile.md` local and ignores `.agentic/artifacts/operations/**` by default.

3. (Optional) Run `@.agentic/setup/01_setup_wizard.md` to create `.agentic/.agentic_profile.md` (local preferences; gitignored by default).
4. Start with `@.agentic/planning/01_describe_problem.md` in your agent chat (tag the file if your tool supports it; otherwise copy/paste its contents).
5. Proceed in order through `@.agentic/planning/06_create_product_backlog.md`.
6. After planning is complete, tag `@.agentic/implementation/01_pick_feature.md` to start delivery.

Note: the agent tracks open questions in `.agentic/artifacts/open_questions.md` and captures decisions in `.agentic/artifacts/decision_log.md`.

Note: the agent keeps `.agentic/artifacts/product_backlog.md` up to date as a living document.

Tip: you can steer the agent's question style for the next turn by writing `Mode: natural`, `Mode: choice`, `Mode: binary`, or `Mode: creative`.

Optional steering knobs for the next turn:
- `@batch 1|2|3`
- `@interrupt minimal|balanced|interactive`
- `@depth light|standard|deep`

You do not need to front-load detail: start Step 01 with a loose paragraph describing the problem; the agent will drive the back-and-forth to gather specifics.

## Forking Guidance

- Rename steps, tweak questions, and delete anything you don't use.
- Add your own templates for recurring work (reviews, incidents, migrations, onboarding).
- Keep outputs consistent so your agents can find and reuse context across sessions.

## Workflows

- Planning: `.agentic/planning/README.md`
- Implementation: `.agentic/implementation/README.md`

## Git Skills

- `.agentic/shared/skills/git/git_commit.md`
- `.agentic/shared/skills/git/git_merge.md`

## Repo Layout

- `.agentic/`: copy this into your project repo
  - `setup/`: optional welcome/setup wizard (writes `.agentic/.agentic_profile.md`)
  - `planning/`: interactive planning templates
  - `implementation/`: implementation templates for delivery
  - `operations/`: free-standing templates for production/ops work (incidents, triage, risk)
  - `shared/`: shared templates used by multiple workflows
  - `artifacts/`: durable project context (committed by default)

## Advanced: Symlinks (macOS/Linux)

If you work on many repos locally, you can keep one clone of this toolkit and symlink the template folders into each project.

Important: Git commits symlinks as pointers (not the target contents). If you commit the symlink, teammates will usually get a broken link. Use this mode for local-only setups; teams should copy + commit `.agentic/`.

Recommended: keep artifacts local and symlink only templates (do not symlink `.agentic/artifacts/`).

Windows note (symlinks): if you want to use symlinks, using WSL is recommended.

## License

See `LICENSE`.
