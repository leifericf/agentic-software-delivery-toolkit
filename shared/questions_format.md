 
# Question Modes (Natural / Choice / Binary / Creative)

When a step asks the user questions, pick the mode that gets new information with the least friction.

Default: Natural.

## Shared Rules (All Modes)
- Ask at most 3 questions per message.
- Keep questions short and phone-scrollable.
- Number questions (1, 2, 3, ...). Restart numbering each message.
- One question per line. Avoid multi-part questions.
- Never ask questions just to placate the user or keep the conversation going.
- If the user can't answer something, treat it as real information.

## When To Use Which

Use Natural when:
- You need context, motivations, or examples.
- The user is already writing in full sentences.
- Forced options would be premature or misleading.

Use Choice when:
- You can offer clear, mutually exclusive branches.
- You want fast, scannable answers that are easy to reference later.

Use Binary when:
- You want a fast clarification (yes/no), or to resolve contradictions.

Use Creative when:
- Progress is stalled (e.g. repeated "not sure", vague answers, circular discussion).
- You want a fresh angle to surface unknown unknowns.

## Choice Mode

### Rules
- Provide 3-5 prefilled choices that are mutually exclusive and cover the main branches (include meaningful extremes when applicable).
- Each choice must be on its own line.
- Each choice must have a letter.
- Each choice should be a short sentence: core value + clarifying hint.
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

2) Pick a project slug.
A) `acme_billing`. Short, explicit, and easy to type.
B) `acme_finance_tools`. Broader; covers billing plus related finance workflows.
C) `billing`. Very short; only use if the repo scope is truly narrow.
D) Write your own answer
E) Can't answer / N/A

## Binary Mode

### Rules
- Ask a yes/no question.
- Accept: Y/y, N/n, DK (don't know), NA (case-insensitive).
- Guardrail: if the goal/success criteria are not yet anchored, prefer 1 Natural anchor question first. Use Binary early mainly for true blockers, contradictions, or non-negotiable constraints.

### Format
Example:

1) Is SSO required? (Y/N/DK/NA)
2) Must this run on-prem? (Y/N/DK/NA)
3) Is there a fixed deadline? (Y/N/DK/NA)

## Natural Mode

### Rules
- Ask broad/open questions to elicit new information.
- Start with one broad question.
- Add a second/third question only when it directly unblocks the next deliverable (artifact, decision, plan).
- Use narrower follow-ups only when the prior answer is incomplete/ambiguous.
- Include a "Can't answer / N/A" escape hatch when a missing answer would block progress.

### Format
Example:

1) Who is the primary user, and what job are they hiring this for?
2) What are the top 1-3 workflows they do today?
3) Any hard constraints? (deadline, budget, on-prem, compliance)

## Creative Mode

### Rules
- Ask exactly 1 question.
- Keep it relevant to the problem at hand.
- Use inversion, analogy, or a constraint twist to unlock new information.
- Light humor is allowed if it helps clarity and stays respectful.
- If the runtime supports web browsing, you may do a brief search (1-3 queries) to find cross-domain analogs and ask a better question.
  - Do not paste links or browsing output; only use it to shape the question.
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
- When it reduces re-asking, reflect back what you heard in <= 280 characters (see `@shared/interaction_protocol.md`).
