# Q426 One-Command Workstream Registration — Copilot Implementation Prompt

## Context
The agenthub-testing-dashboard repository already has Q426 dynamic Level 1 cards, a registry (`data/q426_registry.js`), a shared Level 2 template (`q426_detail.html?workstream=<id>`), and a refresh workflow. Existing workstreams: AgentOps (`agentops`), Builder and Runtime (`builder_runtime`), and Monitoring (`monitoring`). Monitoring was validated with real Jira results. Preserve the existing behavior and verified snapshots.

## Objective
Support the following natural-language command through the existing VS Code Copilot custom agent:

`Add Q426 workstream: <name>`

Make this a repeatable, safe, minimal-change workflow for 8–10 more workstreams. Retain:

`Refresh all Q426 workstreams`

## Required behavior

1. Parse the display name; derive a stable lowercase snake_case ID (e.g. `Security Operations` → `security_operations`). Validate nonempty names, ID syntax, and collisions. Never overwrite an existing entry. If an existing workstream matches, explain and stop without modifying files. Avoid ambiguous or unsafe IDs.
2. Inspect actual registry, refresh script, local config format, README, and tests before editing. Reuse the implemented architecture; do not assume undocumented schema fields or invent a new framework.
3. Register a new workstream using the registry's existing format. Preserve ordering and all existing entries. Create the per-workstream data file only as required by the current design. An unrefreshed workstream must show an explicit unavailable/unverified state (N/A), not a misleading verified 0% or zero defects. Never fabricate Jira data, timestamps, or query results.
4. Read Task JQL and Bug JQL only from the existing ignored local configuration. If either is absent, explain exactly where and how to configure it, without making up JQL or copying another workstream's queries. Registration may be completed safely, but do not run Jira queries or publish verified results for that new workstream until both JQLs are present.
5. When both JQLs are present, run the existing Q426 refresh mechanism, preserving pagination, deduplication, completion status rules (Done/Closed/Resolved case-insensitively), verified zero-task N/A completion, verified zero-bug count 0, and per-workstream failure isolation. Publish each workstream's snapshot only after both queries succeed and validate; otherwise retain its last verified snapshot.
6. Ensure the new card appears in Level 1 and opens `q426_detail.html?workstream=<id>`. Do not create an individual Level 2 HTML page or hardcode the card in `index.html`. Do not change shared rendering code unless a demonstrated defect requires it; explain such changes before making them.
7. Update `.github/agents/testing-dashboard-refresh.agent.md` with a concise, discoverable instruction for `Add Q426 workstream: <name>`, including missing-JQL handling and idempotency. Retain the existing refresh command. A small helper script is acceptable only if it makes repeated registrations safer and fits current repo conventions; avoid dependencies and unnecessary abstractions.
8. Update README with a short operator workflow and configuration example using placeholders only. Never expose private JQL, Jira credentials, or internal URLs in tracked files.
9. Add focused automated tests for: new registration, duplicate/no-op, invalid name/ID, missing Task JQL, missing Bug JQL, safe unverified N/A state, existing workstream preservation, correct routing, and no unintended Healthcheck/Regression changes. Test refresh failure isolation where applicable.
10. Do not modify Healthcheck parsing, Regression ZQL/JQL logic, or unrelated sections. Preserve Day/Night mode and existing Q426 links/data.

## Suggested verification
- Dry-run registration with a temporary test name, if safe and reversible; do not pollute production registry or snapshots. Prefer isolated test fixtures or temp directories.
- Confirm the three existing workstreams and Monitoring real data remain intact.
- Run the repository's existing test commands; report counts and any skipped tests.
- Show `git status` and changed-file summary. Check that ignored local configuration is not staged/tracked.

## Output to user
Report:
- Whether the one-command workflow is ready
- Files changed and why
- Exactly how to use the new command
- Missing-JQL behavior
- Test results
- Any manual UI checks still needed
- Any limitation or deviation from configuration-only registration

**Do not commit or push. Wait for user review.**
