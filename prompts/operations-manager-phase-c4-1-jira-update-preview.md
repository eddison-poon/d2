# Operations Manager — Phase C4.1: Controlled Jira Update Preview (Read-only)

## Objective
Prepare a precise, minimal, reversible update preview for the existing test Story ETIVAI-20609, using the established lightweight Operations Manager workflow. This phase is **read-only**: do not update the issue. Phase C3 verified launcher search/fetch and bounded status reporting; preserve those working paths.

## Non-negotiable restrictions
- Do not create, update, transition, delete, comment on, or otherwise write to any Jira issue.
- No Jira MCP. Use only the approved Operations Manager launcher and existing company Jira Assistant scripts.
- Do not bypass the launcher or change company scripts, authentication, proxies, TLS settings, credentials, environment-wide settings, or dependencies.
- Do not edit, commit, or push any repository files. No new code or scripts.
- Do not revisit Agent Hub Testing Dashboard, Regression, or Bug JQL.
- If required read-only evidence is unavailable, mark BLOCKED and stop; do not infer API support or improvise a write.
- C4.1 approval is **not** approval for C4.2. Obtain explicit approval of the final exact before/after update in a later turn before any Jira write.

## A. Baseline fetch
1. Review existing Operations Manager instructions, launcher, and update skill/command interface without changing files.
2. In a fresh process, fetch ETIVAI-20609 using the approved launcher.
3. Confirm key, project ETIVAI, type Story, current status, summary, description, assignee display name, priority, labels, and available update-relevant fields.
4. Distinguish observed values from fields that the company fetch does not expose. Never claim that absent values are empty.
5. Confirm this is the previously created test Story, not another issue. Stop if identity differs.

## B. Choose one safe candidate change
- Preferred candidate: append the following single sentence to the **description**, retaining the existing description verbatim:
  `Phase C4 controlled update validation.`
- Do not select summary, assignee, priority, status, sprint, epic, labels, or another field unless the description update is demonstrably unsupported. If unsupported, stop with a recommendation; do not silently switch fields.
- Check whether the sentence already exists. If so, report NO-OP and stop rather than duplicate it.
- Confirm the launcher/company update command supports an exact description-only update and inspect how it constructs the request. Read code/instructions only; do not execute an update or a dry-run that sends a write request.
- Preserve existing description formatting and content. If read-back is truncated or the update command would overwrite other fields, stop as BLOCKED.
- If the helper cannot safely preserve Jira's description representation, report the limitation instead of guessing.

## C. Read-only preflight and preview
1. Reuse the approved read-only connectivity and relevant permission/metadata checks where available; clearly distinguish permission evidence from guaranteed update success.
2. Identify any issue-level edit restrictions or unknowns. Do not assume permission from prior create success.
3. Show exact current description and proposed complete description, plus a concise line-level difference.
4. Present the intended update command/payload shape **for review only**. Do not run it.
5. Explicitly state the expected unchanged fields: key, project, issue type, summary, status, assignee, priority, labels, sprint, epic.
6. Explain how C4.2 would perform exactly one authorized update attempt, fetch the issue again, compare changed and unchanged observable fields, and stop without automatic retries if the result is uncertain.
7. Note that Jira's updated timestamp/history may change as a normal consequence of a later approved write.

## D. Required output
A. Launcher and Baseline Fetch — PASS / FAIL / BLOCKED
B. Update Capability and Permission Evidence
C. Exact Before / After Description and Diff
D. Proposed Single-field Update Payload (NOT EXECUTED)
E. Risks, Unknowns, and Rollback Considerations
F. C4.2 Approval Gate — **AWAITING EXPLICIT APPROVAL**

Report zero Jira writes, zero repository changes, and zero commit/push. Do not interpret the request to prepare a preview as authorization to execute the update.

## Acceptance criteria
- ETIVAI-20609 fetched and identified using the approved launcher.
- One minimal description-only change proposed with no collateral field changes.
- Complete before/after values and update mechanics are visible for review, or a specific blocker is reported.
- No Jira write, repository edit, or security configuration change.
- End at the approval gate.
