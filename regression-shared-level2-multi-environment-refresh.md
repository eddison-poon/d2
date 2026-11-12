# Regression Test — Shared Level 2 and Multi-Environment Refresh

## Context
Repository: `agenthub-testing-dashboard` (company GitHub repository, operated locally in VS Code Copilot).
Existing dashboard has 12 Regression Test cards: HK/UK × Ideation/PoC/Prod × v1/v2. Current Regression uses Zephyr ZQL for test cycle execution and Jira JQL for outstanding defects. An existing Regression POC has already worked. Healthcheck has six v2 cards sourced from local Cucumber report.html, and Q426 has a completed dynamic workstream registry, shared detail template, one-command registration and refresh. Preserve all of them.

## Objective
1. Migrate the 12 Regression Test Level 2 views to one reusable page: `regression_detail.html?environment=<id>`.
2. Support a single Copilot custom-agent command: **Refresh all Regression Test environments**.
3. Keep independent per-environment ZQL, JQL, verified snapshots, and failure isolation.
4. Avoid per-environment HTML modifications on subsequent refreshes.

## Phase 0 — Inspect before changing anything
- Inspect `index.html`, Regression detail HTML files, assets, data files, refresh agent instructions, README, tests, and actual local config structure.
- Identify the existing environment IDs, report keys, filenames, ZQL/JQL query format, test status vocabulary, completion calculations, defect columns, and any pagination limitations.
- Document current Level 1 and Level 2 behavior as a baseline. Do not invent environment IDs, data schema, query APIs, status mappings, or paths.
- Prefer reusing existing code conventions and shared components. Do not introduce a framework, database, server, new dependency, or network service.

## 1. Environment registry and shared Level 2
- Create a lightweight registry of all 12 existing Regression environments, preserving exact current labels, ordering, data mappings, and links.
- Create `regression_detail.html` to render any registered environment using the existing Regression Level 2 UI: execution summary, counts, completion, outstanding defects table, Jira issue hyperlinks, existing search/filter behavior where present, and Day/Night theme.
- Use a validated URL `environment` parameter and registry lookup; never concatenate an arbitrary URL value into a file path.
- Display a helpful unavailable/unknown-environment state for missing or invalid IDs.
- Level 1 cards must link to the shared page and use the same per-environment snapshots. Preserve the current number of cards and labels.
- Keep existing per-environment HTML files as compatibility redirects or wrappers during migration, if safe; do not delete them before verification. Preserve direct old bookmarks when possible.
- A verified empty result and an unqueried/failed environment must be distinguishable. Never show fabricated 0% or zero defects as a successful query.

## 2. Regression multi-environment refresh
- Extend the existing `.github/agents/testing-dashboard-refresh.agent.md` with the exact command: **Refresh all Regression Test environments**.
- Discover all 12 environments from the registry/config; do not require the user to list them individually.
- For each environment, load its own Zephyr ZQL test-cycle query and Jira JQL outstanding-bug query from the existing ignored local configuration file. Respect existing report-key conventions; do not invent or copy queries.
- Execute using existing company-approved Zephyr/Jira MCP tools and the existing agent workflow; no direct credentials in code.
- Handle pagination and deduplicate issues/executions using appropriate stable identifiers; detect truncated or incomplete results and treat them as failure, not verified zero.
- Apply the *existing validated* Zephyr execution-status interpretation and completion formula. Explicitly inspect whether Not Executed, Blocked, Failed, Passed, In Progress, etc. are included in denominators; preserve the current business definition unless the user approves a change. Do not reuse Q426 task status rules.
- For Jira defects, preserve the existing outstanding/closed status filters and defect table behavior. Ensure linked Jira IDs use the correct issue URL.
- Publish a new snapshot for an environment only when BOTH its ZQL and JQL retrievals are complete and validated. Preserve its last verified snapshot if either fails. Do not reset counts or timestamps on failure.
- A failure in one environment must not stop the remaining environments. Return a per-environment report with updated / preserved / not configured status and reasons.
- Avoid unnecessary modifications to already verified data. Preserve provenance and collection/verification timestamps where the existing format supports them.
- Keep private ZQL/JQL, credentials, and internal URLs in ignored local config. Never commit or print secrets.

## 3. Safety and compatibility
- Do not modify Healthcheck report.html parsing, Q426 registry, one-command registration, Q426 snapshots, or Q426 shared Level 2.
- Preserve Day/Night mode, sidebar navigation, Level 1 layout, existing regression KPIs, color rules, and defect links.
- Do not hand-edit 12 individual HTML pages to refresh data.
- Minimize code churn and keep static-file compatibility (including opening `index.html` locally via file:// if this is the current supported workflow).
- No commits or pushes.

## 4. Automated and manual validation
Automated tests must cover:
1. All 12 environment registry entries, labels, and mapping integrity.
2. Each Level 1 Regression card routes to the shared Level 2 with its own ID.
3. Correct environment-specific snapshot selection, no cross-environment data leakage.
4. Invalid/missing environment IDs.
5. Existing execution completion and defect-count calculations.
6. Verified zero vs N/A / unverified states.
7. Jira hyperlinks and existing defect table columns.
8. Complete pagination/deduplication, and incomplete-result handling.
9. ZQL failure, JQL failure, both failure, missing config, and snapshot preservation.
10. Isolation: other environments continue if one fails.
11. Existing Regression POC remains correct.
12. Q426 and Healthcheck remain unchanged.
13. Theme and static file routing where testable.

Run existing tests and any new focused tests. If live Jira/Zephyr access is unavailable, explicitly say so and do not claim a live refresh succeeded.

Manual checks required:
- Open HK/UK, v1/v2, and at least Ideation/PoC/Prod examples via Level 1.
- Verify shared URL, data, Jira links, sidebar, and Day/Night mode.
- Run one real known-good environment refresh first (existing Regression POC), then all configured environments when safe.
- Verify failure isolation with a controlled test or fixture, not by corrupting production configuration.

## Deliverables
- Shared Regression Level 2 HTML and minimal registry/rendering changes.
- Updated custom-agent command and any minimal refresh helper required by the existing design.
- README operator instructions and placeholders for per-environment ZQL/JQL.
- Tests and a clear implementation report:
  * files changed
  * actual environment IDs and query-key mapping
  * baseline vs post-change behavior
  * tests passed/failed/skipped
  * manual checks remaining
  * any limitations, especially Zephyr MCP pagination/status handling
  * any deviations requiring approval

**Do not commit or push. Wait for user review.**
