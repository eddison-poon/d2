# Healthcheck Multi-Environment Rollout v2 — Copilot Prompt

Implement Healthcheck Multi-Environment Rollout v2 in the current Agent Hub Testing Dashboard repository.

## Objective
Upgrade the successful HK PoC v2 Cucumber Healthcheck POC into a reusable single-command refresh workflow for all six v2 Healthcheck environments. Preserve Day/Night Mode, Regression Test, and Q426.

## 1. Healthcheck Level 1
Show exactly six v2 cards: HK Ideation, HK PoC, HK Prod, UK Ideation, UK PoC, UK Prod. Remove all six v1 Healthcheck cards and their sidebar links; retain historical v1 files.

All six cards must show the same fields: Pass Rate, Failed Scenarios, RAG progress bar. Unavailable data must display N/A for both fields and a neutral grey bar. Do not show old Execution Completion or Outstanding Defects labels on Healthcheck cards. RAG thresholds: green >=90%, amber >50% and <90%, red <=50%.

## 2. Healthcheck Level 2
Standardize all six v2 pages: Total, Passed, Failed, Execution Completion, and a Failed Scenarios table with Feature and Scenario columns. Reuse the successful HK PoC v2 implementation. Missing data displays N/A and an empty-state message, never fabricated zeros. Preserve Day/Night Mode.

## 3. Local Configuration
Extend inputs/query-config.local.md with separate Cucumber HTML report paths for each of the six v2 environments. Preserve Regression ZQL/JQL configuration. Never commit local configuration, source reports, credentials, or private endpoints. Document placeholder-only configuration in README.

## 4. Refresh Agent
Upgrade .github/agents/testing-dashboard-refresh.agent.md to support this exact command:

Refresh all Healthcheck environments

The agent must:
1. Read all six Healthcheck configurations.
2. Check each report path for configuration and accessibility.
3. For available reports, reuse the working HK PoC v2 Cucumber parsing approach.
4. Extract executed Scenario and Scenario Outline results.
5. Validate Total, Passed, Failed, and other statuses against the report summary.
6. Calculate Pass Rate and Execution Completion independently.
7. Extract Feature and Scenario names for failed results.
8. Update the corresponding data/hc_*.js only after validation succeeds.
9. Preserve the last verified snapshot if a configured report fails validation, and report the error.
10. Leave unconfigured environments N/A if no verified snapshot exists.
11. Continue with other environments even when one fails.
12. Output a final summary table: environment, source availability, total, passed, failed, pass rate, update status.

Never fabricate data. Do not commit or push automatically.

## 5. Compatibility
Keep Regression ZQL/JQL and Q426 unchanged. Preserve data-file names and architecture. Keep implementation lightweight, without Python frameworks or unnecessary dependencies. Share Healthcheck rendering logic across six Level 2 pages.

## 6. Validation
Verify HK PoC v2 retains validated Cucumber results; HK Ideation v2 can refresh independently when its report arrives; UK v2 shows N/A without reports; no HC v1 cards remain in Level 1; all six HC v2 Level 2 pages share the layout; Day/Night Mode works; Regression and Q426 are unaffected; JavaScript syntax checks pass.

Inspect existing code before edits and reuse working components. Report modified files and validation outcomes. Do not commit or push until reviewed.
