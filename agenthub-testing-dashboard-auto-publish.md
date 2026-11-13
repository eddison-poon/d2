# Agent Hub Testing Dashboard — Auto-Publish Implementation

Implement automatic Git commit and push after successful dashboard refresh.

## Supported Commands

- Refresh all Q426 workstreams
- Refresh all Regression Test environments
- Refresh all Healthcheck environments

## Requirements

1. Preserve all existing refresh logic, validation, snapshot protection, and dashboard functionality.
2. At the beginning of each refresh, record Git status and identify any pre-existing changes.
3. Run the existing refresh workflow and relevant tests.
4. Identify exactly which report snapshot files were successfully updated during this execution.
5. Stage only those verified snapshot files. Never use `git add .` or `git add -A`.
6. Never stage local JQL/ZQL configuration, credentials, tokens, unrelated source code, README files, or tests.
7. Before committing, verify:
   - Current branch is `main`.
   - No unrelated files are staged.
   - Target snapshots had no pre-existing uncommitted changes.
   - All required validation and tests passed.
   - Remote `origin/main` is synchronized with local HEAD, using a fresh remote check.
8. If some environments fail validation, preserve their previous snapshots and publish only successfully validated updates.
9. If no verified snapshots changed, skip commit and push.
10. Automatically create a descriptive commit message and push to `origin/main`, without requesting additional confirmation.
11. Never force push, reset, stash, or automatically resolve Git conflicts.
12. If a safety check fails, stop publishing and preserve local changes.
13. If push fails, preserve the local commit and report the failure.
14. Implement a reusable publishing workflow and integrate it into `.github/agents/testing-dashboard-refresh.agent.md`.
15. Add automated tests for successful publishing, partial refresh, no changes, unrelated modifications, pre-existing snapshot modifications, remote divergence, and push failure.

## Implementation Constraints

- Windows PowerShell compatible.
- Lightweight implementation.
- No new dependencies unless essential.
- Do not modify the Dashboard UI.
- Do not change existing Pass Rate calculations.
- Do not commit or push during this implementation task.

## Deliverables

Report:
- Files changed
- Implementation approach
- Tests executed and results
- Example successful Auto-Publish output
- Example blocked Auto-Publish output

After implementation, wait for the user to run a real refresh command to verify Auto-Publish end to end.
