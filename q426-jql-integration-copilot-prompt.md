# Q426 JQL Integration — Copilot Implementation Prompt

Implement Q426 JQL Integration in the current **Agent Hub Testing Dashboard** repository.

## Objective
Enable a single Copilot refresh command to update both Q426 workstreams using Jira JQL for tasks and outstanding defects. Reuse the existing working dashboard architecture and refresh agent. Do not modify Healthcheck v2 or Regression Test behavior.

## 1. Scope and workstreams
There are exactly two Q426 workstreams:
- AgentOps
- Builder and Runtime

Each workstream has TWO independent, locally configured JQL queries:
1. Task JQL: all in-scope Jira tasks used to calculate completion.
2. Bug JQL: only outstanding defects for that workstream, with scope and open-status criteria defined by its JQL.

Do not hardcode real company JQL, Jira endpoints, project identifiers, credentials, or issue contents in committed files.

## 2. Task completion rules
Default completed statuses: **Done**, **Closed**, **Resolved** (case-insensitive, trim whitespace). Make this status list configurable in `inputs/query-config.local.md`.

For each workstream:
- Total Tasks = number of distinct task issues returned by the Task JQL.
- Completed Tasks = distinct returned tasks whose current status is in the configured completed-status list.
- Remaining Tasks = Total Tasks - Completed Tasks.
- Execution Completion (%) = Completed Tasks / Total Tasks * 100, rounded to one decimal for display.
- Treat a valid query with zero tasks as **N/A completion**, not 100% or 0%. Display total 0 if verified.
- Do not classify task completion based on Jira resolution alone.
- Respect the Task JQL scope; do not silently filter out issue types or statuses beyond what is configured. If the JQL returns unintended issue types, flag that as a configuration issue rather than silently altering scope.

Bug JQL is independent. Outstanding Defects = distinct bugs returned by the Bug JQL. Do not infer outstanding bugs from Task JQL or assume the task completed-status rules apply to bugs.

## 3. Level 1 Q426 cards
Preserve the two existing Q426 cards and labels:
- AgentOps
- Builder and Runtime

Show:
- Execution Completion percentage
- RAG progress bar
- Outstanding Defects count

RAG thresholds: green >=90%; amber >50% and <90%; red <=50%. Use neutral grey for unavailable or unverified data. Preserve existing Day/Night Mode and responsive layout.

## 4. Level 2 Q426 pages
Create or adapt one Level 2 page per workstream, consistent with the existing dashboard layout:
- Task Execution Summary: Total Tasks, Completed Tasks, Remaining Tasks
- Execution Completion percentage and progress bar
- Outstanding Defects table with Jira link, Priority, Jira ID, Assignee, Summary (where available)
- Search/filter defects, if supported by existing shared detail renderer
- Clear last-updated/source metadata and N/A/empty states

Use the shared styles and Day/Night Mode. Do not alter Healthcheck failed-scenarios tables or Regression details. Do not fabricate issue values, links, or counts.

## 5. Local configuration
Extend the existing ignored `inputs/query-config.local.md` using the current format and conventions. Add configuration for:
- Q426 AgentOps Task JQL
- Q426 AgentOps Bug JQL
- Q426 Builder and Runtime Task JQL
- Q426 Builder and Runtime Bug JQL
- Completed task statuses: Done, Closed, Resolved

Preserve all existing Healthcheck report paths and Regression queries. Ensure `query-config.local.md` stays ignored by Git. Document only placeholder examples in README or a tracked sample config; do not overwrite the real local config.

## 6. Copilot refresh agent
Extend `.github/agents/testing-dashboard-refresh.agent.md` to support the exact command:

**Refresh all Q426 workstreams**

Use the existing company Jira assistant skill / Jira MCP integration already available in the workspace, following its documented conventions. Avoid adding new dependencies or custom API clients unless the existing integration genuinely cannot meet the requirements.

The agent must:
1. Read and validate both workstreams' Task and Bug JQL configurations.
2. Query Jira for each Task JQL and Bug JQL separately.
3. Handle pagination and any API page-size limits; obtain all results before calculating counts.
4. Deduplicate issues by Jira issue key; avoid double-counting.
5. Read actual issue status for task completion, and collect available defect fields.
6. Calculate task totals, completed, remaining, and completion percentage.
7. Count outstanding defects solely from the Bug JQL results.
8. Validate data integrity, counts, and issue keys before writing.
9. Update only the relevant Q426 data files using the repository's existing data conventions; make Level 1 and Level 2 consume the same source.
10. Isolate failures per workstream and per query. Do not overwrite a previously validated workstream snapshot with zero/N/A after a failed or incomplete query.
11. If Task JQL succeeds but Bug JQL fails (or vice versa), do not falsely present a fully refreshed snapshot. Prefer preserving the last validated data for the failed component, with source freshness clearly indicated; only update independently validated components if existing architecture safely supports this.
12. Leave unconfigured workstreams N/A if no validated snapshot exists.
13. Output a summary table: Workstream, Task Source Status, Total, Completed, Remaining, Completion %, Bug Source Status, Outstanding Defects, Update Status.
14. Never auto-commit or push.

Do not treat partial pagination, permission errors, malformed JQL, or missing fields as a successful zero-result query.

## 7. Validation and acceptance criteria
Inspect current repository files and the existing refresh agent before changing code. Reuse the established implementation and naming patterns.

Validate:
- Both Q426 workstreams have independent Task JQL and Bug JQL.
- Done / Closed / Resolved are counted as completed, case-insensitively.
- Other task statuses remain incomplete.
- Valid zero-task query displays N/A completion.
- Valid zero-bug query displays 0 outstanding defects.
- Missing configuration and query failures display N/A or preserve verified snapshots, not fabricated zero counts.
- Pagination, deduplication, failure isolation, and last-verified-snapshot behavior work.
- Level 1 and Level 2 use consistent data.
- RAG thresholds and Day/Night Mode work.
- Healthcheck v2 Cucumber parsing, six cards, and failed-scenarios Level 2 pages remain unchanged.
- Regression Test ZQL/JQL refresh and display remain unchanged.
- JavaScript syntax and existing tests pass; add focused lightweight tests where appropriate.

Provide the modified file list, test results, and any remaining manual verification steps. Do not commit or push until reviewed.
