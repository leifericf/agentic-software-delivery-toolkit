# Shared Skills

Reusable markdown modules that can be referenced by roles, workflow steps, and standalone prompts.

Convention:
- Reference a skill with: `See @.agentic/shared/skills/<path>.md`.
- Skill files should be role-agnostic (skills do not reference roles).
- Roles bundle skills (one role -> many skills).
- Workflow steps reference a role, then add step-specific skills only when needed.

Directory guide:
- `gates/` - reusable gates and boundary rules
- `interaction/` - how to ask questions and run the chat loop
- `artifacts/` - reusable artifact conventions (decision log, etc)
- `planning/` - planning helpers (bootstrapping, UX gates)
- `implementation/` - implementation helpers (functional elicitation, automation)
- `git/` - git procedure modules
