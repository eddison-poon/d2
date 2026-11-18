# Operations Manager — Phase C2.1.2: Jira Creation Metadata Fix

Approved — proceed with Phase C2.1.2: Jira Creation Metadata Fix.

Implement the minimal fix proposed in Phase C2.1.1.

## Requirements

1. Replace the legacy creation metadata endpoint with the verified paginated project issue-type and field metadata endpoints.
2. Use the discovered Story issue type ID (10001), validating it against the live response.
3. Retrieve all creation fields and verify pagination completeness.
4. Correct the contextual Issue Type validation so it does not incorrectly require the `set` operation.
5. Preserve existing permissions, identity, assignability, authentication, routing, and fail-closed behavior.
6. Modify only `jira_assistant.py` and `README.md`.
7. Preserve existing local changes and do not modify company Jira Assistant scripts.
8. Run regression tests and live read-only preflight for ETIVAI / Story.
9. If preflight passes, perform project-scoped duplicate searches for `[TEST] PT TPM upper limit issue` and prepare the exact ticket preview.
10. Report all validation results and outstanding blockers.

## Restrictions

- No Jira MCP.
- No Jira ticket creation, update, or deletion.
- No new dependencies.
- No proxy, credential, or TLS changes.
- Do not commit or push yet.

Stop after presenting the preflight results, duplicate search results, and final ticket preview.

Jira ticket creation requires my separate explicit approval.
