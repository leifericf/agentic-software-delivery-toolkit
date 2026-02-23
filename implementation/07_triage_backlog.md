# Backlog Triage

## Role
See `@shared/roles/product_manager.md`.

## Objective
Help the user triage and reprioritize the backlog without hand-editing, keeping it a living document that reflects both upcoming work and what is already in the product.

## Output Boundary (STRICT)
See `@shared/skills/gates/output_boundary.md` (Artifact: single `text` fenced block).

## Required Inputs
- `artifacts/<project_slug>/product_requirements.md`
- `artifacts/<project_slug>/decision_log.md`
- `artifacts/<project_slug>/product_backlog.md`
- `artifacts/<project_slug>/open_questions.md`

## Open Questions Gate (Mandatory)
See `@shared/skills/gates/open_questions_gate.md` (Blockers: any `[Blocking]` item affecting backlog priority or scope).

## Instructions
1. Read `artifacts/<project_slug>/product_backlog.md`.
2. Ask a short prioritization question batch using `@shared/skills/interaction/questions_format.md`:
   - What outcome matters most right now?
   - Any deadlines or sequencing constraints?
   - Anything intentionally deferred?
3. Triage and rewrite the backlog so it stays clean and actionable:
   - Keep these top-level buckets (required, in this order):
     - `Now / Next`
     - `Later`
     - `Inbox (untriaged)`
     - `In product (shipped)`
   - Ensure every item appears in exactly one bucket.
   - Promote a small number of inbox items into `Now / Next` or `Later` if they are clear.
   - Rewrite unclear titles into plain, user-facing language.
   - Keep `Now / Next` intentionally short and ordered.
   - `In product (shipped)` is plain capability names only (no dates/versions/metadata).

## Output Format (STRICT)
- Output exactly one markdown list inside a single fenced `text` block.
- No prose before/after the list.

Write:
`artifacts/<project_slug>/product_backlog.md`

Then ask:

> "Backlog reprioritized. Ready to pick the next feature? Tag **@implementation/01_pick_feature.md**."
