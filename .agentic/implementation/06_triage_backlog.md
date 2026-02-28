# Backlog Triage

## Role
See `@.agentic/shared/roles/product_manager.md`.

## Objective
Help the user triage and reprioritize the backlog without hand-editing, keeping it a living document that reflects both upcoming work and what is already in the product.

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/output_boundary.md` (Artifact: single `text` fenced block).

## Required Inputs
- `.agentic/artifacts/product_requirements.md`
- `.agentic/artifacts/decision_log.md`
- `.agentic/artifacts/product_backlog.md`
- `.agentic/artifacts/open_questions.md`

## Open Questions Gate (Mandatory)
See `@.agentic/shared/skills/gates/open_questions_gate.md` (Blockers: any `[Blocking]` item affecting backlog priority or scope).

## Instructions
1. Read `.agentic/artifacts/product_backlog.md`.
2. Ask a short prioritization question batch (max 3) using `@.agentic/shared/skills/interaction/questions_format.md`.
   - Tailor the questions and (if using Choice mode) the options to the *actual* branches implied by this backlog.
   - Use these as themes, not hard-coded questions:
     - Outcome to optimize for (what "better" means right now)
     - Sequencing/prerequisite constraints that should affect ordering (not timelines)
     - Any non-timeline constraints that affect prioritization (e.g., compliance, security, operational limits, infra/tooling spend caps, AI agent usage limits)
   - If you use **Choice mode**, always include "Write your own answer" and "Can't answer / N/A".
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
`.agentic/artifacts/product_backlog.md`

Then ask:

> "Backlog reprioritized. Ready to pick the next feature? Tag **@.agentic/implementation/01_pick_feature.md**."
