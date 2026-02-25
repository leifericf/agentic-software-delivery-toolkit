# Shared Role Definitions

Reusable agent roles used across workflow steps and standalone prompts.

Workflow steps should keep their `## Role` section lean and reference one of these files instead.

Roles may also bundle reusable skills (see `@.agentic/shared/skills/README.md`).

Convention:
- Each role file is a short, expandable definition.
- Workflow steps reference roles via: `See @.agentic/shared/roles/<role_file>.md`.

## Core Roles (Default)

- `@.agentic/shared/roles/product_manager.md`
- `@.agentic/shared/roles/solution_architect.md`
- `@.agentic/shared/roles/ux_designer.md`
- `@.agentic/shared/roles/software_engineer.md`
- `@.agentic/shared/roles/quality_engineer.md`

Legacy/superseded roles may remain for reference, but workflow steps should use only the core roles.
