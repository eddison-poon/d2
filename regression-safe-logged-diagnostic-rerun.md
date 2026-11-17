# Regression Auto-Publish — Safe Logged Diagnostic Rerun

## Context
The Regression refresh diagnostics enhancement passed 58 Python and 33 Node tests. A subsequent `Refresh all Regression Test environments` request yielded no usable terminal output or exit code, so neither wrapper startup nor per-environment results were confirmed. The wrapper accepts the argument `regression`. Do not assume that an unchanged snapshot means the Bug JQL was skipped.

## Objective
Perform **one controlled diagnostic rerun** of the existing Regression Auto-Publish wrapper from the local Windows PowerShell terminal, capture its exit code and **sanitized** per-environment status, and explain whether refresh, validation, commit, or push occurred.

**Important:** This is a live operation. The wrapper may commit and push verified changes if all existing safety gates pass. Ask for explicit user approval before executing. Do not run automatically merely because this prompt is opened.

## Preflight
1. Confirm the current directory is the dashboard repository (`C:\AgentHub\Testing\agenthub-testing-dashboard-fresh`).
2. Inspect `git status --short` and ensure the working tree meets the wrapper's existing safety requirements. Do not reset, stash, discard, or auto-stage files.
3. Verify the wrapper path and its CLI syntax by reading `scripts/auto-publish-refresh.py`. Do not invent flags.
4. Verify which diagnostic lines are emitted by the current implementation. Ensure the filtering rules below match actual output. Do not print or save raw JQL/ZQL, tokens, authorization headers, private config, or tracebacks.
5. If the working tree is dirty, configuration is missing, or safe logging cannot be guaranteed, stop and report; do not run.

## Approved execution approach
After user approval, run **once** from PowerShell. This sample collects process output in memory and writes only allowlisted, sanitized lines to a timestamped log under the OS temporary directory, outside the Git repository. Review and adapt the allowlist to the current wrapper's actual fixed-format diagnostics before execution. Do not print the raw output.

```powershell
Push-Location 'C:\AgentHub\Testing\agenthub-testing-dashboard-fresh'
try {
    $log = Join-Path $env:TEMP ("agenthub-regression-" + (Get-Date -Format 'yyyyMMdd-HHmmssfff') + ".log")
    $output = @(& python -B scripts/auto-publish-refresh.py regression 2>&1)
    $code = $LASTEXITCODE

    $safe = [System.Collections.Generic.List[string]]::new()
    foreach ($item in $output) {
        $line = [string]$item
        # Only keep fixed-format, non-sensitive status labels.
        if ($line -match '^Auto-Publish:\s*(published|no_changes|refreshed_without_publish|blocked|push_failed|failed)\s*$') {
            $safe.Add("Auto-Publish: $($Matches[1])")
        }
        elseif ($line -match '^\s*(rt_(?:hk|uk)_(?:ideation|poc|prod)_v[12])\s*:\s*(SUCCESS|FAILED|UNCHANGED|UPDATED|SKIPPED|N/A)\s*$') {
            $safe.Add("$($Matches[1]): $($Matches[2])")
        }
        elseif ($line -match '^\s*(ZQL|Bug JQL|Snapshot)\s*:\s*(SUCCESS|FAILED|UNCHANGED|UPDATED|SKIPPED|N/A)\s*$') {
            $safe.Add("$($Matches[1]): $($Matches[2])")
        }
    }
    $safe.Add("Exit code: $code")
    $safe | Set-Content -LiteralPath $log -Encoding UTF8
    Write-Output "Sanitized log: $log"
    Write-Output "Exit code: $code"
    $safe
}
finally {
    Pop-Location
}
```

The allowlist is intentionally strict: missing diagnostic lines must be reported as missing, not guessed. Avoid capturing raw process output in PowerShell transcript files. Do not write an unfiltered stderr/stdout log. If actual wrapper messages differ, update the allowlist **only** to accept fixed-format status labels without free-text error content.

## Interpretation
- Distinguish **command submitted** from **wrapper started**, **collector executed**, **snapshots changed**, and **published**.
- Show ZQL, Bug JQL, and snapshot outcome per configured environment when supported by captured evidence.
- An unchanged execution dataset does not imply Bug JQL was skipped; defect-only snapshot changes should be eligible.
- If no eligible snapshots changed, report `no_changes` rather than claiming an error unless the wrapper provides contrary evidence.
- If the process produces no safe output, report that fact and the exit code; do not invent a root cause.
- Preserve all existing dirty-target protection, source validation, test gates, explicit Git staging, branch/remote checks, and push-failure handling.

## Deliverables
Report: command actually executed, whether approval was obtained, sanitized log location, exit code, per-environment statuses supported by evidence, whether any files changed, whether a commit/push happened (with Git evidence), and the smallest next action. Do not change code or run additional refreshes without a separate request.
