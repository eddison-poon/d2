# Operations Manager — Phase C3: Read-only Functional Validation

## Objective
Validate day-to-day Jira search, fetch, and status reporting through the existing lightweight Copilot Operations Manager. Phase C2.2 successfully created and read back Story ETIVAI-20609; Phase C2.3 finalized the E2E documentation and confirmed the Git remote. Do not repeat creation.

## Scope and restrictions
- Read-only Jira operations only. No create, update, transition, delete, or comments.
- No Jira MCP. Use only the existing approved Operations Manager launcher and company Jira Assistant scripts.
- Do not modify company scripts, proxy/TLS configuration, credentials, or repository files.
- No new dependencies, frameworks, or extra scripts. Preserve Markdown-first architecture.
- No commit or push during this validation.
- Do not investigate Agent Hub Testing Dashboard, Regression, or Bug JQL; those issues are resolved.
- Stop and report if approved connectivity or authentication fails. Never bypass security controls.

## A. Environment and launcher check
1. Inspect the current Operations Manager instructions and documented launcher usage.
2. Confirm approved launcher is available and its search/fetch commands are supported.
3. Perform a fresh read-only connectivity check without manual proxy changes.
4. Report PASS/FAIL with concise evidence, excluding secrets.

## B. Search and fetch
1. Fetch ETIVAI-20609 through the launcher.
2. Verify project, issue type, summary, description, status, assignee display name, priority, and labels against available Jira responses. Mark fields not exposed as NOT VERIFIED rather than assuming.
3. Search by exact key and by summary phrase within project ETIVAI. Compare returned issue keys with the fetched issue.
4. Exercise a safe project-scoped JQL status query (e.g., project = ETIVAI ORDER BY updated DESC) with a bounded result limit. Report returned count, Jira-reported total, and pagination/truncation limitations. Do not claim exhaustive coverage.
5. Use a deliberately nonexistent issue key or clearly impossible exact summary for a negative read-only test; distinguish zero results from errors.

## C. Status reporting
1. Generate a compact read-only snapshot from the bounded ETIVAI query: total reported, fetched sample count, and breakdown by Jira status.
2. Show 5 representative issue rows (key, summary, status, assignee, updated time) when these fields are available.
3. Clearly label sample-derived status counts, not whole-project totals, unless complete pagination is actually verified.
4. Provide a reusable example of a project-scoped JQL status query; do not assume sprint or epic filters.
5. Do not write reports to Confluence or any repository file.

## D. Results and recommendation
Return:
A. Launcher and Connectivity
B. Search / Fetch Test Cases — PASS / FAIL / BLOCKED
C. ETIVAI-20609 Field Verification
D. Status Report (sample scope and limitations)
E. Issues / Root Causes
F. Readiness for a separate Phase C4 Update Preview

If a step is blocked, continue only with independent safe read-only steps. Do not alter code to repair failures in this phase. End with a recommendation for a future controlled update test, but do not perform an update or request blanket write approval.

## Acceptance criteria
- Search and fetch work in a fresh session through the approved launcher.
- The previously created Story is retrieved and its available fields checked.
- JQL status reporting is demonstrably grounded in returned data.
- Missing fields, partial results, and errors are explicitly identified.
- Zero Jira writes, zero repository modifications, and zero proxy/security changes.
