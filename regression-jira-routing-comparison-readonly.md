# Regression Refresh — Jira Bug JQL Routing Comparison (Read-Only)

## Objective
Determine whether the intermittent Jira Bug JQL connection failures in Agent Hub Testing Dashboard share the same proxy-routing mechanism previously diagnosed and resolved for Operations Manager. Use existing safe diagnostics; do not assume the causes are identical.

## Verified context
- Operations Manager's company Jira Python helper previously failed with proxy CONNECT 503/timeouts, while browser PAC selected DIRECT for the Jira host.
- Its approved launcher applies an exact-host NO_PROXY exclusion in a child process, preserving parent environment and other proxy settings; authenticated Jira search/fetch and Story creation/read-back subsequently succeeded.
- The Regression dashboard's Jira Bug JQL collector uses a company Python helper and urllib; Zephyr ZQL uses a separate PowerShell transport.
- Prior Regression results: five configured environments had Bug JQL NETWORK failures; HK PoC v2 separately had a Zephyr pagination validation failure. Seven environments are unconfigured.
- Existing dashboard instrumentation added allowlisted network and pagination diagnostics. A prior prompt named regression-controlled-read-only-live-diagnostics.md describes a safe single-run diagnostic.
- A previously successful Regression run does not establish the cause of later failures.

## Phase 1 — Read-only inspection (no live requests yet)
1. Confirm the active workspace is the intended agenthub-testing-dashboard repository. Inspect actual scripts and current working-tree status. Preserve pre-existing edits.
2. Inspect the current Regression Bug JQL execution chain, including collector, company Jira helper invocation, environment inheritance, proxy handling, timeouts, and safe diagnostic output. Inspect only necessary portions of the Operations Manager launcher as a reference, if available.
3. Compare routing behavior, not secrets: whether the Jira hostname uses the explicit HTTPS proxy or an approved exact-host bypass; whether child-process NO_PROXY is inherited; whether the same Jira host and helper are used. Do not display private hostnames, proxy addresses, PAC URLs, credentials, JQL/ZQL, tokens, or raw config.
4. Distinguish confirmed routing evidence from hypotheses. A shared helper or NETWORK classification alone does not prove the same proxy failure.
5. Verify the existing Regression collector's exact read-only live invocation and confirm it cannot write snapshots, modify code, publish, commit, or push. Do not invent flags. If safe non-writing execution cannot be established, STOP and report findings without a live request.

## Phase 2 — One controlled read-only diagnostic run
Only if the existing collector's non-writing behavior is proven:
1. Execute exactly ONE existing live read-only diagnostic collection for the five configured Regression environments, with no automatic retries. Skip all seven unconfigured environments.
2. Report for each configured environment: Zephyr ZQL status; Jira Bug JQL status; allowlisted failure category/subtype; and whether the routing hypothesis is supported, contradicted, or unresolved.
3. For HK PoC v2, separately report the sanitized pagination check identifier and numeric evidence already supported by the collector. Do not weaken completeness checks.
4. Keep diagnostics in memory or a sanitized temporary location outside the repository. Never persist raw stdout/stderr, queries, URLs, payloads, exception text, secrets, or private config.
5. Compare Git status before and after; report unexpected modifications without reverting them.

## Phase 3 — Recommendation only
- If evidence confirms a proxy-routing mismatch, propose the smallest Operations-Manager-style *dashboard-specific child-process* solution for the Jira Bug JQL path, subject to corporate authorization. Preserve other hosts, proxy settings, credentials, TLS checks, and the independent Zephyr path.
- Do NOT copy the launcher blindly, globally modify NO_PROXY, assume DIRECT is authorized for a new execution context, or change system proxy settings.
- If the failure is timeout, authentication, TLS, service availability, or unknown, propose a narrowly scoped next investigation instead.
- Keep HK PoC v2 pagination as a separate issue with its own evidence and recommendation.
- Do not implement any fix in this run.

## Hard restrictions
- No Jira MCP; no Jira writes.
- No refresh, snapshots, publishing, Auto-Publish, commits, pushes, code/config edits, or changes to Q426/Healthcheck.
- No new dependencies or speculative refactoring.
- No automatic retry and no unsafe raw diagnostic logs.
- Stop if approved routing or safe read-only behavior is uncertain.

## Output
A. Workspace and Git baseline
B. Jira routing comparison: Operations Manager vs Regression
C. Five-environment sanitized live results (or reason the run was stopped)
D. HK PoC v2 pagination findings (separate)
E. Confirmed cause vs remaining uncertainties
F. Smallest recommended fix and exact files that would change, **proposal only**
G. Git after-status and confirmation that no data, source, config, or Jira issues were changed

Stop and wait for explicit approval before implementation or any production refresh.
