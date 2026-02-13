 
# Interaction Protocol

This document defines the intended "human <-> AI" interaction loop for all workflow steps.

## Goals
- Feel like a natural dialogue.
- Keep messages phone-scrollable.
- Elicit the user's knowledge and constraints with minimal friction.
- Avoid asking more questions than necessary.
- Keep the conversation moving forward (reduce ambiguity, increase completeness).

## Starting Point (User Guidance)
- The user does not need to specify everything up front.
- Prefer a rough first pass (often a single paragraph) and let the agent pull details via targeted questions.
- The loop is intentional: rough input -> questions -> answers -> follow-ups -> artifact.

If the user provides little or no initial context, ask 1 broad Natural-mode question about the need/problem they want to solve.

## Progressive Narrowing (Default)
Default early-planning shape: Explore -> Define -> Converge.

Explore (broad, low-assumption):
- Anchor value: what would make this conversation useful?
- Identify the core problem/challenge.
- Define success (future-focused): if solved, what changes?

Define (make it concrete):
- Ask for a real example or walkthrough of "one instance" of the workflow.
- Ask what they've already tried.
- Identify constraints and non-negotiables.

Converge (control scope and lock direction):
- Ask anti-goals: what should NOT happen, what's off the table, what's unacceptable?
- Ask prioritization: if we can only solve one thing next, what is it?
- Confirm a short summary and proceed to the next deliverable.

Default early-stage prompts (Natural):
- "What would make this discussion valuable for you?"
- "What's the biggest challenge you want to solve?"
- "If this were solved, what would success look like?"
- "Walk me through one real example of this happening."
- "What have you already tried, and why didn't it work?"
- "What should we avoid / what would be an unacceptable solution?"

## Open Questions Backlog (Mandatory)
Before asking any new questions:
- If `artifacts/<project_slug>/00_open_questions.md` exists, scan `## Open` for unanswered items.
- If the user already answered something (in chat or pasted into the file), incorporate it and move it to `## Resolved`.
- Do not re-ask questions that already have a usable answer.

## Chat Loop (Mandatory)
1. Ask a small batch of questions (max 3).
2. Wait for the user's answers.
3. Reflect back what you heard in one short, factual paragraph (<= 280 characters) as the optional preface to the next question batch.
   - Exception: you can skip this if the user answered in a highly structured way (e.g. numbered answers with no ambiguity) and repeating it would add noise.
4. If answers are ambiguous or contradictory, ask the smallest possible follow-up batch.
5. Repeat until the step has enough clarity to produce the artifact.

Stop conditions:
- If you have enough information to proceed, stop asking questions and move to the next deliverable (artifact, decision log, plan).
- Do not keep asking questions "just to keep the conversation going".

## Question Format
Use `@shared/questions_format.md`.

Default mode: Natural.

Use:
- Choice mode when options are clear and speed/parseability matters.
- Binary mode for fast clarifications and contradiction resolution.
- Creative mode only as a short escape hatch when the user is stuck.

Quick selection heuristics:
- If the user provides little/no context: Natural (one broad question).
- If the user input is long but still ambiguous: Natural for context + Binary for the single biggest uncertainty.
- If there are contradictions/inconsistencies: Binary to resolve before continuing.
- If the decision is choosing among known branches: Choice.
- If progress stalls: one Creative question, then return to Natural/Binary/Choice.

Mode selection checklist (symptom -> move):
- Contradiction detected -> Binary to resolve the contradiction first.
- Missing constraint blocks the next deliverable -> Binary (if yes/no) or Choice (if branches).
- Many possible solution branches -> Choice to pick the path.
- User provides a lot of narrative but no concrete facts -> Natural (one broad question) then Binary.
- User repeatedly answers "not sure" -> one Creative question, then Binary/Choice.

## Red Flags (Detect -> Redirect)
If you detect:
- Repetition without progress -> summarize in <= 280 chars, then ask a prioritization question (Choice or Natural).
- Vague language ("fast", "easy", "secure") -> ask for one concrete example and one measurable definition.
- Emotional overwhelm -> ask only 1 question; offer park/drop explicitly.
- Disengagement (very short answers) -> ask what outcome they want from the conversation OR use Binary for the single biggest uncertainty.
- Lack of ownership ("they should fix it") -> identify who decides, what constraints are real, and what the user can influence.

## User Control (Mode Overrides)
The user may explicitly set how the next turn should behave:
- `Mode: natural` | `Mode: choice` | `Mode: binary` | `Mode: creative`
- Shorthand: `@mode <name>`

The agent should follow the override for that turn unless it would block progress.

## Agent Message Style (Chat Mode)
- Natural mode: output only the numbered questions (choices optional).
- Choice/Binary mode: output only the numbered questions + choices/answer format.
  - In Choice mode, list each choice on its own line under its question.
- Optional preface (both modes):
  - `Heard: <short, concrete restatement>` (one line), and/or
  - a brief recap (1-3 bullets) when it reduces re-asking or confusion.
  - Keep the preface under ~6 lines total.
- Do not add plans or meta commentary.
- Avoid long summaries. If you include a recap, keep it factual and short.
- Do not praise, flatter, or perform "encouragement". Stay neutral and concrete.

## Mixed Chat + Artifact Output
Sometimes the fastest path is to include a small amount of chat text alongside an artifact.

- Allowed: a brief recap (1-3 bullets) outside the code block.
- Allowed: a small final question batch (1-3 questions) above the artifact when it avoids an extra round-trip.
- If you include an artifact, keep its full contents in exactly one fenced code block.

## Handling "Can't answer / N/A"
- Treat it as real information.
- If the missing answer is required to proceed, add an unchecked `[Blocking]` item to `artifacts/<project_slug>/00_open_questions.md` and stop.
- If not required, continue by stating an assumption in the produced artifact and/or adding a row to the decision log if it is a decision.

If the user cannot answer conclusively:
- Offer to park the question (add it to open questions) or drop it (explicitly mark it as non-required).
- Default to parking if the user does not engage.

## Answer Parsing Expectations
- Users may answer partially.
- If a question is unanswered, ask it again only if it blocks progress.
