# Copilot Prompt — Clarify Jira Launcher Instruction Scope in Multi-root Workspace

## Objective
Resolve ambiguous Jira execution instructions between two repositories in the same VS Code multi-root workspace, using the smallest justified instruction-only change.

## Workspace context
- Primary repository: `copilot-operations-manager`
- Additional workspace folder: `agenthub-testing-dashboard-fresh`
- Operations Manager currently uses `scripts/jira_assistant.py` as its Jira launcher.
- The Dashboard has a separate, established Q426 refresh agent and collector; its batch command is `scripts/auto-publish-refresh.py q426`.
- A Q426 refresh succeeded in this workspace on November 19, 2026, but a later Copilot session declined to start it because a broadly worded Operations Manager repository rule said “For Jira” use the launcher.
- Earlier investigation found an old, untracked Dashboard refresh agent copy inside Operations Manager that could also cause agent-selection confusion.
- The launcher requirement appears to be a repository-specific workflow convention, not a company-wide security mandate; **verify this from available repository evidence rather than assuming an exemption**.

## Tasks
1. Inspect the Operations Manager repository rules, agent instructions, README, and Dashboard refresh agent instructions. Record exact relevant file paths and instruction wording.
2. Check whether the launcher requirement is a repository-specific convention and whether any organization-wide requirement or higher-priority instruction actually governs Dashboard Jira access.
3. **Only if the intended scope is confirmed:** minimally clarify Operations Manager's repository instructions so its launcher requirement applies to **Operations Manager Jira operations**, not automatically to unrelated folders merely because they share a VS Code workspace.
4. Clearly state that Dashboard refresh tasks are governed by the Dashboard repository's own applicable instructions and established authorized workflow. Do not assert that any confirmed higher-priority or organization-wide policy is exempted.
5. Preserve the launcher requirement unchanged for Operations Manager work. Avoid changing the Dashboard's runtime/collector architecture.
6. Identify the older Dashboard agent copy in Operations Manager and explain whether it is obsolete; do not delete or modify that copy without separate approval.
7. Show a concise before/after instruction diff and explain why it resolves the scope ambiguity.

## Strict constraints
- **Instruction files only**; no Python, JavaScript, JQL, snapshots, credentials, query configuration, refresh wrappers, or tests unless strictly needed to validate instruction text.
- No new Jira access route and no bypass of security or authorization controls.
- Do not run Jira queries, Dashboard refreshes, or live connectivity checks.
- Do not commit or push.
- If the scope cannot be established from available evidence, **stop without modifying files** and report the unresolved question for owner confirmation.
- Preserve Q426, Healthcheck, and Regression as independent refresh workflows.

## Deliverables
- Exact files inspected and files changed
- Source evidence supporting the intended instruction scope
- Before/after wording (minimal diff)
- Any remaining ambiguity or obsolete agent-copy risk
- Confirmation that no code, configuration, snapshots, queries, commit, or push were changed

Stop after reviewable local instruction changes. Wait for approval before any live Q426 refresh.
