# Copilot Prompt — Owner Confirmation: Jira Launcher Instruction Scope

As the workflow owner, I confirm the intended repository-specific scope:

1. The Jira Assistant launcher requirement applies to `copilot-operations-manager` Jira operations only.
2. `agenthub-testing-dashboard-fresh` has its own independent Dashboard Refresh workflow and should follow its own repository instructions.
3. Sharing the same VS Code multi-root workspace does not extend Operations Manager-specific conventions to the Dashboard repository.
4. All applicable organization-wide security and authorization requirements remain in effect.

Please implement the smallest instruction-only clarification proposed in your investigation.

Expected minimal wording change in Operations Manager repository rules (retain the existing launcher command verbatim):

Before:
```text
For Jira, invoke the existing company Jira Assistant through ...
```

After:
```text
For Operations Manager Jira operations, invoke the existing company Jira Assistant through ...
```

If appropriate, add one concise sentence directing Dashboard refresh tasks to their own repository instructions and authorized workflow, subject to applicable higher-priority requirements.

Constraints:
- Do not modify Python, JavaScript, JQL, snapshots, or refresh wrappers.
- Do not delete or change the older Dashboard agent copy yet.
- Do not run Jira queries or any refresh.
- Do not commit or push.
- Do not weaken any applicable organization-wide policy.
- Keep Q426, Healthcheck, and Regression refresh workflows independent.

Show the exact diff and report the files changed. Stop for review.
