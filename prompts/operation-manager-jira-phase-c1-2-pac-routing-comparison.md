# Operations Manager — Phase C1.2: PAC Routing Comparison

The Jira website works in my browser, but the company Jira Assistant Python script fails with a proxy tunnel 503 or timeout.

Current Python proxy: `intpxy1.hk.hsbc:8080`

Windows browser uses a configured PAC URL.

## Tasks
1. Identify the configured Windows PAC URL without displaying sensitive information.
2. Determine whether the approved PAC configuration specifies DIRECT or PROXY routing for the Jira hostname.
3. Compare that routing decision with Python's effective HTTPS_PROXY and NO_PROXY settings.
4. Identify whether the current Python proxy is inconsistent with the approved browser route.
5. Recommend the smallest approved configuration change needed for Python to use the correct route.
6. If an approved route is confirmed, propose a temporary, process-scoped read-only test. Request my approval before changing any environment settings or executing that test.

## Restrictions
- No Jira MCP.
- No Jira writes.
- No repository changes.
- Do not modify system-wide proxy settings.
- Do not bypass corporate proxy or security controls.
- Do not disable TLS verification.
- Do not expose proxy credentials, tokens or secrets.
- Do not assume DIRECT is permitted merely because it appears in PAC.
- Stop if the approved route cannot be established.

## Output
A. Browser PAC Route
B. Python Current Route
C. Routing Difference
D. Recommended Approved Fix
E. Verification Plan

Wait for my approval before applying changes.
