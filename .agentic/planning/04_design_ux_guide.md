
# UX Design Guide

## Role
See `@.agentic/shared/roles/ux_designer.md`.

## Objective
Prevent interface and interaction entropy before it begins.

## Starting Point (Mandatory)
Do not require detailed UI specs up front.

- If the user has references, collect them.
- If not, start from a 1-2 sentence direction and refine via questions.

## Output Boundary (STRICT)
See `@.agentic/shared/skills/gates/output_boundary.md` (Artifact: single `md` fenced block).

## Applicability Gate (Mandatory)
See `@.agentic/shared/skills/planning/ux_applicability_gate.md`.

## Required Inputs
- `.agentic/artifacts/project_meta.md`
- `.agentic/artifacts/problem_description.md`
- `.agentic/artifacts/product_requirements.md`
- `.agentic/artifacts/risk_assumption_review.md`
- `.agentic/artifacts/decision_log.md`
- `.agentic/artifacts/open_questions.md`

## Input Gate (Default)
See `@.agentic/shared/skills/gates/input_gate.md`.

## Open Questions Gate (Mandatory)
See `@.agentic/shared/skills/gates/open_questions_gate.md` (Affects: `ux_design_guide.md`).

## Instructions
First collect visual references: ask for 3-5 references that match the intended look/feel.

Accept: websites/product pages, design system docs, screenshots/images, CLI/TUI tools (name + link/screenshot). Also accept a short textual direction.

Example references:
- https://linear.app
- https://stripe.com

CLI/TUI reference examples:
- `gh` (GitHub CLI)
- `kubectl`
- `lazygit`
- `htop`

Example textual descriptions:
- "Light Nordic design with ample whitespace, muted neutrals, minimal borders"
- "Dark and gloomy with bold red accents, high contrast typography, moody gradients"
- "Warm editorial: off-white paper background, serif headings, generous line height"

If the user cannot provide references, ask them to pick a direction using the format in `@.agentic/shared/skills/interaction/questions_format.md` (e.g. Minimal / Editorial / Playful / Enterprise / Retro / Luxury).

Ask questions about:
- Primary interface surfaces
- Brand personality
- Visual tone
- Density preferences
- Target users
- Accessibility expectations

Also ask about:
- Input modalities: Keyboard-only | Keyboard+Mouse | Touch | Mixed
- Offline/latency constraints: Low | Medium | High

Ask questions using the format in `@.agentic/shared/skills/interaction/questions_format.md`.

Do NOT assume toolkits unless already selected.

## Decision Log Update (Mandatory)
See `@.agentic/shared/skills/artifacts/decision_log_update.md`.

## Output Artifact
Write:
`.agentic/artifacts/ux_design_guide.md`

## Output Format (STRICT)
Write the artifact using this exact Markdown structure and headings, in this order.

Template:

```md
# UX Design Guide: <Project Name>

## Metadata
- Date: YYYY-MM-DD
- Related:
  - PRD: `.agentic/artifacts/product_requirements.md`

## Visual References
- Reference 1: <URL or description>
- Reference 2: <URL or description>
- Reference 3: <URL or description>
- Reference 4: <optional>
- Reference 5: <optional>
- Textual direction: <optional>

## Design Principles
- <principle>

## Interface Surfaces
- Surfaces: Web | Mobile | Desktop | TUI | CLI
- Primary surface: <one>
- Input modalities: Keyboard-only | Keyboard+Mouse | Touch | Mixed

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
- Layout model: Grid/container | Screen-based | Command-driven | Other
- Spacing scale: <e.g. 4, 8, 12, 16, 24, 32>
- Density: Compact | Comfortable | Spacious

## Components
- Screens/views: <key screens + purpose>
- Navigation model: <pattern>
- Data entry: <inputs/forms rules or ->
- Data display: <tables/lists/log output rules or ->
- Feedback: <loading/success/error patterns>
- Confirmations/dialogs: <pattern or ->
- Empty states: <pattern or ->

## CLI/TUI Conventions (If Applicable)
- Command surface: <commands/subcommands or screens>
- Flags/options style: <rules>
- Output formats: Human-readable | JSON | Both
- Errors and exit codes: <rules>
- Help/usage style: <rules>

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

  > “Approve this UX design guide?  
> If yes, tag **@.agentic/planning/05_create_technical_design.md**.”

(Ask this in a separate Chat mode message after the artifact output.)
