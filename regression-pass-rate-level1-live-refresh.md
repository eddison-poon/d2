# Regression Test — Pass Rate Level 1 and Live Refresh Integration

Update the Regression Test dashboard requirements before proceeding with live refresh integration.

## Confirmed business rules

1. All Regression Test Level 1 cards must display **Pass Rate**, replacing Execution Completion.
2. Pass Rate = number of PASS executions / total executions × 100.
3. PASS is the only successful status. All other statuses are Non-PASS, including unknown custom statuses.
4. Level 1 must retain Outstanding Defects and use the existing RAG thresholds, applied to Pass Rate.
5. Level 2 must display Total Tests, Passed, Non-PASS, Execution Completion, Status Breakdown, and Outstanding Defects.
6. Preserve the raw Zephyr status names and counts in the breakdown.
7. Execution Completion must remain a separate metric: executed / total × 100. Do not calculate it using PASS alone.
8. Unknown statuses are Non-PASS but must not block publication solely because of their name.
9. Unverified or missing data must display N/A, not fabricated zero values.
10. Validate using the existing HK PoC snapshot: 220 total, 205 PASS, 15 Non-PASS, 93.18% Pass Rate, 100% Execution Completion, and 1 outstanding defect.
11. Continue integrating the recovered, validated Zephyr ZQL PowerShell retrieval and Jira JQL search workflow, including pagination, deduplication, per-environment failure isolation, and snapshot preservation.
12. Complete the Regression Test milestone first. Do not modify Q426 or Healthcheck in this phase.
13. Run all existing and new automated tests. Report changed files, test results, live validation results, and remaining blockers.

## Implementation constraints and acceptance checks

- Preserve the existing 12 Regression environments and their labels/order.
- Use the shared `regression_detail.html?environment=<id>` page; do not create new per-environment HTML pages.
- Maintain old detail-page compatibility links where already implemented.
- Do not change the meaning of Execution Completion; it remains distinct from Pass Rate.
- For any valid raw status not equal to PASS, count it as Non-PASS in Pass Rate and show its original name in Level 2 breakdown.
- Verify Zephyr and Jira query completeness before publishing a snapshot. If either query fails, preserve the last verified snapshot for that environment.
- Read private ZQL/JQL and authentication only through the existing approved local configuration and workflow; do not print or commit secrets.
- Use the previously recovered approved Zephyr request pattern and company Jira assistant skill. Do not invent endpoints or credentials.
- Start with a live HK PoC validation; then refresh other configured environments independently. Report unconfigured environments without overwriting their snapshots.
- Preserve Day/Night mode, Jira links, defect table, and existing Regression navigation.
- Keep Q426 and Healthcheck code and data untouched.
- Run automated tests and request manual verification of Level 1 and shared Level 2 before commit.

**Do not commit or push. Wait for manual review.**
