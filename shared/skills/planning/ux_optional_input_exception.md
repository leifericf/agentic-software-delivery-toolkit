# Skill: UX optional input exception

Use when a workflow step lists `artifacts/<project_slug>/ux_design_guide.md` as an input, but the project legitimately has no user-facing interface.

## Rule
`artifacts/<project_slug>/ux_design_guide.md` may be missing only if a decision log row in `artifacts/<project_slug>/decision_log.md` documents that UX was intentionally skipped due to no user-facing interface.
