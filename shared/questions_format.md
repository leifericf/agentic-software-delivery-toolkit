 
# Question Format (Structured vs Natural)

When a step asks the user questions, pick one of two modes:

- Structured: multiple-choice, compact, and easy to answer on mobile.
- Natural: conversational, free-form answers, lower ceremony.

Both modes are allowed. Default to Natural when in doubt.

## When To Use Which

Use Natural when:
- The question is open-ended or needs context.
- The user is already writing in full sentences.
- Providing forced options would be awkward, premature, or misleading.
- You want to keep momentum and reduce ceremony.

Use Structured when:
- You can offer clear options (A/B/C...).
- You want fast, scannable answers.
- You want answers that are easy to parse and reference later.

## Shared Rules (Both Modes)
- Ask at most 10 questions per message.
- Keep questions short and phone-scrollable.
- Number questions (1, 2, 3, ...). Restart numbering each message.
- Avoid multi-part questions. If you need multiple inputs, ask multiple questions.
- If the user can't answer something important, treat it as real information.

## Structured Mode

### Rules
- One question per line.
- Provide 3-5 prefilled answer choices.
- Each choice must have a letter.
- Each choice must be a short sentence: core value + clarifying hint.
  - Rationale: single-letter answers can be ambiguous on mobile; the hint makes options self-explanatory.
- Always include two additional lettered choices:
  - Write your own answer
  - Can't answer / N/A

### Format
Example:

1) Primary interface surface?
A) Web. A browser-based UI is the primary surface.
B) Desktop. A native app is the primary surface.
C) CLI. The user mostly interacts via commands.
D) Write your own answer
E) Can't answer / N/A

2) Accessibility target?
A) WCAG 2.2 AA. Target the latest AA guidance.
B) WCAG 2.1 AA. Target AA with broad compatibility.
C) None specified. Capture best-effort basics only.
D) Write your own answer
E) Can't answer / N/A

3) Pick a project slug.
A) `acme_billing`. Short, explicit, and easy to type.
B) `acme_finance_tools`. Broader; covers billing plus related finance workflows.
C) `billing`. Very short; only use if the repo scope is truly narrow.
D) Write your own answer
E) Can't answer / N/A

## How The User Answers
- Respond with compact codes, separated by spaces or newlines.
- Use: `<question_number><choice_letter>`
- If you chose "Write your own answer", use the letter shown for that choice (usually D-F) and append `:<your text>`.
- Optionally, append `:<comment>` to any answer.

Examples:
- `1A 2B`
- `1D:Both web and desktop 2E`
- `5F:Additional context here` (when the "Write your own answer" choice is labeled F)

## Natural Mode

### Rules
- Still number questions.
- Choices are optional. If you include options, keep them short and non-exhaustive.
- Make it clear how the user should respond (free-form is fine).
- Explicitly include a "Can't answer / N/A" escape hatch when a missing answer would block progress.

### Format
Example:

1) Who is the primary user, and what job are they hiring this for?

2) What are the top 1-3 workflows they do today?

3) Any hard constraints? (deadline, budget, on-prem, compliance)

### How The User Answers
- Plain language is fine.
- If helpful, prefix answers with the question number (e.g. `1) ...`, `2) ...`).

## Agent Loop (Chat Mode)
- Ask up to 10 questions at a time.
- After the user answers, ask the next smallest batch.
- If helpful, add a short acknowledgement line and/or a brief recap before the next batch (see `@shared/interaction_protocol.md`).
