
# Skill: Functional elicitation

## Purpose
Help the agent capture story requirements in user-facing language before planning or implementation.

This is not a PRD replacement. It is a lightweight gate to prevent avoidable rework.

## Operating Rules
- Prefer functional, observable language.
- Avoid technical design discussion unless it is unavoidable.
- If a technical choice must be made, translate it into a user-visible tradeoff (what changes for the user).
- Ask only what you need. Cap at 1-2 short batches (max 3 questions per batch; respect user batch-size preference if set in `.agentic_profile.md`).

## Question Order (Default)
Use this order when requirements are missing or ambiguous:

1. Problem and intent
2. Success criteria (observable outcomes)
3. User outcomes
   - What the user must be able to do
   - What must never happen
   - Most important edge cases
4. User flow
   - Primary path
   - Alternate paths
   - Current friction points (if improving existing behavior)
5. Business and domain rules
6. Integrations (functional view)
   - External systems involved
   - Data that flows in/out
   - Dependency constraints and failure expectations
7. Prioritization
   - Minimal viable increment (MVI)
   - What must be correct first
   - What can be deferred
8. Constraints (non-timeline)
   - Privacy/security expectations (user/business needs)
   - Regulatory/compliance
   - Operational limitations
9. Delight and quality bar
   - What would exceed expectations
   - What would feel broken or unacceptable

## "Good Enough To Start" Checklist
Before drafting a plan or starting a chunk, confirm you can answer these in plain language:

- Who is the primary user and what are they trying to accomplish?
- What does success look like (observable outcomes)?
- What is the primary user flow (a step narrative)?
- What must never happen?
- What are the key edge cases and expected behavior?
- What business rules apply?
- What integrations exist and what happens when they fail (if applicable)?
- What is the MVI and what is explicitly deferred?

If any item is unknown and blocks correct delivery, add it to `artifacts/<project_slug>/00_open_questions.md` as `[Blocking]` and stop.
