# Skill: Project artifact bootstrapping

Use when starting a new project and you need to initialize `artifacts/<project_slug>/`.

## Procedure
1. Ensure `project_slug` is locked (see `@shared/skills/planning/project_slug.md`).
2. Create: `artifacts/<project_slug>/`
3. Create: `artifacts/<project_slug>/project_meta.md` with this minimal structure:

```md
# Project Meta

## Identity
- Project Name: <Project Name>
- Project Slug: <project_slug>

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

4. Create: `artifacts/<project_slug>/open_questions.md` (if it does not already exist) with this minimal structure:

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

5. Create: `artifacts/<project_slug>/decision_log.md` with this minimal structure:

```md
# Decision Log

| Date | Decision | Why | Tradeoff |
| --- | --- | --- | --- |
| YYYY-MM-DD | <decision> | <why> | <tradeoff> |
```
