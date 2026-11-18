# Regression Refresh — Controlled Read-Only Live Diagnostics

## Objective
Validate the newly implemented safe Network and Zephyr Pagination diagnostics against live sources without modifying snapshots, configuration, source code, or Git state.

## Context
- The diagnostic enhancement was implemented locally in `scripts/refresh-regression.py` and `scripts/auto-publish-refresh.py`, with tests and README changes.
- Synthetic validation passed: 64 Python and 33 Node tests.
- The precise causes of prior Jira Bug JQL NETWORK failures and HK PoC v2 pagination failure remain unconfirmed.
- Five Regression environments are configured; seven are unconfigured and must be skipped.
- Local working tree contains uncommitted diagnostic changes. Do not use Auto-Publish or any command that requires a clean working tree or can commit/push.
- This is a single explicitly approved **read-only diagnostic collection**. No refresh or publication is approved.

## Instructions to Copilot

1. Verify the current working directory is the `agenthub-testing-dashboard-fresh` repository. Inspect the existing collector CLI and code to determine the exact supported **live, non-writing** invocation. Do not invent flags or commands. In particular, verify the semantics of `--live`, `--write`, and default behavior before execution.
2. Perform a read-only preflight. Identify the five configured environments from the local private config without printing, copying, committing, or logging raw JQL/ZQL, credentials, tokens, headers, or private configuration. Report the seven unconfigured environments as SKIPPED.
3. Confirm the proposed invocation will not modify snapshot files, source files, Git state, or dashboard output. Do not run `scripts/auto-publish-refresh.py`, use `--write`, or invoke any publishing wrapper. If non-writing behavior cannot be proven, stop and explain.
4. Execute **one** live read-only diagnostic collection for the five configured environments using the verified collector interface. No automatic retries.
5. Capture only the explicitly allowlisted sanitized diagnostic fields to a temporary location **outside the repository**. Do not save raw stdout/stderr or exception text, raw query strings, URLs, credentials, IDs, headers, response bodies, or stack traces. If safe capture cannot be guaranteed, keep results in memory and report only sanitized status fields.
6. For each configured environment, report:
   - Zephyr ZQL: SUCCESS / FAILED / UNKNOWN
   - Jira Bug JQL: SUCCESS / FAILED / UNKNOWN
   - Safe failure category and subtype, if evidence exists
   - Pagination check identifier and available numeric evidence (requestedOffset, returnedOffset, pageLimit, rowsReceived, expectedTotal, observedTotal, duplicateCount, conflictCount) where the implemented sanitizer allows it
   - Whether the result supports a specific cause or remains UNKNOWN
7. Treat read-only collection results as diagnostic observations only. Do not claim snapshots were updated or published. Never infer success merely from unchanged snapshots.
8. After the run, inspect `git status --short` and verify that no files were modified by this diagnostic beyond the pre-existing local changes. If unexpected modifications occurred, report them without reverting or committing.

## Safety and stopping rules
- No source/config edits, no `--write`, no snapshot updates, no commit/push, no Auto-Publish, no retry.
- Do not reveal private configuration or raw errors.
- If the collector cannot safely perform live read-only collection, stop before execution.
- If a live request fails, preserve existing data and report the sanitized evidence rather than guessing a root cause.

## Deliverables
Provide the exact verified read-only command, confirmation of one execution (or reason stopped), a compact per-environment results table, sanitized diagnostic log path if safely created, Git before/after status, and the smallest next action supported by evidence. Distinguish confirmed findings from hypotheses.
