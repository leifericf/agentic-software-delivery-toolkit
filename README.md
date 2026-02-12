
# Agentic Software Delivery Toolkit

Workflows and prompt templates for planning and shipping software with LLM-powered agents.

This repo is intentionally **pre-coding**: it helps you elicit constraints, make decisions explicit, and produce durable artifacts before you generate a codebase.

These templates emerged from many hours of experimentation across different LLMs and platforms and are intended to be mostly model-agnostic. Treat them as a starting point: fork this repo and adapt whatever you need as you learn what works for your team and project.

## What You Get

- A step-by-step planning sequence in `planning/` (interactive templates).
- An implementation workflow in `implementation/` for picking a feature, planning tasks, and delivering incrementally.
- A consistent artifact set written to `artifacts/<project_slug>/`.
- Reusable standalone prompts in `prompts/`.

## Quickstart

1. Fork this repo and make it your own.
2. Start with `@planning/01_describe_problem.md` in your agent chat (tag the file if your tool supports it, otherwise copy/paste its contents).
3. Step 01 will capture your project name, define the project slug, and bootstrap `artifacts/<project_slug>/`.
4. Proceed in order through `planning/10_design_repo_blueprint.md`.

Note: the agent tracks open questions in `artifacts/<project_slug>/00_open_questions.md` and captures decisions in `artifacts/<project_slug>/04_decision_log.md`. You can paste answers into the open questions file and ask the agent to incorporate them into the relevant artifacts.

You do not need to front-load detail: start Step 01 with a loose paragraph describing the problem; the agent will drive the back-and-forth to gather specifics.

## Forking Guidance

- Rename steps, tweak questions, and delete anything you don't use.
- Add your own templates for recurring work (reviews, incidents, migrations, onboarding).
- Keep outputs consistent so your agents can find and reuse context across sessions.

## Operating Principles

- Sequence beats cleverness: the order of decisions matters.
- Prefer durable simplicity: designs that still feel right in 5-10 years.
- Put novelty in the product, keep infrastructure boring.
- Capture decisions: undocumented decisions get re-litigated.
- Constrain the agent: good outputs follow good constraints.

## Workflows

- Planning: `planning/README.md`
- Implementation: `implementation/README.md`

## Standalone Prompts

Prompt templates you can use independently live in `prompts/`.

- `prompts/git_commit.md`

## Repo Layout

- `planning/`: interactive planning templates
- `implementation/`: implementation templates for delivery
- `shared/`: shared templates used by multiple workflows
- `prompts/`: standalone prompts
- `artifacts/`: project-specific outputs (directory included; contents ignored by default)

## License

See `LICENSE`.
