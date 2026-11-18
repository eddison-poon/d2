# Operations Manager — Phase C2.2: First Jira Story Creation E2E Validation

## Objective
Validate one end-to-end Jira Story creation through the existing Operations Manager and company Jira Assistant scripts, using the approved Jira connectivity launcher. Do not create any ticket until the user explicitly approves the exact final preview in this Copilot session.

## Constraints
- Lightweight, Markdown-first. No architecture redesign, new dependencies, or unrelated changes.
- No Jira MCP. Use only the approved Operations Manager launcher and unchanged company Jira Assistant scripts.
- Preserve existing proxy settings, credentials, TLS verification, and corporate routing.
- Never call the company scripts directly when the approved launcher is required.
- Do not modify or delete any existing Jira issue.
- Sprint and Epic are optional and must be omitted; never claim they were assigned.
- Do not expose secrets or tokens.
- No automatic retry of a potentially successful create operation.

## Step 1 — Review and commit Phase C2.1.2 changes
1. Inspect git status, current branch, remote, and the diff.
2. Identify the approved Phase C2.1.2 changes in `jira_assistant.py` and `README.md` only.
3. Preserve unrelated local edits; stage only the intended hunks. If changes cannot be isolated safely, stop and request clarification.
4. Run available no-write regression checks, including preflight and search/fetch.
5. Commit only the approved changes with message: `fix: validate Jira Story creation metadata preflight`.
6. Attempt normal non-force push. Verify remote status. If push fails, report the exact failure and preserve the commit; do not alter GitHub proxy/security settings, rebase, or force-push without separate approval.
7. Do not let a push failure cause a Jira write.

## Step 2 — Fresh read-only preflight
Use the existing launcher for a fresh preflight:
- Site: alm
- Project: ETIVAI
- Issue Type: Story
- Verify project key, Story ID, required fields, available defaults, Create Issues and Assign Issues permissions, and current user assignability.
- The prior run reported Story ID 10001, required Project/Issue Type/Summary, and verified the user's assignable account. Reconfirm live; do not blindly reuse stale evidence.
- Confirm launcher search/fetch functionality.
- If any mandatory preflight check fails, stop before creation.

## Step 3 — Duplicate search
Repeat project-scoped duplicate searches, including:
- Exact summary: `[TEST] PT TPM upper limit issue`
- Summary containing `PT TPM`
- Relevant broader terms `TPM`, `upper`, and `limit`
Check Jira-reported totals against returned counts. Search is single-page and not exhaustive; disclose coverage limits. Review relevant matches, including prior related issue ETIVAI-13104, without automatically treating it as a duplicate. If an exact or material duplicate is found, stop and ask the user.

## Step 4 — Exact ticket preview
Show the final fields before requesting approval:
- Project: ETIVAI
- Issue Type: Story (previously verified ID 10001; reconfirm)
- Summary: [TEST] PT TPM upper limit issue
- Description: Validate Jira ticket creation, duplicate checking, read-back verification, and reporting through Operations Manager.
- Assignee: authenticated and verified assignable Jira user (do not infer the API identifier from display name)
- Priority: omit; use Jira default (previous metadata reported Major)
- Labels: none
- Sprint: omitted
- Epic: omitted
- Additional mandatory fields: only those confirmed by current preflight

Present the exact request payload, with credentials excluded. Stop and ask for explicit approval to create exactly ONE Story using that preview. Prior approvals for implementation, read-only investigation, or this prompt do NOT authorize ticket creation.

## Step 5 — Create exactly once, only after explicit approval
Once the user clearly approves the exact Step 4 preview in a subsequent Copilot response:
1. Recheck material prerequisites if the session or data has changed.
2. Use the approved launcher and company create command once.
3. Record the returned issue key and link.
4. If a timeout or ambiguous response occurs, search/reconcile before any retry; do not create again automatically.
5. Do not update the ticket to compensate for mismatches without a new approval.

## Step 6 — Read-back verification
Fetch the created issue through the approved launcher. Compare project, type, summary, description, assignee (display name read-back is acceptable, with identity limitation disclosed), priority/default, labels, and absence of Sprint/Epic claims. Report per-field outcomes. If creation succeeded but read-back differs, preserve the issue key and report the discrepancy; do not recreate.

## Step 7 — Final report
Provide:
A. C2.1.2 commit SHA and push status
B. Fresh preflight results
C. Duplicate-search queries, counts, matches, and limitations
D. Exact preview and explicit approval record
E. Create invocation outcome (one attempt maximum)
F. Jira issue key and URL, if created
G. Read-back field comparison
H. Remaining limitations and next steps

Stop at the approval gate during the initial execution of this prompt. Do not create a Jira issue in the initial run.
