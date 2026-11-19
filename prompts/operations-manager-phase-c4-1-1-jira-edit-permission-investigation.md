# Operations Manager — Phase C4.1.1: Jira Edit Permission Read-only Investigation

## Objective
Resolve the edit-specific evidence gap found in Phase C4.1 before considering Phase C4.2. Target only existing test Story ETIVAI-20609. Determine, without any Jira write, whether the authenticated user has project and issue-level edit permission and whether Description is editable. Preserve the lightweight Markdown-first Operations Manager architecture.

## Confirmed baseline from C4.1
- Approved launcher successfully fetched ETIVAI-20609 (ETIVAI / Story, status Open).
- Complete current Description: `Validate Jira ticket creation, duplicate checking, read-back verification, and reporting through Operations Manager.`
- Proposed C4.2 change: append one LF newline and `Phase C4 controlled update validation.`
- Existing company update helper accepts a description-only update, sending only `fields.description` in its PUT body, but this was verified by code inspection only.
- Current preflight covers creation permissions/metadata, not `EDIT_ISSUES`, issue-level restrictions, or description editability.
- C4.1 made zero Jira writes and zero repository changes.

## Restrictions
1. Read-only only. Do not create, update, transition, comment on, delete, or otherwise modify any Jira issue.
2. No Jira MCP. Use the existing approved Operations Manager launcher and company Jira Assistant integration only.
3. No modifications to company scripts, launcher, repo files, dependencies, credentials, proxy, TLS, authentication, or system settings. No commits or pushes.
4. Do not bypass the launcher or invoke company scripts directly. Do not introduce arbitrary URL/HTTP command functionality.
5. Inspect bundled Jira REST documentation and existing code first. Only use documented, explicitly supported read-only GET requests with the existing approved authentication and routing; if the launcher cannot safely issue the needed request, report BLOCKED rather than inventing a workaround.
6. Do not treat a successful Create permission check or previous Story creation as proof of Edit permission.
7. Do not request blanket Jira write approval. Phase C4.2 requires a separate explicit approval for the exact final before/after change.

## A. Existing capability assessment
1. Inspect the current launcher, company integration, bundled Jira REST reference, and relevant Operations Manager instructions.
2. Identify existing read-only commands, supported permission checks, and any edit metadata capability. Distinguish available implementation from merely documented endpoints.
3. Confirm the approved launcher can still fetch ETIVAI-20609 in a fresh process.
4. Report whether edit-specific checks are possible without changing any file or bypassing the launcher.

## B. Project-scoped edit permission
1. Determine whether the existing approved read-only interface can retrieve the authenticated user's `EDIT_ISSUES` permission for project ETIVAI (or an issue-scoped equivalent) using a documented supported endpoint.
2. If supported, obtain evidence and distinguish Granted, Denied, and Unknown.
3. If unavailable, report precisely why; do not substitute `CREATE_ISSUES` or `ASSIGN_ISSUES` as evidence.

## C. Issue-level editability and Description field
1. Determine whether the existing approved read-only interface supports a documented edit-metadata GET for ETIVAI-20609, or an equivalent explicitly supported read-only capability.
2. If available, inspect whether Description is present and settable and whether edit restrictions or workflow constraints are reported.
3. If the endpoint returns 403/404/unsupported or the interface cannot access it, distinguish endpoint unavailability from permission denial. Do not guess or try arbitrary alternate API paths.
4. Clearly state that read-only metadata and permission checks cannot guarantee acceptance by custom server-side validators.

## D. Baseline and update safety
1. Re-fetch ETIVAI-20609 through the approved launcher.
2. Verify the current Description remains exactly the C4.1 baseline and the proposed appended sentence is not already present.
3. Inspect, without execution, that the existing helper would submit only Description, replacing its entire value.
4. Note the helper has no concurrency guard; any later authorized C4.2 must re-fetch immediately before its single write and stop if the baseline changed.
5. Do not execute any update, including a write-capable dry run.

## E. Required report
A. Launcher and Baseline Fetch — PASS/FAIL/BLOCKED
B. Existing Read-only Edit Verification Capabilities
C. `EDIT_ISSUES` Permission — GRANTED/DENIED/UNKNOWN with evidence
D. Issue-level Editability and Description — VERIFIED/BLOCKED/UNKNOWN with evidence
E. Current Description and Proposed One-line Addition (preview only)
F. Remaining Risks and Exact Blockers
G. C4.2 Readiness — READY or BLOCKED, with explicit reasons

If all required evidence is obtained, recommend a separately approved, single-attempt C4.2 update with immediate read-back and field comparison. If any evidence remains unavailable, state the smallest next read-only capability needed as a proposal only; do not implement it.

## Acceptance criteria
- Ground every permission/editability conclusion in an actual supported read-only response, or explicitly mark it UNKNOWN.
- Preserve the exact original Description and all unrelated fields.
- Zero Jira writes, zero repository modifications, zero commits/pushes, zero security configuration changes.
- End without executing C4.2.
