# Decision Log Update (Shared)

If this step introduces or finalizes decisions:

- Append one or more rows to `artifacts/<project_slug>/00_decision_log.md` using this table format:

```md
# Decision Log

| Date | Decision | Why | Tradeoff |
| --- | --- | --- | --- |
| YYYY-MM-DD | <decision> | <why> | <tradeoff> |
```
- Do not rewrite prior rows except to correct factual errors.
- If a decision changes, append a new row that references the earlier decision.
