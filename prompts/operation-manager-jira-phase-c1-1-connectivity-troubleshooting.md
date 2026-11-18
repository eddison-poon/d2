# Operations Manager — Phase C1.1: Jira Connectivity Troubleshooting

## Confirmed user context
- The company Jira website **opens successfully in the browser on the same computer/network**.
- The existing Jira Assistant Python search command failed with `Tunnel connection failed: 503 Service Unavailable`.
- Focus on differences between browser access and the VS Code terminal/Python process: proxy, VPN, authentication, trust certificates, and environment inheritance.
- **Assignee read-back showing display name is acceptable** for this workflow; do not prioritize changing it.
- Sprint and Epic remain optional and non-blocking.
- Use company Jira Assistant scripts and Jira REST API only; **no Jira MCP**.

## Investigation
1. Inspect existing Jira site/auth configuration and the actual Python HTTP client used by `search_jira.py`. Never display tokens or credentials.
2. Compare browser and VS Code/Python network paths at a safe, non-secret level. Browser success does not by itself prove Python proxy or authentication is configured correctly.
3. Check whether `HTTP_PROXY`, `HTTPS_PROXY`, `NO_PROXY` (and lowercase variants) are set and inherited by the relevant terminal/process. Report presence and sanitized proxy host/port only, never userinfo or passwords.
4. Check whether the script uses environment proxy settings or explicitly overrides them. Identify any corporate CA/certificate issues without disabling TLS verification.
5. Run safe, read-only connectivity checks using existing approved company tools. Distinguish DNS, proxy CONNECT/tunnel 503, TLS, HTTP authentication, authorization, and Jira service errors. Do not interpret a proxy 503 as Jira permission denial.
6. Inspect relevant Jira URL and project-key configuration for mismatches (e.g., `ETIV_AI Platform` versus `ETIVAI`) without assuming either is correct until live verified.
7. Recommend the smallest compliant fix and how to verify it using a read-only Jira fetch/search.

## Output
A. Browser vs Python Connectivity Comparison
B. Sanitized Proxy / Environment Findings
C. Most Likely Failure Point, with evidence and uncertainty
D. Minimal Recommended Fix (instructions only)
E. Read-only Verification Steps
F. Phase C2 Readiness and Remaining Blockers

## Restrictions
- No Jira MCP or new dependencies.
- No Jira writes or repository edits.
- Do not change proxy, VPN, certificates, or credentials automatically.
- Do not reveal passwords, tokens, authorization headers, or proxy URL userinfo.
- Do not bypass corporate controls or disable TLS verification.
- Stop and explain any access blocker; do not invent successful results.
- Wait for explicit approval before making changes.
