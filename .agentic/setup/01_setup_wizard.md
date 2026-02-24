# Setup Wizard (Welcome Workflow)

## Role
See `@.agentic/shared/roles/product_manager.md`.

## Operating Mode
- Interactive preference capture.
- Ask questions via `@.agentic/shared/skills/interaction/questions_format.md` (cap 3 per turn).

## Output Boundary (STRICT)
Override: this step writes/updates a repo-local profile file.

- Chat mode: follow `@.agentic/shared/skills/gates/output_boundary.md`.
- Artifact mode: output exactly one `md` fenced code block containing the full contents of `.agentic/.agentic_profile.md`.

## Inputs
- Optional: existing `.agentic/.agentic_profile.md` (if present, treat it as the source of truth; update it, do not throw it away).

## Objective
Capture how the user wants to work with the agent so future steps can adapt automatically.

## Instructions
1. If `.agentic/.agentic_profile.md` exists, skim it first.
2. Ask only for missing/unclear fields, plus any updates the user wants to make.
3. Use Choice mode when it speeds things up; otherwise Natural.
4. Never request or store secrets (API keys, tokens, passwords). If the user shares one, tell them to remove it and do not include it.

## Question Set (Use In Small Batches)
Prioritize in this order:

1) Interaction defaults
- Default question mode (Natural/Choice/Binary/Creative)
- Question batch size (1/2/3)
- Interruption tolerance (Minimal/Balanced/Interactive)
- Probing depth (Light/Standard/Deep)
- Defaults vs questions preference
- Verbosity preference

2) Engineering preferences (only if relevant)
- Languages/frameworks you prefer
- Testing preference
- Tooling defaults (package manager/test runner)
- Git conventions

3) Constraints / red lines
- Anything the agent must avoid or must do

## Output File
Write/update: `.agentic/.agentic_profile.md`

## Output Format (STRICT)
Write `.agentic/.agentic_profile.md` using the template in `.agentic/setup/agentic_profile.template.md`.

After generating `.agentic/.agentic_profile.md`, ask (Chat mode, separate message):

> "Profile saved. If you're starting a new project, tag **@.agentic/planning/01_describe_problem.md**."
