# Q426 Dynamic Workstream Architecture v2 — Implementation Prompt

Implement a configuration-driven Q426 dashboard architecture in the current `agenthub-testing-dashboard` repository.

## Objective

Replace the existing one-HTML-per-workstream design with a single reusable Level 2 page:

`q426_detail.html?workstream=<id>`

Enable adding new Q426 workstreams without creating new HTML pages or manually modifying dashboard rendering logic.

## 1. Shared Level 2 Template

- Create `q426_detail.html`.
- Reuse the existing Q426 Level 2 design and Day/Night mode.
- Read the workstream ID from the URL.
- Load the corresponding workstream data using a validated registry.
- Dynamically render the title, task execution summary, completion percentage, and outstanding defects.
- Preserve the existing four-column defect table: Priority, Jira ID, Assignee, Summary.
- Make Jira IDs clickable using their existing issue URLs.
- Show a clear error for an unknown or missing workstream ID.
- Do not construct arbitrary file paths from URL parameters.

## 2. Configuration-driven Workstream Registry

Introduce a lightweight workstream registry with stable IDs, display names, and data file mappings.

Initially register:
- `agentops` — AgentOps
- `builder_runtime` — Builder and Runtime

Design the registry so additional workstreams can be added without editing HTML.

## 3. Dynamic Level 1 Cards

- Generate Q426 cards from the registry.
- Each card links to `q426_detail.html?workstream=<id>`.
- Preserve existing RAG thresholds, completion calculations, defect counts, and unavailable-data behavior.
- Automatically update the displayed workstream count.
- Keep existing Healthcheck and Regression Test cards unchanged.

## 4. Configuration-driven JQL Refresh

Extend the existing Q426 refresh workflow to discover all configured workstreams.

Each workstream must support independent:
- Task JQL
- Bug JQL
- Data output file
- Last verified snapshot

Preserve the existing rules:
- Done / Closed / Resolved count as completed tasks, case-insensitively.
- Other statuses count as incomplete.
- Zero verified tasks produce N/A completion.
- Zero verified bugs produce 0 outstanding defects.
- Query failures must preserve the last verified snapshot.
- Pagination and Jira issue deduplication remain mandatory.
- A workstream must only publish updated data after both Task and Bug queries validate successfully.
- One failed workstream must not prevent other workstreams from refreshing.

Keep private JQL and Jira connection settings in `query-config.local.md`. Do not commit this file.

## 5. Refresh Agent

Update `.github/agents/testing-dashboard-refresh.agent.md` to support the command:

**Refresh all Q426 workstreams**

The agent must discover the configured workstreams and refresh each one without requiring individual workstream names in the prompt.

Document how to add a new workstream by editing only the necessary configuration.

## 6. Migration and Backward Compatibility

- Migrate the existing AgentOps and Builder and Runtime cards to the shared Level 2 template.
- Preserve their verified data and existing Jira hyperlinks.
- Do not delete the original Level 2 HTML files until the new implementation has been validated.
- Do not modify Healthcheck Cucumber parsing or Regression ZQL/JQL logic.
- Preserve Day/Night mode throughout.

## 7. Validation

Verify:
1. AgentOps opens the shared Level 2 with correct data.
2. Builder and Runtime opens the same HTML with its own data.
3. Existing Jira hyperlinks work.
4. Unknown workstream IDs display an appropriate error.
5. A new test workstream can be registered without creating another HTML file.
6. The new workstream appears automatically on Level 1.
7. Refresh processes all configured workstreams.
8. Failed queries preserve verified snapshots.
9. Existing Q426 metrics remain unchanged.
10. Healthcheck and Regression Test remain unaffected.
11. Existing JavaScript tests pass.
12. Day/Night mode works on both levels.

Reuse existing components and keep dependencies minimal.

Report all modified files, test results, and any manual verification required.

**Do not commit or push until reviewed.**
