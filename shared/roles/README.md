# Shared Role Definitions

These files define reusable agent roles used across workflow steps and standalone prompts.

Workflow steps should keep their `## Role` section lean and reference one of these files instead.

Convention:
- Each role file is a short, expandable definition.
- Workflow steps reference roles via: `See @shared/roles/<role_file>.md`.

## Core roles (default)

- `@shared/roles/product_manager.md`
- `@shared/roles/solution_architect.md`
- `@shared/roles/ux_designer.md`
- `@shared/roles/software_engineer.md`
- `@shared/roles/quality_engineer.md`

Legacy/superseded roles may remain for reference, but workflow steps should use only the core roles.
