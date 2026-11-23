# Q426 — Correct Outstanding Defects Status Filtering (Level 2)

## Background
The Q426 Bug JQL is intentionally correct and retrieves bugs across **all statuses**. However, Q426 Level 2 currently counts bugs in terminal statuses such as `Closed` and `Rejected` as Outstanding Defects. This is a dashboard calculation/filtering defect, **not a JQL defect**.

## Objective
Fix Q426 Outstanding Defects counting and display using a consistent, case-insensitive Jira Bug status rule. Preserve the full Bug JQL result set in the collection/snapshot where the current architecture permits it.

## Approved Bug Status Mapping
| Jira Bug Status | Outstanding? |
| --- | --- |
| Open | Yes |
| To Do | Yes |
| In Progress | Yes |
| Reopened | Yes |
| Resolved | No |
| Closed | No |
| Rejected | No |
| Done | No |

Implementation rule: normalize status with trim and case-insensitive comparison. The completed/non-outstanding set is `Resolved`, `Closed`, `Rejected`, `Done`. All other valid statuses are outstanding unless the existing data model has an explicitly documented exception. Treat missing/unknown status conservatively as outstanding, but preserve the original status and do not silently classify it as completed.

## Tasks
1. Inspect the current Q426 Bug collection, snapshot generation, and rendering flow, particularly `scripts/refresh-q426.py`, `assets/q426.js`, the Q426 snapshot data schema, and existing Q426 tests. Determine where Level 2 Outstanding Defects count and table rows are derived; do not assume the bug count is calculated in the UI.
2. Keep the existing dedicated Bug JQL **unchanged** and continue retrieving all statuses. Do not add a status exclusion to the JQL or require Jira Saved Filters.
3. Introduce or reuse **one shared logical rule** for identifying outstanding bugs. Avoid inconsistent filtering between count, table, and other Q426 views.
4. Ensure Q426 Level 2 Outstanding Defects **count** excludes `Resolved`, `Closed`, `Rejected`, and `Done`.
5. Ensure the Q426 Level 2 Outstanding Defects **table** displays only outstanding bugs, so the count matches the number of displayed rows (subject to any existing, explicitly documented pagination/row limits).
6. If Q426 Level 1 displays an Outstanding Defects count, ensure it uses the same filtering rule. Do not change its Pass Rate or Task calculations.
7. Preserve all original Bug records and statuses in the existing snapshot model when feasible; avoid deleting completed bugs merely to make the count correct. If the current schema cannot support this without a larger change, report the smallest compatible approach and any trade-off.
8. Do not modify Q426 Task completion logic: Task Pass Rate still counts Jira Task statuses `Done`, `Closed`, `Resolved` as PASS. **Bug status filtering is a separate rule** and includes `Rejected` as non-outstanding.
9. Add focused deterministic tests for all listed statuses, mixed case, leading/trailing whitespace, unknown/missing status, count/table consistency, and Level 1 consistency if applicable. Ensure existing Q426 refresh and auto-publish tests remain green.
10. Run relevant Python and Node tests plus `git diff --check`. Report test counts and changed files. Keep the change minimal and scoped to Q426.

## Safety and workflow
- Do not change `query-config.local.md`, private JQL, credentials, Jira endpoints, or configuration.
- Do not modify Regression or Healthcheck code, snapshots, metrics, or workflows.
- Preserve snapshot validation, source completeness, Git dirty-target protection, and Auto-Publish safety checks.
- Do not execute a live Q426 refresh, commit, or push as part of implementation.
- Do not hand-edit live snapshot counts to conceal the problem.

## Deliverables
Report:
- Root cause and exact file/functions where the erroneous count originated
- Files changed and the final status normalization/filtering rule
- Evidence that Level 2 count and table agree, and Level 1 uses the same rule if applicable
- Test results (Python, Node, `git diff --check`)
- Any backward-compatibility considerations for existing snapshots

Stop after implementation and tests. Wait for user review before live refresh and publishing.
