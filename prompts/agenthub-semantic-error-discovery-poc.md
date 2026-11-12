# PoC — Agent Hub Semantic Error Discovery

## Objective

Evaluate whether the existing observability agent can proactively discover Agent Hub executions that returned HTTP 200 at the transport layer but contained application-level errors in the response content.

This is a read-only Proof of Concept using a historical performance-testing window.

Do not require predefined Query Names or Execution IDs.

## Input

- Environment: UK
- GCP Project: Resolve from existing repository configuration
- Start Time: `<YYYY-MM-DD HH:MM HKT>`
- End Time: `<YYYY-MM-DD HH:MM HKT>`
- Error Codes of Interest: 400, 401, 403, 408, 429, 500, 502, 503, 504
- Execution Type: Agent Hub requests

## Phase 1 — Log Discovery

1. Review existing repository observability runbooks and available log correlation patterns.
2. Identify Agent Hub execution completion logs, response content fields, structured errors and related microservice logs.
3. Search the entire specified time window using bounded, paginated queries.
4. Identify executions where the outer HTTP response is 200 but the application-level result contains error evidence.
5. Include structured error fields, tool errors, provider errors and final agent response errors.
6. Avoid treating arbitrary occurrences of error-code numbers in user prompts or normal explanations as failures.
7. Report missing logging coverage and query truncation.

## Phase 2 — Execution Correlation

For each candidate failure, retrieve:

- Environment
- Tenant Name / Tenant ID
- Query Name
- Execution ID
- Correlation ID / Request ID
- Execution Timestamp
- Outer HTTP Status
- Embedded Error Code
- Sanitized Error Message
- Originating Microservice, if identifiable
- Final Execution Outcome
- Number of related error events

Use existing repository correlation and replay capabilities where useful.

Do not perform full deep RCA for every execution.

## Phase 3 — Error Classification

Classify each execution as:

**User-visible Failure**
The final response contains an unresolved application-level error.

**Recovered Error**
An internal error occurred but the execution subsequently recovered successfully.

**Suspected Error**
Error evidence exists, but the final user-visible outcome cannot be verified.

For each classification, provide evidence and confidence.

Deduplicate repeated error logs belonging to the same execution.

## Phase 4 — Error Analysis

Group results by:

- Error Code
- Tenant
- Microservice
- Error Category
- Final Outcome

Identify the most frequent error signatures and affected tenants.

For 1–3 representative failures, perform a short targeted investigation to identify likely originating services.

Do not assume every HTTP 429 is a rate-per-minute limit; distinguish token quota, rate limits and other provider restrictions using evidence.

## Phase 5 — Reports

Generate:

1. Standalone HTML Summary
2. CSV containing execution-level error records

HTML sections:

- Investigation Scope
- Total Executions Inspected
- Confirmed User-visible Failures
- Recovered Errors
- Suspected Errors
- Error Code Distribution
- Affected Tenants
- Error Details Table
- Key Findings
- Data Coverage and Limitations

CSV should contain one row per execution/error signature, not one row per raw log entry.

## PoC Validation

Report:

1. Whether the agent can discover errors without supplied Query Names.
2. Whether Tenant Name and Query Name can be recovered.
3. Whether final HTTP 200 and embedded application errors can be distinguished.
4. Whether error classifications are supported by evidence.
5. Whether the approach is suitable for recurring four-hour monitoring.
6. Estimated execution time, log-query count and operational limitations.

## Constraints

- Read-only GCP access.
- No infrastructure or IAM changes.
- No new dependencies.
- No repository source modifications.
- No automatic Git commits or pushes.
- Only create local HTML and CSV reports.
- Sanitize sensitive response content.
- Keep log queries time-bounded.
- Do not claim complete discovery if logs are sampled, truncated or missing.
- Do not schedule recurring execution yet.

## Final Output

Provide a concise PoC result in Copilot Chat, including:

- Number of executions inspected
- Number of confirmed and suspected failures
- Number of affected tenants
- Most common error codes
- Discovery coverage and limitations
- HTML and CSV report paths

Conclude whether the existing observability approach is feasible for four-hour automated semantic error monitoring.
