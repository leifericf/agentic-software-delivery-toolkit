
# Create Technical Design

## Role
See `@shared/roles/solution_architect.md`.

## Objective
Produce one durable technical design artifact that implementation can follow without improvising architecture, stack, or repo conventions.

This step consolidates architecture/data model, tech stack selection, and lightweight repo/CI conventions.

## Starting Point (Mandatory)
Do not require a fully specified design up front.

- Start from constraints and desired shape.
- Ask only what is needed to avoid expensive wrong assumptions.
- Prefer simplicity and a small number of moving parts.

## Output Boundary (STRICT)
See `@shared/output_boundary.md` (Artifact: single `md` fenced block).

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/03_risk_assumption_review.md`
- `artifacts/<project_slug>/00_decision_log.md`
- `artifacts/<project_slug>/04_ux_design_guide.md` (if applicable; see `@planning/04_design_ux_guide.md`)
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Default)
See `@shared/input_gate.md`.

Exception:
- `artifacts/<project_slug>/04_ux_design_guide.md` may be missing only if a decision log row in `artifacts/<project_slug>/00_decision_log.md` documents that UX was intentionally skipped due to no user-facing interface.

## Open Questions Gate (Mandatory)
See `@shared/open_questions_gate.md` (Affects: `05_technical_design.md`).

## Architectural Philosophy
- Prefer simplicity.
- Avoid premature infrastructure.
- Optimize for change.
- Minimize moving parts.
- Avoid trend-driven choices.

## Instructions
1. Review all inputs.
2. Ask (via `@shared/questions_format.md`) only the smallest set of clarifications needed to lock:
   - System boundaries and key flows
   - Data durability, integrity, and retention
   - External integrations and failure behavior
   - Operational posture (hosting, environments, deployment frequency)
   - Team constraints (language familiarity, operational tolerance)
   - Repo conventions required for implementation (commands + CI outline)
3. When you introduce or finalize decisions, append row(s) per `@shared/decision_log_update.md`.

## Decision Log Update (Mandatory)
See `@shared/decision_log_update.md`.

## Output Artifact
Write:
`artifacts/<project_slug>/05_technical_design.md`

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

```md
# Technical Design: <Project Name>

## Metadata
- Date: YYYY-MM-DD
- Related:
  - PRD: `artifacts/<project_slug>/02_product_requirements.md`
  - Risk review: `artifacts/<project_slug>/03_risk_assumption_review.md`
  - Decision log: `artifacts/<project_slug>/00_decision_log.md`
  - UX guide: `artifacts/<project_slug>/04_ux_design_guide.md` (if applicable)
  - Open questions: `artifacts/<project_slug>/00_open_questions.md`

## System Shape
<1-2 paragraphs describing the overall shape>

## Domain Boundaries
- <domain>
  - Responsibilities: <short>
  - Owns Data: <yes/no + what>
  - External Interfaces: <APIs/events/files/manual>

## Components
- <component name>
  - Type: Service | Web App | Worker | Job | Library | External
  - Responsibilities: <short>
  - Depends On: <list or ->
  - Data Stores: <list or ->

## Key Flows
- <flow name>
  - Trigger: <what starts it>
  - Steps:
    1. <step>
    2. <step>
  - Data touched: <list>
  - Failure handling: <short>

## Data Model
- <entity name>
  - Purpose: <short>
  - Key fields: <comma-separated>
  - Relationships: <relationship notes>
  - Retention: <short>

## Integrity Strategy
- Invariants: <bullet list>
- Idempotency: <short>
- Concurrency: <short>

## Audit and Compliance
- Audit needs: <short>
- PII handling: <short>

## Integrations
- <system>
  - Direction: Inbound | Outbound
  - Interface: API | Webhook | File | Manual
  - Notes: <short>

## Technology Stack

### Backend
- Language/Runtime: <choice>
- Web toolkit: <choice>
- API style: REST | GraphQL | RPC
- Background jobs: <choice>

### Frontend (If Applicable)
- Approach: SPA | MPA | SSR | Static
- UI toolkit: <choice>
- Styling: <choice>

### Data
- Primary database: <choice>
- Migrations: <choice>
- Search/indexing: <choice or ->
- Caching: <choice or ->

### Infrastructure Posture
- Hosting: <choice>
- Environments: Local | Dev | Staging | Prod
- Deployment style: <choice>

### Observability
- Logging: <choice>
- Metrics: <choice>
- Tracing: <choice or ->

### Testing Posture
- Unit: <short>
- Integration: <short>
- E2E: <short>

## Repository & Delivery Conventions

### Repository Structure (Sketch)
```text
<tree>
```

### Command Surface
- `dev`: <what it does>
- `test`: <what it does>
- `lint`: <what it does>
- `build`: <what it does>
- `format`: <optional>

### CI Outline
- Lint: <command>
- Typecheck: <command>
- Test: <command>
- Build: <command>
- Security checks: <optional>

### Environment Model
- Configuration sources: <.env/secret manager/etc>
- Required environment variables:
  - `VAR_NAME`: <purpose>

## Evolution Strategy
- Versioning approach: <short>
- Migration approach: <short>

## Known Tradeoffs
- <tradeoff>
  - Why chosen: <short>
  - Cost: <short>
```

Then ask:

> “Is the technical design acceptable and ready to use?  
> If yes, tag **@planning/06_create_product_backlog.md**.”

(Ask this in a separate Chat mode message after the artifact output.)
