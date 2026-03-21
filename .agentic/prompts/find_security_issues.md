# Prompt: Find Security Issues

## Role
Primary: `@.agentic/shared/roles/quality_engineer.md`
Secondary: `@.agentic/shared/roles/software_engineer.md`

## Objective
- Find security issues (not general bugs, not UX/UI issues).
- Evaluate exploitability, exposure, and potential impact.
- Assign category, severity, priority, and fix complexity consistently.
- Create and maintain a durable security issue list artifact separate from the bug list, UX/UI issue list, and product backlog.
- Keep the security issue list as a living document as new findings are discovered.

## Hard Rules
- Do not add security issues to `.agentic/artifacts/product_backlog.md`. Security issues live in `.agentic/artifacts/security_issue_list.md`.
- Do not add security issues to `.agentic/artifacts/bug_list.md` or `.agentic/artifacts/ux_ui_issue_list.md`.
- Do not fix issues in this prompt. This prompt is for discovery + documentation only.
- Prefer evidence-based entries (PoC/repro, logs, traces, config/code references, scanner output). If evidence is missing, explicitly record what is needed.
- Follow repository-level policy (for example `AGENTS.md`) and relevant `@.agentic/` policies when choosing checks and phrasing.
- Stay non-destructive: do not run intrusive or production-impacting actions.

## Deterministic Discovery Protocol (Default)
- Freeze context: include reviewed commit SHA in recap.
- Run discovery in fixed phases:
  1) Baseline security signals (scanner/config/test clues)
  2) Systematic authn/authz and trust-boundary review
  3) Targeted probe queries
  4) Gap-focused second pass (saturation)
- Use the same scan order each run:
  - config/runtime security policy -> routing/middleware/auth -> privileged business flows -> sensitive data paths -> external integrations/background jobs.
- Saturation gate (mandatory): run pass 2 on highest-risk paths (login/session/token handling, authorization gates, data export/query boundaries, webhook/integration inputs, secrets); only stop when pass 2 yields no clear net-new security issues.

## Output Boundary
- Update (or create) exactly one artifact: `.agentic/artifacts/security_issue_list.md`.
- Optional: a brief chat recap (3-8 bullets) of what changed.

## Shared List Thread
Keep only genuinely useful alignment with other issue lists.

- Recommended shared columns:
  - `severity | priority | fix_complexity | category | area | summary`
- Use security-specific columns where they are more meaningful than generic bug fields.

## Security Issue Definition (Working)
A security issue is a weakness that could allow unauthorized access, data exposure, privilege misuse, integrity loss, or abuse of system resources, including:
- Authentication/session weaknesses
- Authorization/access control gaps
- Injection and unsafe input handling
- Secrets and credential exposure
- Insecure transport/storage/crypto practices
- CSRF/CORS/clickjacking and boundary control gaps
- Dependency/supply-chain exposure
- Sensitive data leakage in logs/errors/telemetry

## Severity (Shared Scale)
Use exactly one value:

Blocker
- Active or trivially exploitable issue with catastrophic impact and no practical mitigation.

Very High
- Severe impact with credible exploit path; mitigation/workaround is weak or costly.

High
- Significant impact and realistic exploitability; workaround exists but is painful.

Normal
- Moderate impact or limited exploitability; risk is meaningful but constrained.

Minor
- Low impact and/or low exploitability; defense-in-depth hardening issue.

### Severity Escalators
- Cross-tenant or wrong-account data access/write
- Unauthenticated remote exploit path
- Irreversible data loss/corruption
- Secrets/keys/token leakage
- Legal/compliance exposure

## Priority (Shared Scale)
Use exactly one value:

Very High
- Fix immediately; unacceptable exposure.

High
- Fix in the next cycle; strong risk reduction value.

Medium
- Schedule soon; meaningful risk but not urgent.

Low
- Safe to defer briefly with explicit rationale.

Very Low
- Backlog hardening/cleanup; defer until convenient.

## Fix Complexity (Shared Scale)
Use exactly one value:

Trivial
- Very small, low-risk change; usually a few lines.

Easy
- Straightforward, localized change with clear behavior.

Challenging
- Moderate complexity across multiple files or controls.

Difficult
- High complexity, broad impact, or significant coordination.

Very Difficult
- System-level security redesign or high-uncertainty effort.

## Categories
Use exactly one primary category:
- Authentication/Session
- Authorization/Access Control
- Input Validation/Injection
- Secrets/Credential Management
- Data Protection/Privacy
- Transport/Crypto
- Dependency/Supply Chain
- Security Misconfiguration
- Monitoring/Detection/Response

## Procedure (Discovery Loop)
1. Ensure `.agentic/artifacts/security_issue_list.md` exists. If missing, create it from the template below.
2. Collect security signals (prefer non-mutating checks first). Use checks and evidence sources that exist in this repo; examples:
   - Existing test failures and security-oriented checks (if present)
   - Dependency/security scan output (if available)
   - Config/runtime policy inspection (auth, CORS, headers, secrets handling)
   - Code paths handling authn/authz, external inputs, and sensitive data
3. Review all security-relevant code and configuration (mandatory): do a repo-wide security review pass in addition to available checks.
   - Scope: auth/session, policy gates, data access boundaries, external integrations, input handling, secrets/config, logging/error handling.
   - Method: combine systematic walkthrough + targeted probes.
     - Systematic: traverse entrypoints first, then privileged workflows, then sensitive data paths, then integrations/background jobs.
     - Targeted probes: look for missing authorization checks, trust-boundary violations, unsafe parsing/eval, insecure defaults, weak token/session handling, plaintext secrets, and overexposed data.
   - Goal: surface evidence-based, testable security findings with clear impact and mitigation direction.
4. Run pass-2 saturation (mandatory):
    - Re-check threat hotspots: auth/session lifecycle, IP/client identity trust, cross-tenant/account scoping, secret defaults, and logging/PII leakage.
    - Re-check open security rows for adjacent variants.
    - If pass 2 finds net-new issues, include them and mark that saturation produced net-new findings in recap.
5. For each issue found:
   - Duplicate check (mandatory): search for a similar issue by `summary`, same `area`, and/or matching key terms in `threat_scenario`/`evidence`.
   - Add a new entry (or update an existing one).
   - Assign Category, Severity, Priority, and Fix Complexity.
   - Keep entries specific and actionable.
   - If evidence is missing, set `evidence` to a concrete `NEEDS_EVIDENCE:` request.
6. Keep it living:
   - Deduplicate similar reports.
   - Tighten PoC/evidence as you learn more.
   - Remove issues from `.agentic/artifacts/security_issue_list.md` in the same commit that implements the fix (see `@.agentic/prompts/fix_issues_by_type.md`).

## Required Recap (when chat recap is provided)
Include:
- commit SHA reviewed
- baseline security checks/scans used
- threat surfaces covered
- whether pass-2 saturation found net-new security issues
- count of rows added vs updated

## Artifact Template: `.agentic/artifacts/security_issue_list.md`
If the file does not exist, create it with exactly this structure:

```md
| severity | priority | fix_complexity | category | area | summary | threat_scenario | evidence | suggested_mitigation |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
```

## One Row Per Security Issue (Markdown Table)
Each open issue is one table row with:
- `severity`: `Blocker|Very High|High|Normal|Minor`
- `priority`: `Very High|High|Medium|Low|Very Low`
- `fix_complexity`: `Trivial|Easy|Challenging|Difficult|Very Difficult`
- `category`: one of the Categories listed above
- `area`: short subsystem/page/module hint
- `summary`: short human-readable title
- `threat_scenario`: concise attacker path or abuse scenario
- `evidence`: proof signal, code/config references, scanner output, or `NEEDS_EVIDENCE:` request
- `suggested_mitigation`: clear, implementation-ready mitigation guidance

Ordering rule in the file:
- Keep rows sorted by `severity` then `priority` using this order:
  - Severity: `Blocker -> Very High -> High -> Normal -> Minor`
  - Priority: `Very High -> High -> Medium -> Low -> Very Low`
