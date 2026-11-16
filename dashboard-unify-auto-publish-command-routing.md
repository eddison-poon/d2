# Unify Auto-Publish Command Routing for All Dashboard Modules

## Objective

Ensure all three Dashboard modules automatically execute the existing Refresh → Validate → Commit → Push workflow, regardless of whether the user includes the word "all" in the refresh command.

## Supported Commands

Q426:
- Refresh all Q426 workstreams
- Refresh Q426 workstreams

Regression:
- Refresh all Regression Test environments
- Refresh Regression Test environments

Healthcheck:
- Refresh all Healthcheck environments
- Refresh Healthcheck environments

All six commands must invoke the existing Auto-Publish wrapper.

## Confirmed Root Cause

The previous Healthcheck refresh bypassed Auto-Publish. The agent ran `scripts/refresh-healthcheck.py --write` directly, which updates snapshots locally but does not commit or push. General agent instructions require `scripts/auto-publish-refresh.py healthcheck` for the exact "Refresh all Healthcheck environments" command, while Healthcheck-specific instructions contradict this by directing the agent to the collector and saying "Never commit or push automatically." The user omitted "all" in the request, which contributed to ambiguous routing. Q426 and Regression successfully published when using the wrapper.

Two Healthcheck snapshots are currently modified locally and must be preserved for separate recovery:
- HK Ideation v2: 44 total, 43 passed, 1 failed, 97.7% Pass Rate.
- HK PoC v2: 44 total, 41 passed, 3 failed, 93.2% Pass Rate.

## Implementation Requirements

1. Inspect `.github/agents/testing-dashboard-refresh.agent.md` and identify conflicting refresh instructions.
2. Remove or correct any instructions that allow the six supported commands to bypass Auto-Publish.
3. Specifically resolve the Healthcheck instruction that calls `scripts/refresh-healthcheck.py --write` directly and says "Never commit or push automatically."
4. Route all six commands through `scripts/auto-publish-refresh.py` using the correct module argument.
5. Keep the underlying collectors available for explicitly requested local-only operations, but never use them directly for the six supported commands.
6. Ensure command matching is case-insensitive and tolerant of harmless punctuation and whitespace differences.
7. Preserve existing snapshot validation, Python/Node test gates, Git safety checks, and failure handling.
8. Update README documentation to show all six supported commands.
9. Add automated tests verifying that all six commands resolve to the correct Auto-Publish workflow and that no conflicting agent instructions remain.
10. Keep implementation minimal. Do not modify dashboard UI, metrics, snapshot data, or private query configuration.

## Important Safety Constraints

- Do not bypass dirty-snapshot protection.
- Do not force push, reset, stash, or discard local changes.
- Do not automatically stage unrelated files.
- Do not execute a real refresh, commit, or push during implementation.

## Deliverables

Report:
- Root cause and conflicting instructions corrected.
- Files changed.
- Routing test results.
- Python and Node test results.
- Confirmation that all six command variants use Auto-Publish.

This task fixes future command routing only. Preserve the two existing dirty Healthcheck snapshots for separate recovery.
