 
# Interaction Protocol

This document defines the intended "human <-> AI" interaction loop for all workflow steps.

## Goals
- Feel like a natural dialogue.
- Keep messages phone-scrollable.
- Elicit the user's knowledge and constraints with minimal friction.
- Avoid asking more questions than necessary.

## Starting Point (User Guidance)
- The user does not need to specify everything up front.
- Prefer a rough first pass (often a single paragraph) and let the agent pull details via targeted questions.
- The loop is intentional: rough input -> questions -> answers -> follow-ups -> artifact.

## Chat Loop (Mandatory)
1. Ask a small batch of questions (max 10).
2. Wait for the user's answers.
3. If answers are ambiguous or contradictory, ask the smallest possible follow-up batch.
4. Repeat until the step has enough clarity to produce the artifact.

## Question Format
Use `@shared/questions_format.md`.

- Default: Natural mode.
- Use Structured mode when options are clear and speed/parseability matters.

## Agent Message Style (Chat Mode)
- Natural default: output only the numbered questions (choices optional).
- Structured mode: output only the numbered questions + choices.
- Optional preface (both modes):
  - `Heard: <short, concrete restatement>` (one line), and/or
  - a brief recap (1-3 bullets) when it reduces re-asking or confusion.
  - Keep the preface under ~6 lines total.
- Do not add plans or meta commentary.
- Avoid long summaries. If you include a recap, keep it factual and short.

## Mixed Chat + Artifact Output
Sometimes the fastest path is to include a small amount of chat text alongside an artifact.

- Allowed: a brief recap (1-3 bullets) outside the code block.
- Allowed: a small final question batch (1-3 questions) above the artifact when it avoids an extra round-trip.
- If you include an artifact, keep its full contents in exactly one fenced code block.

## Handling "Can't answer / N/A"
- Treat it as real information.
- If the missing answer is required to proceed, create an entry in `artifacts/<project_slug>/00_open_questions.md` and stop.
- If not required, continue by stating an assumption in the produced artifact and/or recording an ADR if it is a decision.

## Answer Parsing Expectations
- Users may answer partially.
- If a question is unanswered, ask it again only if it blocks progress.
