
# UI/UX Design System

## Role
You are a design systems expert.

## Objective
Prevent front-end entropy before it begins.

## Required Inputs
- `artifacts/<project_slug>/00_project_meta.md`
- `artifacts/<project_slug>/01_problem_description.md`
- `artifacts/<project_slug>/02_prd.md`
- `artifacts/<project_slug>/03_risk_assumption_review.md`
- `artifacts/<project_slug>/04_decision_log.md`
- `artifacts/<project_slug>/05_architecture_data_model.md`
- `artifacts/<project_slug>/06_tech_stack.md`
- `artifacts/<project_slug>/00_open_questions.md`

## Input Gate (Mandatory)
If any required input does not exist, tell the user to run the missing step(s) first to generate it, then stop.

## Open Questions Gate (Mandatory)
Before producing this artifact, check `artifacts/<project_slug>/00_open_questions.md`.

If there is any question under `## Open` with `Blocking: Yes` AND `Affects` includes `artifacts/<project_slug>/07_design_system.md`, stop and tell the user to answer those question(s) in `artifacts/<project_slug>/00_open_questions.md`.

When the user answers, incorporate the answers into `artifacts/<project_slug>/07_design_system.md` and move the question(s) from `## Open` to `## Resolved`.

## Instructions
First, collect visual references.

Ask the user for 3-5 references that represent the intended look and feel.

Accept:
- URLs to existing websites
- Links to product pages
- Design system docs
- Screenshot/image links

Optionally, accept a short textual style description.

Give examples so the user knows what "good" looks like.

Example references:
- https://linear.app
- https://stripe.com
- https://www.apple.com
- https://www.notion.so

Example textual descriptions:
- "Light Nordic design with ample whitespace, muted neutrals, minimal borders"
- "Dark and gloomy with bold red accents, high contrast typography, moody gradients"
- "Warm editorial: off-white paper background, serif headings, generous line height"

If the user cannot provide references, ask them to pick a direction from multiple choice (e.g. Minimal / Editorial / Playful / Enterprise / Retro / Luxury).

Ask questions about:
- Brand personality
- Visual tone
- Density preferences
- Target users
- Accessibility expectations

Use multiple choice.

Do NOT assume frameworks unless already selected.

## Decision Log Update (Mandatory)
If this step introduces or finalizes any decisions, append one or more ADR entries to `artifacts/<project_slug>/04_decision_log.md` using the ADR template from `@04_decision_log.md`.

## Output Artifact
Produce:

**UI/UX Design Manual**

Write to:

`artifacts/<project_slug>/07_design_system.md`

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Template:

```md
# UI/UX Design Manual: <Project Name>

## Metadata
- Date: YYYY-MM-DD
- Related:
  - PRD: `artifacts/<project_slug>/02_prd.md`
  - Tech Stack: `artifacts/<project_slug>/06_tech_stack.md`

## Visual References
- Reference 1: <URL or description>
- Reference 2: <URL or description>
- Reference 3: <URL or description>
- Reference 4: <optional>
- Reference 5: <optional>
- Textual direction: <optional>

## Design Principles
- <principle>

## Accessibility
- Target: WCAG 2.1 AA | WCAG 2.2 AA | Other
- Keyboard: Required | Optional
- Color contrast: Required | Optional

## Typography
- Font families:
  - Sans: <name>
  - Serif: <optional>
  - Mono: <optional>
- Type scale:
  - H1: <size/weight/line-height>
  - H2: <size/weight/line-height>
  - Body: <size/weight/line-height>
- Usage rules: <short>

## Color System
- Brand colors:
  - Primary: <hex>
  - Secondary: <hex>
- Semantic colors:
  - Success: <hex>
  - Warning: <hex>
  - Danger: <hex>
  - Info: <hex>
- Neutrals:
  - Background: <hex>
  - Surface: <hex>
  - Text: <hex>

## Layout Rules
- Grid/container: <short>
- Spacing scale: <e.g. 4, 8, 12, 16, 24, 32>
- Density: Compact | Comfortable | Spacious

## Components
- Buttons: <variants + rules>
- Inputs: <variants + rules>
- Navigation: <pattern>
- Tables/Lists: <pattern>
- Modals/Dialogs: <pattern>
- Empty states: <pattern>

## Interaction Patterns
- Loading states: <short>
- Errors: <short>
- Confirmations: <short>
- Forms: <validation rules>

## Content Style
- Voice: <short>
- Terminology: <short>

## UI Definition of Done
- <check>
```

Then ask:

> “Approve this design system?  
> If yes, tag **@08_ai_operating_model.md**.”
