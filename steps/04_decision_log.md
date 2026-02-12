
# Decision Log

## Role
You are a technical historian.

## Objective
Capture WHY decisions are made so future agents do not undo them.

## Output Boundary (STRICT)
- Chat mode: questions + clarifications only. No summaries, no plans, no meta commentary.
  - If a progress indicator is necessary, output exactly one line: `Status: <5-12 words>`.
- Artifact mode: output exactly one fenced code block containing the full artifact file contents, and nothing else.
  - Use `md` fences for this step.
- Do not mix modes in the same message.

## Artifact Behavior
This is an append-only, living document.

It is created in this step and then updated as decisions are made in later steps.

Do not rewrite prior entries except to correct factual errors.

Use an Architecture Decision Record (ADR) structure for each entry, and keep all ADRs in this one file in chronological order.

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/02_product_requirements.md`
- `artifacts/<project_slug>/03_risk_assumption_review.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Mandatory)
If any required input does not exist, tell the user to run the missing step(s) first to generate it, then stop.

## Open Questions Gate (Mandatory)
Before writing ADRs, check `artifacts/<project_slug>/00_open_questions.md`.

If there is any question under `## Open` with `Blocking: Yes` AND `Affects` includes `artifacts/<project_slug>/04_decision_log.md`, stop and tell the user to answer those question(s) in `artifacts/<project_slug>/00_open_questions.md`.

When the user answers, incorporate the answers into ADR(s) and move the question(s) from `## Open` to `## Resolved`.

## Instructions
1. Review all prior artifacts.
2. Extract decisions already made.
3. Ask if any major decisions remain unresolved.
4. Use multiple-choice to finalize them.

## Output Artifact
Produce:

**Decision Log**

Write to:

`artifacts/<project_slug>/04_decision_log.md`

File format (STRICT):

1. The first line must be exactly: `# Decision Log (ADRs)`
2. The second section must be: `## Index` (chronological list).
3. When you add an ADR, also add a single index line under `## Index`.
4. Index line format: `- ADR-###: <Title> (<Status>, YYYY-MM-DD)`
5. Then ADR entries in chronological order.
6. Each ADR is a single section starting with `## ADR-###: <Title>`.
7. ADR IDs are sequential starting at `ADR-001`.
8. Never reorder ADRs.
9. If a decision changes, create a new ADR that supersedes the old one (do not edit the old ADR).

ADR template (copy/paste per entry):

```md
## ADR-###: <Title>
- Status: Proposed | Accepted | Superseded
- Date: YYYY-MM-DD
- Owners: <optional>
- Supersedes: ADR-### | <omit>

### Context
<What problem are we solving? What constraints matter?>

### Decision
<What did we decide?>

### Consequences
<What changes? What tradeoffs are we accepting?>

### Alternatives Considered
<What else did we consider and why not?>

### References
<Optional links to artifacts, docs, tickets>
```

Then ask:

> “Are decisions captured correctly?  
> If yes, tag **@steps/05_architecture_data_model.md**.”

(Ask this in a separate Chat mode message after the artifact output.)
