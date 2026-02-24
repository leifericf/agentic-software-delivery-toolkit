# Skill: Project artifact bootstrapping

Use when starting a new project and you need to initialize `.agentic/artifacts/`.

## Procedure
1. Create: `.agentic/artifacts/` (if missing).
2. Create: `.agentic/artifacts/project_meta.md` (if missing) with this minimal structure:

```md
# Project Meta

## Identity
- Project Name: <Project Name>

## Ownership
- Owner: <name or role>

## Dates
- Started: YYYY-MM-DD

## Links
- Repository: <optional>
- Docs: <optional>

## Notes
- <optional>
```

3. Create: `.agentic/artifacts/open_questions.md` (if it does not already exist) with this minimal structure:

```md
# Open Questions

## Open

- [ ] [Blocking] [Affects: <artifact_filename>.md] <question> (Answer: TBD)
- [ ] [Affects: <artifact_filename>.md] <question> (Answer: TBD)

## Resolved

- [x] [Affects: <artifact_filename>.md] <question> (Answer: <answer>) (Date: YYYY-MM-DD)
```

Notes:
- Use `[Blocking]` only when you truly cannot proceed without the answer.
- `Affects` should list artifact filenames (e.g. `product_requirements.md`, `technical_design.md`).

4. Create: `.agentic/artifacts/decision_log.md` (if missing) with this minimal structure:

```md
# Decision Log

| Date | Decision | Why | Tradeoff |
| --- | --- | --- | --- |
| YYYY-MM-DD | <decision> | <why> | <tradeoff> |
```
