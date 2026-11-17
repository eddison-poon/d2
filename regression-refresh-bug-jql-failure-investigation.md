# Regression Refresh Failure — Bug JQL Change Investigation

## Objective
Investigate why the latest Regression Test refresh failed after the Bug JQL configuration was updated. Determine whether the refresh incorrectly ignores defect changes when Zephyr execution data is unchanged, or whether a collection/query failure prevented snapshot validation.

## Evidence
- Auto-Publish reported: `Refresh returned failure; no verified snapshots changed`.
- Regression snapshot timestamps remained unchanged.
- Five environments have both ZQL and JQL configured; seven lack configuration.
- The wrapper did not expose the underlying service error. Authentication, endpoint, and pagination problems have not been ruled out.
- No Regression commit or push occurred.

These observations **do not yet prove** that unchanged execution data caused Bug JQL to be skipped.

## Instructions for Copilot
**Read-only investigation. Do not modify files, refresh data, commit, push, reset, or discard changes.**

1. Inspect `scripts/refresh-regression.py`, `scripts/auto-publish-refresh.py`, the Regression collector, and `.github/agents/testing-dashboard-refresh.agent.md`.
2. Determine whether Regression execution data and Jira defect data are independently refreshed and validated.
3. Check whether changes to Outstanding Defects trigger snapshot updates even when Regression execution counts and statuses remain unchanged.
4. Determine whether the refresh skips Jira Bug JQL when Zephyr execution data is unchanged.
5. Inspect available logs and error handling to identify why the latest refresh returned `failure; no verified snapshots changed`. If logs are insufficient, identify exactly what evidence is missing; do not guess.
6. Check whether a failed query in one environment prevents other successfully refreshed environments from being published.
7. Confirm whether collection timestamps alone can trigger unnecessary commits.
8. Identify the exact functions and conditions responsible for the observed behavior, distinguishing confirmed facts from hypotheses.

## Expected behavior
- Refresh Regression execution data using ZQL.
- Refresh Outstanding Defects using the dedicated Bug JQL.
- If either dataset changes, update the corresponding environment snapshot.
- If both datasets are unchanged, report no data changes.
- A failed query must never be reported as unchanged data.
- Preserve existing Git safety checks, verified snapshot protection, and failure isolation.

## Deliverables
Report:
- Confirmed root cause or remaining uncertainty
- Relevant file names, functions, and branching conditions
- Whether Bug JQL is executed when Zephyr results are unchanged
- Whether defect-only changes are persisted and eligible for Auto-Publish
- Smallest recommended fix, without implementing it

**Do not implement changes yet. Wait for user review.**
