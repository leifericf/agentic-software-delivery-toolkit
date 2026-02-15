# Shared Skills

Reusable markdown modules that can be referenced by roles, workflow steps, and standalone prompts.

Convention:
- Reference a skill with: `See @shared/skills/<path>.md`.
- Skill files should be role-agnostic (skills do not reference roles).
- Roles bundle skills (one role -> many skills).
- Workflow steps reference a role, then add step-specific skills only when needed.

Directory guide:
- `shared/skills/gates/` - reusable gates and boundary rules
- `shared/skills/interaction/` - how to ask questions and run the chat loop
- `shared/skills/artifacts/` - reusable artifact conventions (decision log, etc)
- `shared/skills/planning/` - planning helpers (slugs, bootstrapping, UX gates)
- `shared/skills/implementation/` - implementation helpers (functional elicitation, automation)
- `shared/skills/git/` - git procedure modules
