# Regression Auto-Publish Diagnostic — Partial Configuration Preflight

## Context
A previous read-only preflight stopped because 7 of 12 Regression Test environments had neither ZQL nor Bug JQL configured. Five environments are configured. Missing configuration in the other seven is expected; it must not block diagnostics or refresh of the configured environments.

## Task for Copilot
Continue the Regression Auto-Publish diagnostic investigation, correcting **only the diagnostic preflight interpretation**. Do not assume the Regression collector or publisher implementation is defective.

### Updated preflight rules
1. Confirm the working directory is the Agent Hub Testing Dashboard repository and Git working tree is clean.
2. Configured environments: eligible for refresh using the existing collection, validation, and Auto-Publish workflow.
3. Unconfigured environments: skip, report as UNCONFIGURED/SKIPPED, and preserve existing snapshots without modification.
4. Do not require all 12 Regression environments to have ZQL and JQL configured.
5. Preserve environment-level failure isolation. A failed source must not be misreported as unchanged.
6. Preserve all snapshot validation, dirty-target protection, test gates, explicit staging, branch/remote synchronization, and push-failure handling.
7. Do not modify source code, dashboard UI, snapshots, or private query configuration for this diagnostic.
8. Review the PowerShell sanitized-logging command from `regression-safe-logged-diagnostic-rerun.md` against the **actual** wrapper output format. Log only fixed-format, allowlisted status fields and exit code to a local temporary file outside the Git repository. Do not print or save raw JQL/ZQL, credentials, tokens, authorization headers, tracebacks, or other sensitive free text.

### Execution approval
**Stop and request explicit user approval before executing** one live `python -B scripts/auto-publish-refresh.py regression` diagnostic run. This wrapper can commit and push verified changes if its existing safety gates pass. Do not run it before approval, and do not rerun automatically.

### Deliverables
Report all 12 environments as configured or unconfigured and, for configured ones, the evidence-backed ZQL, Bug JQL, snapshot, and publication outcomes (successful, failed, unchanged, updated, or unknown as appropriate). Include process exit code, sanitized diagnostic log path, whether any files changed, and Git evidence of any commit/push. Do not invent results when output is missing.

The objective is to observe the existing workflow with partial configuration, not to bypass its protections.
