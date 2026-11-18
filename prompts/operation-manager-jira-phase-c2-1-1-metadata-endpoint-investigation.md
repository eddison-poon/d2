# Operations Manager — Phase C2.1.1: Jira Creation Metadata Endpoint Investigation

Proceed with Phase C2.1.1 — Jira Creation Metadata Endpoint Investigation.

The Phase C2.1 implementation passed 34 no-write tests, but the live preflight failed because GET `/rest/api/latest/issue/createmeta` returned HTTP 404.

Please:

1. Investigate the Jira deployment type and API version using existing company Jira Assistant references and approved read-only requests.
2. Identify the supported REST endpoint for retrieving Story creation metadata in project ETIVAI.
3. Determine whether the 404 is caused by an unsupported endpoint, API version, URL construction, or another identifiable issue.
4. Use only approved Jira connectivity routing and existing authentication.
5. If appropriate, test specific documented candidate endpoints using read-only GET requests.
6. Report the working endpoint and evidence, or explain why no supported endpoint could be confirmed.
7. Propose the smallest necessary change to the existing preflight implementation.

## Restrictions

- No Jira MCP.
- No Jira ticket creation or modification.
- Do not modify company Jira Assistant scripts.
- Do not modify repository files yet.
- Do not commit or push.
- Do not change proxy, credentials, or TLS settings.

Stop after reporting findings and the proposed fix. Wait for my approval before implementation.
