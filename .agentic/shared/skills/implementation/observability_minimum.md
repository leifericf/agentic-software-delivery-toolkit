# Skill: Minimum viable observability

## Purpose
Ensure feature work includes enough observability (logs/metrics and failure-mode awareness) to operate safely, without turning planning into a separate project.

## Applicability
Observability is **Required** when the feature:
- Touches money, auth/access control, permissions, account state, or irreversible actions
- Touches PII/sensitive data (note: never log secrets)
- Can cause data loss/corruption/duplication or user lockout
- Introduces or modifies an integration boundary (external service, queue, database boundary, background worker)
- Adds a new scheduled/job/async flow

Observability may be `N/A` for purely local refactors or trivial UI copy changes. If `N/A`, include one line explaining why.

## Minimum Plan Output (Keep Short)
In the feature plan, capture:
- Failure modes (3-6 bullets): what can break and how it should degrade
- Logs (structured) at boundaries:
  - Event names (intent), level (info/warn/error), and a minimal set of fields
  - Correlation: request id / trace id / job id (whatever the repo uses)
  - Redaction: confirm no secrets/PII are logged
- Signals/metrics (at least one for critical flows):
  - What indicates success vs failure (error rate, latency, retries, queue depth, etc.)

## Execution Expectations
During implementation:
- Implement the planned boundary logs and confirm they are exercised by at least one test or a manual validation step.
- Add the planned signal/metric when required (or explicitly record why it is deferred).
