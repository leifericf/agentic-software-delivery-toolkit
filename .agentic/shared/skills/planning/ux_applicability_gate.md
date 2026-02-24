# Skill: UX applicability gate

Use when a workflow step may be skipped if there is no user-facing interface.

## Procedure
1. Determine whether any user-facing interface surface is in-scope: Web, Mobile, Desktop, TUI, CLI.
2. If none apply (e.g., pure library, backend-only service, batch job, data pipeline):
   - Do not produce the UX artifact.
   - Add a decision log row documenting the skip:
     - Decision: Skip UX design guide (no user-facing interface)
     - Why: No UI surfaces are in-scope
     - Tradeoff: Less UX guidance if UI is added later; revisit UX
   - In Chat mode, output exactly one line:
     `Status: UX design guide skipped; tag @.agentic/planning/05_create_technical_design.md`
   - Then stop.
