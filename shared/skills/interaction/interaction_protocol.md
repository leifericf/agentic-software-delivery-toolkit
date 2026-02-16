 
# Skill: Interaction protocol

Intended human <-> AI loop for all workflow steps.

## Goals
- Natural dialogue; phone-scrollable.
- Pull user knowledge/constraints with minimal friction.
- Ask only what you need; keep forward motion (reduce ambiguity, increase completeness).

## Starting Point (User Guidance)
- Users need not front-load detail.
- Prefer a rough first pass (often 1 paragraph), then pull specifics via targeted questions.
- Loop: rough input -> questions -> answers -> follow-ups -> artifact.
- If initial context is thin: ask 1 broad Natural-mode question about the need/problem.

## User Profile (Optional, Recommended)
If a repo-local profile file exists at `.agentic_profile.md`:

- Treat it as authoritative user preferences for interaction style and defaults.
- Apply it consistently across steps (verbosity, question mode, default-vs-ask bias).
- Do not copy it into project artifacts unless the user explicitly requests it.
- Never store secrets in it.

Interaction preferences are interpreted via `@shared/skills/interaction/interaction_meta_preferences.md`.

## Progressive Narrowing (Default)
Default early shape: Explore -> Define -> Converge.

Explore (broad, low-assumption)
- Anchor value (what makes this useful?).
- Name the core problem.
- Define success (if solved, what changes?).

Define (make it concrete)
- Walk through one real example.
- What was tried already (and why it failed)?
- Constraints + non-negotiables.

Converge (control scope; lock direction)
- Anti-goals (what must not happen / is off-limits?).
- Prioritize (if we solve one thing next, what is it?).
- Confirm a short summary; move to the next deliverable.

Default early Natural prompts
- "What would make this discussion valuable for you?"
- "What's the biggest challenge to solve?"
- "If solved, what does success look like?"
- "Walk me through one real example."
- "What should we avoid / what would be unacceptable?"

## Open Questions Backlog (Mandatory)
Before asking new questions:
- If `artifacts/<project_slug>/open_questions.md` exists, scan `## Open` for unanswered items.
- If the user already answered (in chat or file), incorporate it and move to `## Resolved`.
- Do not re-ask questions that already have a usable answer.

## Chat Loop (Mandatory)
1. Ask a small batch based on the user profile (cap 3).
   - Default: 2 questions if no profile exists.
   - If Interruption tolerance is Minimal, prefer 1 question and proceed with explicit assumptions when possible.
2. Wait for answers.
3. Optional preface for the next batch: one factual recap (<= 280 chars).
   - Skip if the user answered in a clear, structured way and restating adds noise.
4. If answers are ambiguous/contradictory, ask the smallest possible follow-up batch.
5. Repeat until you can produce the deliverable.

Stop conditions:
- If you have enough to proceed, stop asking and move to the next deliverable (artifact, decision log, plan).
- Do not ask questions just to keep the conversation going.

## Question Format
Use `@shared/skills/interaction/questions_format.md`.

Default mode:
- If `.agentic_profile.md` exists, use its default question mode.
- Otherwise: Natural.

Use:
- Choice when options are clear and speed/parseability matters.
- Binary for fast clarifications / contradiction resolution.
- Creative only as a short escape hatch when progress stalls.

Quick selection heuristics:
- Little/no context: Natural (1 broad question).
- Long but ambiguous: Natural for context + Binary for the single biggest uncertainty.
- Contradictions: Binary first.
- Choosing among known branches: Choice.
- Stalled: 1 Creative question, then back to Natural/Binary/Choice.

Mode selection checklist (symptom -> move):
- Contradiction detected -> Binary first.
- Missing constraint blocks next deliverable -> Binary (yes/no) or Choice (branches).
- Many possible branches -> Choice.
- Narrative but no concrete facts -> Natural (1 broad) then Binary.
- Repeated "not sure" -> 1 Creative, then Binary/Choice.

## Red Flags (Detect -> Redirect)
If you detect:
- Repetition without progress -> recap in <= 280 chars; ask a prioritization question (Choice or Natural).
- Vague language ("fast", "easy", "secure") -> ask for 1 concrete example + 1 measurable definition.
- Emotional overwhelm -> ask only 1 question; explicitly offer park/drop.
- Disengagement (very short answers) -> ask desired outcome OR use Binary on the biggest uncertainty.
- Lack of ownership ("they should fix it") -> identify who decides, what constraints are real, what the user can influence.

## User Control (Mode Overrides)
The user may explicitly set how the next turn should behave:
- `Mode: natural` | `Mode: choice` | `Mode: binary` | `Mode: creative`
- Shorthand: `@mode <name>`

Additional optional overrides for the next turn:
- `@batch 1|2|3`
- `@interrupt minimal|balanced|interactive`
- `@depth light|standard|deep`

The agent should follow the override for that turn unless it would block progress.

## Agent Message Style (Chat Mode)
- Natural: output only numbered questions.
- Choice/Binary: output only numbered questions + choices/answer format.
  - Choice: each choice on its own line under the question.
- Optional preface (any mode): `Heard: ...` (one line) and/or 1-3 factual recap bullets; keep under ~6 lines.
- No plans or meta commentary; keep summaries short.
- No praise/flattery; stay neutral and concrete.

## Ask Vs Assume (Mandatory)
Follow the decision policy in `@shared/skills/interaction/interaction_meta_preferences.md`.

Practical rule:
- If a missing answer is not blocking, prefer to proceed with an explicit assumption when the user prefers fewer interruptions.
- When you assume, make assumptions visible and easy to correct (short bullets), then continue.

## Mixed Chat + Artifact Output
Sometimes the fastest path is to include a small amount of chat text alongside an artifact.

- Allowed: a brief recap (1-3 bullets) outside the code block.
- Allowed: a small final question batch (1-3 questions) above the artifact when it avoids an extra round-trip.
- If you include an artifact, keep its full contents in exactly one fenced code block.

## Handling "Can't answer / N/A"
- Treat it as real information.
- If the missing answer is required to proceed, add an unchecked `[Blocking]` item to `artifacts/<project_slug>/open_questions.md` and stop.
- If not required, continue by stating an assumption in the produced artifact and/or adding a row to the decision log if it is a decision.

If the user cannot answer conclusively:
- Offer to park (add to open questions) or drop (explicitly mark non-required).
- Default to parking if the user does not engage.

## Answer Parsing Expectations
- Users may answer partially.
- If a question is unanswered, ask it again only if it blocks progress.
