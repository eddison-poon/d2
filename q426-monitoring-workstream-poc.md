# Q426 Dynamic Workstream POC — Add Monitoring

We have completed the Q426 Dynamic Workstream Architecture v2 implementation.

The existing AgentOps and Builder and Runtime cards have passed manual UI verification.

Now perform the first real configuration-driven workstream registration.

## New Workstream

- Display Name: Monitoring
- Workstream ID: `monitoring`
- Section: Q426
- Detail URL: `q426_detail.html?workstream=monitoring`
- Task JQL: Read from local configuration
- Bug JQL: Read from local configuration

## Instructions

1. Inspect the current Q426 workstream registry and the existing local configuration format.
2. Register the Monitoring workstream using the existing configuration-driven mechanism.
3. Follow the documented configuration structure. Do not introduce a new architecture.
4. Do not invent or reuse JQL from other workstreams.
5. If Monitoring Task JQL or Bug JQL is missing, report the missing configuration and stop before running Jira queries.
6. Never overwrite existing verified snapshots with empty, fabricated, or incomplete results.
7. Once both JQL queries are configured, execute the existing "Refresh all Q426 workstreams" workflow.
8. Verify that Monitoring appears automatically on Level 1 and opens the shared Level 2 template.
9. Confirm Monitoring's Task Execution Summary and Outstanding Defects are derived from its own Jira results.
10. Verify AgentOps and Builder and Runtime remain unchanged except for legitimate refresh updates.
11. Confirm Healthcheck and Regression Test remain unaffected.
12. Run the existing automated tests.

## Constraints

- Do not create `q426_monitoring.html`.
- Do not manually hardcode a Monitoring card in `index.html`.
- Do not modify shared rendering logic unless a genuine architecture defect is discovered.
- Keep private JQL and Jira settings in the ignored local configuration file.
- Do not expose private JQL in committed files or test fixtures.
- Do not install dependencies.
- Do not commit or push.

## Output

Report:
- Files changed
- Configuration entries added
- Monitoring registration status
- Jira query results, if available
- Automated test results
- Whether adding Monitoring required any HTML or JavaScript changes
- Any blockers or manual verification needed

Wait for review before commit or push.

## Execution sequence

**First run:** Register Monitoring and identify any missing local JQL. Do not query Jira until both queries are configured.

**Second run (after local JQL configuration):** `Refresh all Q426 workstreams`

The key POC acceptance criterion is that Monitoring can be added without editing `index.html`, `q426_detail.html`, or shared rendering logic. Registry/configuration changes are expected.
