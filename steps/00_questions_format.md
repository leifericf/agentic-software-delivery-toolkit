 
# Question/Answer Format

Use this format whenever a step asks the user questions.

## Rules (Mandatory)
- Ask at most 10 questions per message.
- One question per line. Keep it as short as possible.
- Each question must be numbered (1, 2, 3, ...). Restart numbering each message.
- Provide 3-5 prefilled answer choices.
- Each choice must have a letter.
- Always include two additional lettered choices:
  - Write your own answer
  - Can't answer / N/A

## Format
Example:

1) Primary interface surface?
A) Web
B) Desktop
C) CLI
D) Write your own answer
E) Can't answer / N/A

2) Accessibility target?
A) WCAG 2.2 AA
B) WCAG 2.1 AA
C) None specified
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

## Additional Guidance
- Avoid multi-select questions. If you need multiple inputs, ask multiple questions.

## Agent Loop (Chat Mode)
- Ask up to 10 questions at a time.
- After the user answers, ask the next smallest batch.
- If helpful, add a single acknowledgement line before the next batch (see `@steps/00_interaction_protocol.md`).
