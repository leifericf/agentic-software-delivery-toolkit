# Prompt: Find UX/UI Issues

## Role
Primary: `@.agentic/shared/roles/ux_designer.md`
Secondary: `@.agentic/shared/roles/quality_engineer.md`

## Objective
- Find UX/UI issues (not bugs).
- Evaluate usability, accessibility, consistency, and interaction friction.
- Assign category, severity, priority, and fix complexity consistently.
- Create and maintain a durable UX/UI issue list artifact separate from the bug list and product backlog.
- Keep the UX/UI issue list as a living document as new findings are discovered.

## Hard Rules
- Do not add UX/UI issues to `.agentic/artifacts/product_backlog.md`. UX/UI issues live in `.agentic/artifacts/ux_ui_issue_list.md`.
- Do not add UX/UI issues to `.agentic/artifacts/bug_list.md`.
- Do not add security vulnerabilities to `.agentic/artifacts/ux_ui_issue_list.md`; route those to `@.agentic/prompts/find_security_issues.md`.
- Do not fix issues in this prompt. This prompt is for discovery + documentation only.
- Do not perform bug or security detection. If you notice a probable bug or security issue, list it only under `Out-of-scope notes` in the artifact and route it to the corresponding prompt.
- Follow repository-level policy (for example `AGENTS.md`) and relevant `@.agentic/` policies when choosing checks and phrasing.

## Output Boundary
- Update (or create) exactly one artifact: `.agentic/artifacts/ux_ui_issue_list.md`.
- Optional: a brief chat recap (3-8 bullets) of what changed.

## Shared List Thread
Keep only genuinely useful alignment with the bug list.

- Recommended shared columns:
  - `severity | priority | category | area | summary`
- Use UX/UI-specific columns where they are more meaningful than bug-oriented fields.

## UX/UI Issue Definition (Working)
A UX/UI issue is an experience-quality problem that harms usability, clarity, or confidence even when the system is technically functional, including:
- Confusing layout or weak visual hierarchy
- Unclear labels, copy, or terminology inconsistencies
- Missing or delayed feedback after user actions
- Poor discoverability of key actions and flows
- Interaction friction (too many steps, unnecessary effort, unclear next action)
- Accessibility barriers (contrast, keyboard flow, focus visibility, semantics, alt text)

## Severity (Shared Scale)
Use exactly one value:

Blocker
- Core UX flow is unusable or inaccessible for intended users; no practical workaround.

Very High
- Severe UX harm in a critical journey; workaround is risky, costly, or unrealistic.

High
- Important journey has significant friction/confusion; workaround exists but is painful.

Normal
- Noticeable UX friction with moderate impact; tasks remain completable.

Minor
- Small usability/polish issue with low practical impact.

## Priority (Shared Scale)
Use exactly one value:

Very High
- Fix immediately; blocks adoption/task success or causes major user harm.

High
- Fix in the next cycle; strong experience impact.

Medium
- Schedule soon; meaningful but not urgent.

Low
- Safe to defer; limited impact.

Very Low
- Backlog polish/cleanup; defer until convenient.

## Fix Complexity (Shared Scale)
Use exactly one value:

Trivial
- Very small, low-risk change; usually a few lines.

Easy
- Straightforward, localized change with clear expected outcome.

Challenging
- Moderate complexity across multiple screens/components or states.

Difficult
- High complexity with broad UX impact, risk, or dependency coordination.

Very Difficult
- Large cross-system redesign or high-uncertainty change.

## Categories
Use exactly one primary category:
- Usability/Information Architecture
- Interaction/Feedback
- Content/Terminology
- Visual Hierarchy/Readability
- Accessibility
- Consistency/Standards
- Discoverability/Wayfinding
- Flow Friction/Efficiency

## Evaluation Frameworks (Cheat Sheet)
Use all three lenses together.

### Nielsen Heuristics
- Visibility of system status
- Match between system and real-world language
- User control and freedom
- Consistency and standards
- Error prevention
- Recognition over recall
- Flexibility and efficiency
- Aesthetic/minimalist design
- Error recovery support
- Help/documentation quality

### WCAG-Oriented Accessibility
- Color contrast and readability
- Keyboard navigation and focus management
- Screen reader compatibility and semantic structure
- Alternative text for meaningful images
- Heading and structure clarity

### Rams Design Principles
- Understandable
- Unobtrusive
- Aesthetic
- Honest
- As little design as possible

## Interface-Type Awareness
1. Detect interface type first.
2. Apply the same principles in context.

Examples:
- Web: navigation clarity, layout hierarchy, click targets, action feedback
- Terminal/CLI: command discoverability, output readability, actionable errors, help discoverability
- Mobile: touch target size, gesture discoverability, constrained-screen prioritization
- Desktop: information density, shortcut discoverability, state visibility

## Procedure (Discovery Loop)
1. Ensure `.agentic/artifacts/ux_ui_issue_list.md` exists. If missing, create it from the template below.
2. Collect UX/UI signals (prefer non-mutating checks first). Use checks and evidence sources that exist in this repo; examples:
   - Manual walkthroughs of core journeys (capture concrete interaction paths)
   - Existing UI/e2e test output and snapshots (if present)
   - Accessibility checks (keyboard-only traversal, focus visibility/order, contrast checks)
   - Existing product copy/help/docs that shape user-facing terminology
3. Review all user-facing surfaces (mandatory): do a repo-wide UX/UI review pass in addition to available checks.
   - Scope: all relevant UI surfaces and interaction layers (web pages/components, CLI/TUI output, mobile/desktop views, onboarding/help/error flows).
   - Method: combine systematic walkthrough + targeted probes.
     - Systematic: traverse entrypoints first, then primary journeys, then secondary/edge journeys, then settings/help/error-recovery paths.
     - Targeted probes: look for unclear labels, inconsistent terms/patterns, weak hierarchy/readability, missing action feedback, weak empty/loading/error states, accessibility barriers, and poor discoverability.
   - Goal: surface evidence-based UX/UI issues with clear user impact and actionable improvements.
4. For each issue found:
   - Duplicate check (mandatory): search for a similar issue by `summary`, same `area`, and/or matching key terms in `reasoning`/`suggested_improvement`.
   - Add a new entry (or update an existing one).
   - Assign Category, Severity, Priority, and Fix Complexity.
   - Keep entries specific and actionable.
   - If validation is missing, set `reasoning` to a concrete `NEEDS_VALIDATION:` request.
5. Keep it living:
   - Deduplicate similar reports.
   - Tighten wording and recommendations as evidence improves.
   - Remove issues from `.agentic/artifacts/ux_ui_issue_list.md` in the same commit that implements the fix.

## Artifact Template: `.agentic/artifacts/ux_ui_issue_list.md`
If the file does not exist, create it with exactly this structure:

```md
| severity | priority | fix_complexity | category | area | summary | reasoning | suggested_improvement |
| --- | --- | --- | --- | --- | --- | --- | --- |

## Out-of-scope notes (probable bugs)
- None
```

## One Row Per UX/UI Issue (Markdown Table)
Each open issue is one table row with:
- `severity`: `Blocker|Very High|High|Normal|Minor`
- `priority`: `Very High|High|Medium|Low|Very Low`
- `fix_complexity`: `Trivial|Easy|Challenging|Difficult|Very Difficult`
- `category`: one of the Categories listed above
- `area`: page/screen/command/component/flow step
- `summary`: concise human-readable title
- `reasoning`: why this harms usability or experience (or `NEEDS_VALIDATION:` request)
- `suggested_improvement`: clear, implementation-ready recommendation

Ordering rule in the file:
- Keep rows sorted by `severity` then `priority` using this order:
  - Severity: `Blocker -> Very High -> High -> Normal -> Minor`
  - Priority: `Very High -> High -> Medium -> Low -> Very Low`
