# Regression Refresh — Error Diagnostics and Defect-Only Change Test

## Context
A read-only investigation confirmed:
- Regression refresh independently attempts Zephyr ZQL and Jira Bug JQL for each configured environment, regardless of whether execution results changed.
- Defect-only changes are included in snapshot comparison and should be persisted.
- Snapshot comparison excludes `updatedAt` and `sources`, so timestamp-only changes should not publish.
- Environment failures are isolated; validated changes from other environments remain eligible for Auto-Publish.
- The latest failure displayed only `Refresh returned failure; no verified snapshots changed`. The underlying cause is **unknown** because the relevant collector output was not retained/exposed.

## Objective
Make the **smallest safe change** to expose actionable, sanitized per-environment collection failures, and add a focused regression test for defect-only changes. Do not change refresh semantics, calculations, or Git safety gates.

## Implementation tasks
1. Inspect `scripts/refresh-regression.py`, `scripts/auto-publish-refresh.py`, and relevant Regression tests before editing. Preserve the existing behavior.
2. Improve diagnostics so the Auto-Publish result includes a concise per-environment summary: environment/report key, Zephyr ZQL status, Jira Bug JQL status, snapshot outcome (UPDATED / UNCHANGED / PRESERVED / FAILED), and a safe failure category/reason where known.
3. On failure with zero publishable snapshots, expose the collector's **sanitized** failure summary instead of only the generic message. If the underlying error cannot be classified, state UNKNOWN rather than guessing.
4. Keep logs/output free of raw JQL/ZQL, authorization headers, bearer tokens, passwords, private configuration contents, and sensitive response bodies. Avoid echoing raw exception messages or URLs containing query strings. Use explicit safe error categories such as AUTHENTICATION, AUTHORIZATION, ENDPOINT, PAGINATION, VALIDATION, NETWORK, or UNKNOWN **only when supported by evidence**. Prefer concise messages with no sensitive data.
5. Preserve per-environment failure isolation. A failed environment must preserve its prior snapshot, while other successfully validated changed snapshots remain eligible for Auto-Publish. Do not turn a partial failure into an unconditional global block.
6. Add a deterministic automated test: Zephyr executions remain identical, Jira Bug JQL returns a different defect set, and the snapshot is classified as changed/updated. Ensure the test does not depend on live Jira/Zephyr or private JQL.
7. Add focused tests for sanitized failure reporting, including one failing environment plus one valid changed environment, and zero valid changes with a failure. Verify that no secrets or raw query text appear in diagnostics.
8. Run all relevant Python and Node test suites and `git diff --check`. Report counts and any failures.
9. Update README only if necessary to document the new diagnostics.

## Example desired output (illustrative, NOT observed)
```text
Regression Refresh Summary
HK PoC v2
  ZQL: SUCCESS
  Bug JQL: FAILED
  Reason: AUTHORIZATION (HTTP 403)
  Snapshot: PRESERVED

UK Prod v1
  ZQL: SUCCESS
  Bug JQL: SUCCESS
  Snapshot: UNCHANGED

Auto-Publish: No eligible snapshots to publish
```
Do not invent HTTP status codes or error reasons when evidence is unavailable.

## Constraints
- Do not modify Dashboard UI, metrics, or snapshot schema unless strictly necessary for safe diagnostics.
- Do not change Q426 or Healthcheck behavior.
- Preserve existing snapshot validation, dirty-target protection, explicit staging, tests, branch/remote synchronization, and push-failure handling.
- Do not read out or commit `query-config.local.md` or any credentials.
- Do not execute a live refresh, commit, or push during implementation.
- Keep implementation minimal; avoid new dependencies or broad refactors.

## Deliverables
Report files changed, diagnostic behavior and sanitization approach, tests added and results, and any remaining unknowns. Stop for user review before any live refresh or publication.
