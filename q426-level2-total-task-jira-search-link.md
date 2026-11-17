# Q426 Level 2 — Total Task Jira Search Hyperlink

## Objective

Make the Total Task number on each Q426 Level 2 page clickable, opening Jira Issue Search with the dedicated Task JQL for that workstream.

## Scope

Q426 Level 2 only.

Use the existing shared page:
`q426_detail.html?workstream=<id>`

Do not modify Healthcheck, Regression, or Q426 Level 1.

## Requirements

1. Inspect the existing Q426 registry, snapshot schema, shared Level 2 renderer, refresh workflow, and private JQL configuration.
2. Identify how each Q426 workstream maps to its dedicated Task JQL.
3. Determine the correct Jira Issue Search URL format from existing project configuration or verified Jira links. Do not invent a Jira host or URL pattern.
4. Assess whether storing URL-encoded Task JQL in committed snapshots is permitted. If this cannot be established, stop and report the decision needed before implementing that storage approach.
5. Add a Jira Search hyperlink to the Total Task number, preserving its current displayed value and styling as much as possible.
6. The hyperlink must open in a new browser tab using `target="_blank"` and `rel="noopener noreferrer"`.
7. The hyperlink must use the corresponding workstream's Task JQL, not the Bug JQL.
8. Use proper URL encoding so spaces, quotes, parentheses, and special characters are handled correctly.
9. For missing or invalid Task JQL/Search URL, show Total Task as plain text without a broken hyperlink.
10. Ensure all existing Q426 workstreams and newly registered workstreams use the same behavior.
11. Preserve existing Task counts, Pass Rate calculations, defect tables, refresh behavior, and Auto-Publish safety checks.
12. Add focused tests for correct workstream-to-JQL mapping, URL encoding, missing configuration, and link rendering.
13. Keep the implementation lightweight. Avoid unnecessary dependencies or refactoring.

## Safety

- Do not commit private `query-config.local.md`.
- Do not expose credentials, tokens, or authentication headers.
- Do not hardcode real Task JQL into source code or test fixtures.
- Do not execute a real refresh, commit, or push during implementation.

## Deliverables

Report:
- Files changed
- How the dedicated JQL is mapped to each workstream
- Jira Search URL format
- Whether the URL exposes JQL in committed files
- Test results
- Any configuration or security decision required

After implementation, wait for user review before publishing.
