# Skill: SemVer Release Decision Gates

## Objective
Prepare the next release (candidate or proper) when the user says they are release-ready.

## Trigger
Use this skill only when the user explicitly requests a new release version.

## Inputs
- `.agentic/artifacts/release_versioning.md`
- Project release manifest/version source (if present)
- Git history since the last release tag

## Mandatory Decision Gates (In Order)

### Gate 1: Release Type (Mandatory, Always Ask First)
Ask the user:
> "Do you want to create a **release candidate** (for staging validation) or a **proper release** (for production readiness)?"

- Pause and wait for the user's answer.
- Never assume or auto-select the release type.

### Gate 2: SemVer Recommendation (Mandatory, Always Ask Second)
Before asking the user to choose a bump type:

1. Run `git log <last-release-tag>..HEAD --oneline` to review changes since the last release.
2. Classify changes against SemVer rules:
   - `major`: incompatible or behavior-changing release contract.
   - `minor`: backward-compatible capability additions.
   - `patch`: backward-compatible fixes and maintenance.
3. Present a short summary and gently suggest a bump type with brief reasoning.
4. Explicitly state that the user makes the final decision.
5. Pause and wait for the user's answer.
6. Never assume or auto-select the bump type.

## Procedure: Release Candidate

Use this path when the user chose "release candidate" in Gate 1.

1. Determine the target version from the user's bump type choice.
2. Determine the RC number:
   - Check tags for `vX.Y.Z-rc.*` to find the next `N`.
   - If no prior RC exists for this target, use `rc.1`.
3. Create git tag: `vX.Y.Z-rc.N`.
4. Do not run release-file bump automation unless the project explicitly requires it for RCs.

### RC Output
- Git tag: `vX.Y.Z-rc.N`
- Deployment target: non-production validation environment(s)

## Procedure: Proper Release

Use this path when the user chose "proper release" in Gate 1.

1. Run the project's release bump workflow for the chosen SemVer type.
2. Verify changed release metadata files (project-specific).
3. Ensure release notes are complete before tagging/publishing.
4. Create git tag: `vX.Y.Z`.

### Proper Release Output
- Git tag: `vX.Y.Z`
- Updated release metadata according to project workflow
- Eligible for production promotion (per project policy)
