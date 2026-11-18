# Operations Manager — Phase C2: Jira Story Creation E2E Validation

## Objective
Validate the existing Operations Manager Jira ticket creation workflow using the company Jira Assistant scripts and verified Jira connectivity launcher.

**This run must stop after ticket preview. Do not create a Jira ticket until explicit approval of the exact proposed ticket in a subsequent message.**

## Part 1 — Review and Commit Phase C1.3
1. Run `git status` and inspect relevant diffs.
2. Identify the six files changed during Phase C1.3.
3. Confirm the approved Operations Manager-specific Jira launcher is implemented.
4. Confirm company Jira Assistant scripts remain unchanged.
5. Check that no credentials, tokens, passwords, or sensitive local configuration are included.
6. Preserve unrelated or pre-existing local changes; exclude them from this commit.
7. Run existing no-write launcher tests, if available.
8. Stage only reviewed Phase C1.3 changes.
9. Commit with message: `fix: persist Jira connectivity for Operations Manager`
10. Push to the current tracking branch.

If changes cannot be confidently attributed to Phase C1.3 or branch state risks overwriting other work, stop and request clarification. Do not force-push, rebase, or overwrite remote changes. Report commit SHA and push result.

## Part 2 — Jira Read-only Preflight
Use the existing Operations Manager launcher (`jira_assistant.py`) for all Jira operations. Do not invoke company scripts directly. No Jira MCP.

### Target ticket
- Project key: **ETIVAI**
- Issue type: **Story**
- Assignee: **My verified Jira account**
- Summary: **[TEST] PT TPM upper limit issue**
- Description: **Validate Jira ticket creation, duplicate checking, read-back verification, and reporting through Operations Manager.**
- Sprint: Not specified (optional)
- Epic: Not specified (optional)

This is a technical E2E test. The summary and description need not describe the same business issue; preserve both exactly.

### Preflight checks
1. Verify connectivity via the persistent launcher in a fresh process.
2. Confirm ETIVAI is the correct project key.
3. Verify Story is creatable in this project.
4. Identify required creation fields and expected values.
5. Resolve my Jira account using verified Jira information; do not guess identifiers.
6. Verify the account can be assigned to this Story.
7. Check available create permissions.
8. Identify mandatory fields not supplied.

No Jira writes during preflight. Stop if required fields or assignee cannot be verified.

## Part 3 — Duplicate Detection
Run read-only, project-scoped searches for:
- Exact summary matches
- Similar summaries containing `PT TPM`
- Existing tickets describing the same upper-limit issue

Report potential duplicates with issue key, summary, status, URL, and similarity reason. The current helper may return limited results: do not claim exhaustive coverage without verified pagination. Stop and request a decision if likely duplicates exist. Do not automatically update or reuse an issue.

## Part 4 — Ticket Preview
Present the exact proposed Story:

| Field | Proposed value |
|---|---|
| Project | ETIVAI |
| Issue Type | Story |
| Summary | [TEST] PT TPM upper limit issue |
| Description | Validate Jira ticket creation, duplicate checking, read-back verification, and reporting through Operations Manager. |
| Assignee | Verified Jira account |
| Priority | Jira default unless required |
| Labels | None unless required |
| Sprint | Not assigned |
| Epic | Not assigned |

Show verified mandatory fields and report connectivity, project/type/assignee verification, create permission, duplicate results/limitations, exact preview, and blockers.

## Mandatory Approval Gate
**STOP after presenting the preview. Do not execute Jira create.**
Wait for explicit approval of exact ticket details in a subsequent message. Approval to commit/push Phase C1.3 is NOT approval to create an issue.

## Part 5 — Post-approval Execution Plan (do not execute in this run)
Only after explicit subsequent approval:
1. Reconfirm unchanged approved fields.
2. Recheck likely duplicates if needed.
3. Create exactly one Story via the existing launcher.
4. Capture issue key and URL.
5. Fetch the new issue.
6. Verify saved project, issue type, summary, description, labels, priority, and assignee where supported.
7. Report mismatches or partial failures.

If create times out or outcome is uncertain, search/reconcile before any retry. Never automatically create a second issue. Never claim Sprint or Epic was assigned.

## Restrictions
- No Jira MCP, new dependencies, unnecessary scripts, or company Jira Assistant script changes.
- No system-wide proxy changes.
- No Jira writes before explicit ticket approval.
- No credentials or secrets in output or commits.
- Preserve the lightweight Markdown-first architecture.

## Expected output for this run
A. Phase C1.3 Commit and Push Result
B. Jira Connectivity Verification
C. Project / Story / Assignee Validation
D. Duplicate Search Results
E. Exact Jira Ticket Preview
F. Outstanding Issues
G. Awaiting Explicit Ticket Creation Approval

Do not proceed to Jira ticket creation during this run.
