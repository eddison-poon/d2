# Regression Auto-Publish — Stale Assertion Fix and Safe Recovery

## Context

A real Regression Test refresh updated two local snapshots:
- HK PoC v2: 217 total, 205 PASS, 12 non-PASS, 94.47% Pass Rate, 100% completion, 1 defect.
- UK Prod v1: 22 total, 20 PASS, 2 non-PASS, 90.91% Pass Rate, 100% completion, 0 defects.

Python tests passed 48/48, but Node tests passed only 29/31. Two assertions apparently expect older HK PoC figures (220 total, 205 PASS, 15 non-PASS, 2 defects). Auto-Publish correctly blocked publication. Updated snapshots remain modified locally, so a new attempt encounters the pre-existing dirty-snapshot protection.

Some other environments retained their snapshots because the latest query status was unavailable. Do not treat preserved data as newly verified.

## Objective

Investigate and fix stale live-data test assertions without weakening validation or snapshot safety. Preserve and assess the locally refreshed snapshots, then recommend a safe recovery/publishing path.

## Tasks

1. Inspect the actual Node test failures and verify the root cause; do not assume both failures have identical causes without evidence.
2. Replace hardcoded assertions against mutable live snapshot counts with stable data-driven integrity assertions, including:
   - Total = PASS + non-PASS (where those categories cover all executions).
   - Pass Rate = PASS / Total × 100, with the established rounding and N/A rules.
   - Execution Completion follows the existing definition and is not conflated with Pass Rate.
   - Snapshot schema, status breakdown and defect record structure are valid.
   - Level 1 and shared Level 2 render consistent values from the same snapshot.
3. Keep deterministic fixture-based tests with explicit expected values for calculation and rendering behavior. Do not merely delete failing tests or loosen them into vacuous assertions.
4. Preserve existing Regression refresh, validation, snapshot protection, and Auto-Publish safety checks.
5. Run the full relevant Python and Node test suites and report actual results.
6. Inspect existing dirty Regression snapshot files. Compare their contents with the available successful refresh evidence and clearly identify which files are verified, unverified, or cannot be verified.
7. Do not overwrite, reset, discard, stash, or silently regenerate those snapshots.
8. Explain how to safely publish verified snapshots after the test repair. Keep this repair task read-only with respect to Git publishing: **do not commit or push**.
9. Do not modify Q426, Healthcheck, private JQL/ZQL configuration, or unrelated Dashboard functionality.
10. If verification evidence is incomplete, report the gap and stop rather than claiming that the data is verified.

## Deliverables

- Confirmed root cause and exact failing assertions.
- Files changed and rationale.
- Python/Node test results.
- Snapshot-by-snapshot verification status.
- Recommended minimal manual commit/push steps for the repaired tests and verified snapshots, or a safe alternative if verification is incomplete.
- A subsequent clean-worktree Regression refresh test plan to validate automatic publishing end to end.

## Important

This is a repair and recovery request, **not** a fresh Regression refresh. Do not bypass dirty-snapshot protection, force push, or publish automatically during this task.
