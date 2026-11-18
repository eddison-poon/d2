# Operations Manager — Phase C1.3: Persistent Jira Connectivity Fix

## Objective
Implement a reliable, persistent, Operations Manager-specific Jira connectivity solution using the previously approved and successfully tested exact-host routing.

The existing temporary test succeeded when the Jira hostname was appended to NO_PROXY in a child process.

## Requirements
1. Inspect the existing Operations Manager agent, Jira Assistant integration, and execution configuration.
2. Recommend the smallest persistent solution that ensures all Jira Assistant commands use the approved routing:
   - Search
   - Fetch
   - Create
   - Update
3. Prefer an Operations Manager-specific execution configuration rather than Windows system-wide environment changes.
4. Preserve all existing proxy settings and NO_PROXY exclusions.
5. Apply the exact-host exception only to the verified Jira hostname.
6. Ensure the configuration works across new VS Code sessions without requiring manual setup.
7. Keep the solution lightweight and maintainable. Avoid new dependencies or unnecessary scripts.
8. Do not modify the company Jira Assistant skill or its Python scripts unless absolutely necessary.
9. Do not use Jira MCP.

## Implementation Process

### Step 1 — Review
Inspect the current execution environment and propose the smallest persistent solution.

Explain:
- Files or settings requiring changes
- How the routing will be applied
- How other services remain unaffected
- How the configuration persists across sessions

Present the proposed changes and wait for my approval.

### Step 2 — Implementation
After approval:
- Apply only the agreed configuration changes.
- Preserve existing settings.
- Do not modify system-wide proxy settings.
- Do not expose credentials or tokens.
- Do not disable TLS verification.

### Step 3 — Verification
After implementation:
- Start a fresh execution context.
- Verify the effective Jira routing.
- Execute a read-only Jira search.
- Fetch an existing Jira issue.
- Confirm both operations succeed.
- Verify that unrelated proxy settings remain unchanged.

## Expected Output
A. Proposed Solution
B. Files / Configuration Changes
C. Implementation Result
D. Read-only Verification Results
E. Remaining Risks
F. Phase C2 Readiness

## Restrictions
- No Jira write operations.
- No Jira MCP.
- No system-wide proxy changes.
- No new dependencies unless explicitly approved.
- No credentials or secrets in repository files.
- No changes before approval.
- Do not claim success without a fresh read-only verification.

Wait for approval before implementation.
