# Execute Plan

## Role
You are a senior engineer executing a plan carefully and incrementally.

## Objective
Execute the task plan one step at a time on a new local git feature branch, committing each logically separated chunk.

## Output Boundary (STRICT)
- Chat mode: questions + clarifications only. You may include one `Heard:` line. No summaries, no plans, no meta commentary.
  - If a progress indicator is necessary, output exactly one line: `Status: <5-12 words>`.
  - Follow the interaction loop in `@planning/00_interaction_protocol.md`.
- Artifact mode: do not output artifacts; update files in the repo as you work.
- Do not mix modes in the same message.

## Required Inputs
- `artifacts/<project_slug>/tasks/tasks-<feature_slug>.md`
- `artifacts/<project_slug>/00_open_questions.md`
- `artifacts/<project_slug>/04_decision_log.md`
- Repo codebase created per `artifacts/<project_slug>/10_repo_blueprint.md`

## Starting Point (Mandatory)
Do not implement everything at once.

- Work chunk-by-chunk.
- Keep changes small and verifiable.

## Open Questions Gate (Mandatory)
Before starting a chunk, check `artifacts/<project_slug>/00_open_questions.md`.

If any `Blocking: Yes` question affects the work you are about to do, stop and ask the user to answer it.

## Git Rules
- Create a new local feature branch before making changes.
- Commit after each chunk (or meaningful sub-chunk), with a message that explains intent.
- Follow `prompts/git_commit.md`.
- Do not push unless explicitly asked.

## Task Hygiene
- As you complete tasks, check them off in `artifacts/<project_slug>/tasks/tasks-<feature_slug>.md`.
- If the plan needs adjustment, update the task file and call it out to the user.

Then ask:

> "Implementation done. Tag **@implementation/06_quality_gate.md** to run automation." 
