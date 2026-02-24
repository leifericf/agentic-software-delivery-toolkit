# Skill: Output boundary

Applies to workflow step templates unless they explicitly override it.

## Chat mode
- Output only questions + clarifications.
- Optional preface: one `Heard:` line and/or 1-3 short recap bullets.
- No plans or meta commentary. Avoid long summaries.
- If needed: output exactly one line: `Status: <5-12 words>`.
- Follow `@.agentic/shared/skills/interaction/interaction_protocol.md`.

## Artifact mode
- Output exactly one fenced code block containing the full artifact file contents.
- Fence language must match the step (`md` or `text`).

## Mixed output
Allowed only when it reduces friction.

- Allowed outside the code block: a brief recap (1-3 bullets).
- Allowed above the code block: a final question batch (1-3 questions).
- Keep the artifact contents in exactly one fenced code block.

## No-artifact steps
Some steps produce no artifact and/or update repo files directly. Those steps must state the override and follow it.
