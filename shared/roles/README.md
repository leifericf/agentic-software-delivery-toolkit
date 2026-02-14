# Shared Role Definitions

These files define reusable agent roles used across workflow steps and standalone prompts.

Workflow steps should keep their `## Role` section lean and reference one of these files instead.

Convention:
- Each role file is a short, expandable definition.
- Workflow steps reference roles via: `See @shared/roles/<role_file>.md`.
