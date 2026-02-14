# Open Questions Gate (Shared)

Before drafting/updating an artifact or starting work:

1. Check `artifacts/<project_slug>/00_open_questions.md`.
2. If any unchecked item under `## Open` is tagged `[Blocking]` and it blocks the current work, stop and ask the user to answer it in that file.
   - If the file uses `[Affects: ...]`, treat an item as blocking when `Affects` includes the current artifact/step.
3. When the user answers:
   - Incorporate the answer.
   - Move the item to `## Resolved` and mark it `[x]`.
4. If you discover new clarification questions, add them under `## Open`.
   - Use `[Blocking]` only when you truly cannot proceed without the answer.
   - Prefer user-facing language; add technical detail only when unavoidable.
