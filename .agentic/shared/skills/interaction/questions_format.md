 
# Skill: Question modes (Natural / Choice / Binary / Creative)

When you need user input, pick the mode that gets new information with the least friction.

Default: Natural.

## Shared Rules (All Modes)
- Ask at most 3 questions per message (and no more than the user's preferred batch size, if set in `.agentic/.agentic_profile.md`).
- Keep questions short and phone-scrollable.
- Number questions (1, 2, 3, ...). Restart numbering each message.
- One question per line. Avoid multi-part questions.
- Never ask questions just to placate the user or keep the conversation going.
- If the user can't answer something, treat it as real information.
- The question text and (for Choice mode) the options must be tailored to the current context; examples in templates are illustrative, not a fixed script.
- If asking about "budget", treat it as non-labor constraints (e.g., infra/tooling spend caps, AI agent usage/credits), not people/time.

## Interactive Form Mode (When Available)
If the runtime supports an interactive question UI, prefer it for **Choice** and **Binary** questions.

- The UI is triggered by using the runtime's structured question mechanism (not by markdown formatting).
- If you only print text, it will stay as plain chat text (no tabs/form view).
- Fall back to the text formats below when the interactive UI/tool is not available.

## When To Use Which

Natural: need context/motivation/examples; user is writing in sentences; options would be premature.

Choice: clear, mutually exclusive branches; you want fast, scannable answers.

Binary: fast clarification (yes/no) or contradiction resolution.

Creative: progress is stalled ("not sure", vagueness, circular loop); you need a fresh angle.

## Choice Mode

### Rules
- Provide 3-5 prefilled choices that are mutually exclusive and cover the main branches (include meaningful extremes when applicable).
- The question must be on its own line.
- Do not put any choices on the same line as the question.
- Each choice must be on its own line under the question it belongs to.
- Each choice must have a letter.
- Each choice should be a short sentence: core value + clarifying hint.
- Always include two additional lettered choices:
  - Write your own answer
  - Can't answer / N/A

### Format
Example:

1) Primary interface surface?
A) Web. Browser UI is primary.
B) Desktop. Native app is primary.
C) CLI. Mostly commands.
D) Write your own answer
E) Can't answer / N/A

## Binary Mode

### Rules
- Ask a yes/no question.
- Accept: Y/y, N/n, DK (don't know), NA (case-insensitive).
- Guardrail: if goals/success criteria are not anchored, ask 1 Natural anchor question first. Use Binary early mainly for blockers, contradictions, non-negotiables.

### Format
Example:

1) Is SSO required? (Y/N/DK/NA)
2) Must this run on-prem? (Y/N/DK/NA)

## Natural Mode

### Rules
- Ask broad/open questions to elicit new information.
- Start with one broad question.
- Add a second/third question only when it directly unblocks the next deliverable (artifact, decision, plan).
- Use narrower follow-ups only when the prior answer is incomplete/ambiguous.
- If a missing answer would block progress, include a "Can't answer / N/A" escape hatch.

### Format
Example:

1) Who is the primary user, and what job are they hiring this for?
2) What are the top 1-3 workflows they do today?
3) Any hard constraints? (infra/tooling spend, AI agent usage limits, on-prem, compliance, security)

## Creative Mode

### Rules
- Ask exactly 1 question.
- Keep it relevant to the problem at hand.
- Use inversion, analogy, or a constraint twist to unlock new information.
- Light humor is allowed if it helps clarity and stays respectful.
- If runtime supports browsing, you may do 1-3 queries for cross-domain analogs.
  - Do not paste links/output; only use it to shape the question.
- After the user answers, return to Natural/Binary/Choice.

### Format
Example:

1) Imagine this fails in the most embarrassing way six months from now. What happened, and what warning sign did we ignore?

## How The User Answers

Choice mode:
- Use: `<question_number><choice_letter>`
- If you chose "Write your own answer", append `:<your text>`.
- Optionally, append `:<comment>` to any answer.

Examples:
- `1A 2B`
- `1D:Both web and desktop 2E`

Binary mode:
- Use: `<question_number><Y|N|DK|NA>`

Examples:
- `1Y 2DK 3NA`

Natural mode:
- Plain language is fine.
- If helpful, prefix answers with the question number (e.g. `1) ...`, `2) ...`).

Parking / dropping (optional):
- If you want to defer a question, answer with: `<question_number>P` (Park for later).
- If you want to skip a question entirely, answer with: `<question_number>D` (Drop).

Examples:
- `2P 3D`

## Agent Loop (Chat Mode)
- Ask up to 3 questions at a time.
- After the user answers, ask the next smallest batch.
- When it reduces re-asking, reflect back what you heard in <= 280 characters (see `@.agentic/shared/skills/interaction/interaction_protocol.md`).
