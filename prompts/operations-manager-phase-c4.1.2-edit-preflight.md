# Operations Manager — Phase C4.1.2: Minimal Jira Edit Preflight Enhancement

## Objective
Resolve the read-only edit-verification gaps identified in Phase C4.1.1 for the existing test Story ETIVAI-20609. Add the smallest narrowly scoped read-only edit-preflight capability to the existing Operations Manager Jira launcher. Do not update any Jira issue in this phase.

## Confirmed baseline
- Jira deployment reports Server 10.3.8, with /jira context path.
- Existing launcher supports search, fetch, create, update, and creation preflight.
- Phase C4.1.1 fetched ETIVAI-20609 and confirmed the original Description remains unchanged.
- The current creation preflight does not check EDIT_ISSUES.
- Existing launcher does not expose issue edit metadata.
- Phase C4.1.1 did not obtain live edit-permission or edit-metadata responses; no permission denial is established.
- Proposed later change: append exactly one LF newline and the sentence `Phase C4 controlled update validation.` to the existing Description, with no trailing newline. This is preview-only in this phase.

## Phase A — Read-only compatibility investigation
1. Inspect the existing launcher, README, relevant local agent/skill instructions, approved company Jira helper and bundled REST references. Preserve existing local edits.
2. Identify the narrowest Jira Server-compatible, read-only routes for:
   - project-scoped EDIT_ISSUES permission for ETIVAI;
   - issue-scoped EDIT_ISSUES permission for ETIVAI-20609, if supported;
   - issue edit metadata for ETIVAI-20609, including Description and its permitted edit operations.
3. Prefer the existing approved authentication, routing, API root, and JSON-request helper. Do not assume Jira Cloud v3 documentation proves support on this Server deployment.
4. If compatibility cannot be established safely, stop and report the exact unknowns and a minimal proposal. Do not guess paths or silently fall back to another API version.

## Phase B — Minimal implementation (only after compatibility is established)
1. Add a single explicit `edit-preflight` read-only command to the existing `scripts/jira_assistant.py` launcher, scoped to an explicit site and issue key. No generic arbitrary-URL or arbitrary-REST interface.
2. Check the authenticated user's EDIT_ISSUES permission at the applicable project and issue scopes, clearly distinguishing granted, denied, unknown, and unsupported.
3. Retrieve issue edit metadata and determine whether Description is present and editable; evaluate supported operations based on the actual response schema, not a Cloud-only assumption.
4. Return sanitized structured JSON with: site, issue key, checked endpoint families, permission evidence, Description editability evidence, completeness, ready boolean, and explicit blockers/unknowns. Never print credentials, tokens, authorization headers, or unnecessary personal information.
5. Fail closed on HTTP errors, missing fields, ambiguous response shapes, incomplete data, or inconsistent evidence. No guessed defaults.
6. Keep company Jira scripts, existing search/fetch/create/update behavior, proxy/TLS/authentication configuration, and parent process environment unchanged.
7. Update only essential launcher documentation in README.md. Do not introduce dependencies or refactor unrelated code. Preserve unrelated working-tree edits.

## Phase C — Verification
1. Run focused mocked no-write tests for successful permission/editability checks, permission denied, missing Description, unsupported edit operations, HTTP 403/404, incomplete/ambiguous metadata, and output sanitization.
2. Re-run applicable existing no-write regressions.
3. Run a fresh live `edit-preflight` for ETIVAI-20609 through the approved launcher, using read-only requests only.
4. Fresh-fetch the issue and confirm its Description remains exactly unchanged.
5. Report precise endpoints used and HTTP outcomes (sanitized), plus whether project permission, issue permission, and Description editability were each independently verified. Do not label a check PASS merely because an endpoint returned 200.
6. Report exact files changed, tests executed and passed/failed, limitations, and readiness for C4.2. If readiness remains blocked, identify the blocker and the smallest safe next action.

## Safety and approval gates
- ZERO Jira writes: no PUT, POST, PATCH, DELETE, issue update, issue creation, or workflow transition.
- No Git commit or push in this phase unless separately approved.
- No modifications to company scripts, system proxy, TLS verification, credentials, or security controls.
- No automatic retries of writes; no writes are authorized here.
- Do not execute the previously previewed Description update.
- Do not treat read-only preflight as a guarantee against custom server-side validators or concurrent modifications.
- C4.2 requires separate explicit approval of the exact final before/after Description and one controlled update attempt, following a fresh baseline check.

## Required final report
A. Compatibility evidence and exact read-only endpoints
B. Minimal changes made (or why implementation stopped)
C. Mocked and regression test results
D. Live ETIVAI-20609 permission/editability evidence
E. Baseline unchanged confirmation
F. C4.2 readiness: READY / BLOCKED, with explicit caveats
G. Git status, with confirmation that no commit/push or Jira write occurred

Stop after reporting. Do not proceed into C4.2.
