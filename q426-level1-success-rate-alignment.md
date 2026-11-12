# Q426 — Level 1 Success Rate KPI Alignment

## Context
Repository: agenthub-testing-dashboard. Q426 already has a dynamic workstream registry, one-command registration, a shared Level 2 page (`q426_detail.html?workstream=<id>`), and Jira JQL-driven task/defect snapshots. Regression Test now displays Pass Rate on Level 1 and execution details on Level 2. This change is limited to Q426 and must not affect Regression or Healthcheck.

## Confirmed business rule
- A Jira Task is PASS if its status is `Done`, `Closed`, or `Resolved` (case-insensitive; trim surrounding whitespace).
- Every other status is Non-PASS.
- **Q426 Success Rate = PASS Tasks / Total Tasks × 100%**.
- If Total Tasks is zero, unavailable, or unverified, display `N/A` rather than a fabricated 0%.
- A verified nonzero task total with zero PASS tasks displays 0%.
- Use the existing task deduplication and verified snapshot semantics; never count duplicate Jira tasks twice.

## Requested UI behavior
1. Change the KPI label on **all Q426 Level 1 workstream cards** from `Execution Completion` to **`Success Rate`**.
2. Use the existing completed-task count and total-task count if they already implement this exact rule; avoid redundant calculations or Jira queries. Confirm the mapping against actual code first.
3. Keep the existing progress bar and RAG color thresholds, now representing Success Rate, and keep Outstanding Defects unchanged.
4. Keep Q426 Level 2's current **Task Execution Summary**, including Total Tasks, Completed, Remaining, Execution Completion, and Outstanding Defects. Do not rename its Execution Completion metric in this milestone.
5. Preserve the shared Level 2 routing, dynamic registry, all existing workstream IDs/order/data, and the `Add Q426 workstream: <name>` and `Refresh all Q426 workstreams` commands. Newly registered workstreams must automatically show Success Rate on Level 1 without HTML edits.
6. Preserve correct N/A vs verified-zero behavior, snapshots, Jira hyperlinks, search, and Day/Night mode.
7. Do not modify Healthcheck or Regression Test code/data/UI.

## Implementation approach
- Inspect existing Q426 calculation, rendering, registry, data format, and tests before editing.
- Make the smallest possible change to shared Q426 Level 1 rendering and any required tests/documentation. Avoid changes to per-workstream data snapshots unless a genuine defect is discovered and explained.
- No new dependencies, new HTML pages, new API integrations, or changes to private local JQL.
- Update README or agent instructions only where existing text would otherwise misdescribe the Level 1 KPI.

## Validation
- Test Done, Closed, Resolved, case variants, and all other statuses as Non-PASS.
- Test 1/9 -> 11.1%, 0/N -> 0%, and 0/0 -> N/A.
- Test unknown/unverified data -> N/A and verified zero defects -> 0.
- Confirm all current and future registry-driven Q426 cards display the new label and correct metric.
- Confirm Level 2 continues to show Execution Completion and its existing summary and defects table.
- Confirm Regression and Healthcheck remain unchanged.
- Run all existing and new automated tests and report pass/fail/skip counts.
- Request manual verification of Q426 Level 1, Level 2, and Day/Night mode.

## Report
Summarize files changed, formula validation, test results, UI checks still required, and any unexpected scope expansion.

**Do not commit or push. Wait for user review.**
