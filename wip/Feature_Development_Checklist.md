# Feature Development Checklist

Use this as a minimal execution checklist.

------------------------------------------------------------------------

## Selection

☐ Backlog item selected\
☐ Scope clarified

------------------------------------------------------------------------

## Requirements

☐ BDD scenarios written\
☐ Acceptance criteria clear

------------------------------------------------------------------------

## Architecture

☐ Architectural fit evaluated\
☐ Backward compatibility decision made\
☐ Integration boundaries identified

------------------------------------------------------------------------

## Observability

☐ Logging requirements defined\
☐ Metrics defined\
☐ No sensitive data in logs

------------------------------------------------------------------------

## Planning

☐ Components identified\
☐ Dependencies mapped\
☐ Vertical slices defined\
☐ Feature flag decision made\
☐ Migration plan defined

------------------------------------------------------------------------

## Testing Strategy

☐ Tier 0 tests defined (unit + fakes + contracts)\
☐ Tier 1 tests defined (container integration)\
☐ Tier 2 sandbox strategy defined

------------------------------------------------------------------------

## Implementation

☐ Tests written first\
☐ Code implemented incrementally\
☐ Logging added\
☐ Metrics added\
☐ Tier 0 + Tier 1 green

------------------------------------------------------------------------

## Data Changes

☐ Up migration created\
☐ Down migration created (if possible)\
☐ Backup/restore plan defined

------------------------------------------------------------------------

## Validation

☐ User-level validation performed\
☐ Bugs fixed\
☐ Sandbox tests executed

------------------------------------------------------------------------

## Review

☐ AI review completed\
☐ Self-review checklist completed\
☐ Technical debt items captured

------------------------------------------------------------------------

## Documentation

☐ Backlog updated\
☐ Changelog updated (if applicable)\
☐ README updated (if needed)

------------------------------------------------------------------------

## Cleanup

☐ Debug code removed\
☐ Temporary flags removed\
☐ Transitional artifacts removed\
☐ `.gitignore` verified

------------------------------------------------------------------------

## Merge

☐ CI green\
☐ Small PR merged\
☐ Feature branch deleted

------------------------------------------------------------------------

## Deploy

☐ Feature flag configured\
☐ Deployment verified\
☐ Logs/metrics confirmed healthy

------------------------------------------------------------------------

System reset to clean baseline.
