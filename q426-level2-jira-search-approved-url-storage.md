# Q426 Level 2 — Jira Search Link (Approved URL Storage)

## Decision

The user has confirmed that Jira Search URLs may be stored in the company GitHub repository.

Update the previous implementation approach accordingly.

Do not use Jira Saved Filters.

## Objective

Make the Total Task number on each Q426 Level 2 page clickable. Open Jira Issue Search using the exact dedicated Task JQL configured for that workstream.

## Implementation

1. Use the existing `query-config.local.md` as the single source of truth for Task JQL.
2. Map each Q426 workstream through its existing `reportKey`.
3. During Q426 refresh, generate a Jira Search URL from the same Task JQL used to retrieve Task data.
4. URL-encode the complete JQL correctly.
5. Store the generated Jira Search URL in the corresponding Q426 snapshot, for example `taskSearchUrl`.
6. The generated URL may contain URL-encoded JQL and may be committed to the company GitHub repository.
7. Keep `query-config.local.md` private and Git-ignored.
8. Determine the actual Jira Issue Search URL format from verified company Jira evidence. Do not invent an endpoint.
9. Update the shared Q426 Level 2 renderer in `assets/q426.js` so the Total Task number links to the snapshot's `taskSearchUrl`.
10. Open the link in a new tab using `target="_blank"` and `rel="noopener noreferrer"`.
11. If the URL is missing or invalid, render Total Task as plain text.
12. Support all existing and newly registered Q426 workstreams.
13. Ensure the Task JQL is used, not the Bug JQL.
14. Do not introduce Jira Saved Filters or duplicate JQL configuration.

## Validation

Add focused automated tests covering:
- Correct workstream-to-Task-JQL mapping
- URL encoding
- Valid and missing Jira Search URLs
- Total Task hyperlink rendering
- Existing Task Count and Pass Rate calculations
- Q426 refresh compatibility

## Constraints

- Minimal changes only.
- Preserve existing Q426 Level 1 and Level 2 calculations.
- Do not modify Regression or Healthcheck.
- Preserve Auto-Publish and Git safety checks.
- Do not store credentials or authentication tokens.
- Do not run a real refresh, commit, or push during implementation.

## Deliverables

Report:
- Files changed
- Jira Search URL pattern used
- How the URL is generated
- Automated test results
- Any remaining blockers

Wait for user review before publishing.
