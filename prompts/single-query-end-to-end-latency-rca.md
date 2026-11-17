# Deep RCA — Single Query End-to-End Latency & Tool Execution Breakdown

## Objective

Perform a comprehensive, evidence-based Root Cause Analysis (RCA) for **one Agent Hub query execution in one environment**.

Reconstruct the complete execution lifecycle, from initial request acceptance to final response completion.

Determine:
1. What happened throughout the execution?
2. Which microservices and components participated?
3. What operations were performed, and in what order?
4. How long did each operation take?
5. Which LLM models, tools, MCP servers and external services were invoked?
6. How long did each individual tool invocation take?
7. Where was the majority of execution time spent?
8. Were there errors, retries, timeouts, queues or unexplained delays?
9. What is the most likely cause of excessive latency?

Deliver a detailed visual HTML report with execution timelines and latency breakdowns.

## Investigation Input

- Environment: `<ENVIRONMENT>`
- GCP Project: Resolve from existing repository configuration
- Query Name: `<QUERY_NAME>`
- Start Time: `<YYYY-MM-DD HH:MM HKT>`
- End Time: `<YYYY-MM-DD HH:MM HKT>`

Optional:
- Correlation ID: `<CORRELATION_ID>`
- Execution ID: `<EXECUTION_ID>`
- Tenant Name: `<TENANT_NAME>`

Use Query Name as the initial discovery identifier. If multiple executions share it, distinguish by IDs/timestamps; analyze only the requested execution. Ask if ambiguous. Do not investigate unrelated queries or environments.

## Phase 1 — Execution Discovery and Correlation

Reuse existing observability runbooks, correlation rules, execution replay and analysis capabilities.

1. Identify the initial incoming request.
2. Locate correlation_id, request_id, execution_id and trace_id where available.
3. Identify tenant, agent and execution attempt.
4. Trace related events across microservices using validated identifiers.
5. Determine earliest reliable request-acceptance and final response/completion timestamps.
6. Identify missing lifecycle events and incomplete coverage.

Do not assume identifiers are interchangeable or correlate unrelated events solely by time proximity.

## Phase 2 — End-to-End Execution Timeline

Reconstruct chronological flow across components actually observed, potentially:
- API Gateway / Request Gateway
- Tenant Runtime API
- Agent Manager / Controller
- Agent Runtime / Orchestrator
- Executor / Agent Framework
- LLM Gateway / Provider
- MCP Gateway / MCP Servers
- Memory / Redis
- Sandbox / Workspace
- External APIs / tools
- Response finalization

For every significant event, extract start/end timestamps, microservice, operation, call ID, measured duration, status, parent operation, evidence reference and confidence. Distinguish sequential, parallel and nested operations.

## Phase 3 — Detailed Latency Breakdown

Calculate validated total end-to-end duration. Break down, where evidenced:
1. Request acceptance/routing
2. Agent initialization
3. Planning/orchestration
4. LLM processing
5. Tool discovery/initialization
6. Tool/MCP execution
7. Memory
8. Sandbox
9. Retry/backoff/queueing
10. Response preparation/finalization

| Stage | Service | Start | End | Duration | % of E2E | Confidence |
|---|---|---|---|---|---|---|

Percentages are **individual comparisons** against E2E, not additive shares. Do not sum overlapping/nested children or double-count parent durations. Do not fabricate boundaries or treat log gaps as measured service time. Identify observation gaps separately. Use stacked charts only for verified non-overlapping intervals. Identify top five measured child operations.

## Phase 4 — LLM Call Breakdown

Identify every observed LLM invocation and, where available:
- Sequence, caller, provider and exact model ID
- Configured endpoint and region
- Start/end, measured latency, TTFT and generation duration
- Input/output/thinking tokens
- Streaming mode
- Retries, provider errors/status
- Associated agent steps/tool calls

Produce a per-call table. Mark missing TTFT, token counts or provider-internal duration Unknown. Do not infer inference geography from hostname.

## Phase 5 — Tool and MCP Execution Breakdown (High Priority)

Identify **every observable tool invocation**, including tool discovery, server initialization, dispatch, individual MCP calls, external APIs, sandbox/workspace operations, retries and failures.

For each invocation show:
- Sequence and tool name
- MCP server
- Calling agent/component
- Start/end timestamps and measured duration
- Success/failure/timeout
- Retry count
- Parent/call identifier
- Evidence reference

Where measurable, separate discovery, initialization, gateway dispatch, actual tool execution and response processing. Otherwise show the measured outer tool-call duration and label inner stages Unknown.

For repeated tools, show **each invocation separately** plus aggregate by tool name/server:
- Observable invocation count and unique tool count
- Failed and retried calls
- Slowest single tool invocation
- Cumulative tool duration where aggregation is valid
- Elapsed wall-clock tool activity, separately from summed concurrent call durations

Do not silently omit unknown tool names/durations.

## Phase 6 — Errors, Retries and Delays

Investigate HTTP 4xx/5xx, application errors inside HTTP 200, provider/MCP failures, timeouts, retries/backoff, gateway issues, resource exhaustion, queueing and unexplained intervals.

For each issue report timestamp, service/operation, category, sanitized message, recovery, measurable latency impact, final outcome, evidence and confidence. HTTP 200 alone does not prove business success.

## Phase 7 — Bottleneck and RCA

Identify:
1. Slowest measured operation
2. Slowest LLM invocation
3. Slowest tool invocation
4. Largest unattributed observation gap
5. Retries/errors contributing to latency
6. Sequential operations explaining elapsed time

Classify conclusions as Confirmed, Probable, Possible or Unknown. Separate immediate bottleneck from underlying root cause. Never claim an uninstrumented observation gap is a confirmed microservice bottleneck.

## Phase 8 — Standalone HTML RCA Report

Create `reports/single-query-latency-rca-<ENV>-<TIMESTAMP>.html` locally.

Include:
1. **Executive Summary:** environment, query, sanitized execution ID, tenant, outcome, E2E latency, main finding, confidence.
2. **End-to-End Execution Timeline:** chronological Gantt-style visualization of validated sequential, parallel and nested activity, with timestamps and duration.
3. **Latency Breakdown:** stage and microservice/operation durations, top five measured child operations, individual comparison charts and separate observation gaps.
4. **LLM Call Analysis:** every observed invocation, per-call latency, TTFT, tokens, retries and errors.
5. **Tool / MCP Call Breakdown:** complete observable invocation list with server, per-call timing/status, slowest/repeated tools and discovery/initialization overhead.
6. **Error and Retry Analysis:** errors, retry sequence, recovery and measurable impact.
7. **Bottleneck Analysis:** evidence-backed latency attribution versus unknown intervals.
8. **Root Cause and Conclusion:** confirmed findings, probable causes, unknowns and at most three next actions.
9. **Data Coverage:** project, time window, sources, query count, records, missing/capped data, correlation confidence and limitations.

Use clean responsive offline HTML with no external dependencies. Sanitize sensitive data; do not embed credentials, access tokens, prompts or raw response payloads.

## Constraints

- Exactly one execution and one environment.
- Explicit GCP project; approved read-only logs/traces/metrics.
- Reuse existing repository observability capabilities.
- No infrastructure/IAM/API/deployment changes, load tests or new dependencies.
- No repository source changes; no automatic commits or pushes.
- Keep queries bounded to this execution; avoid broad project dumps.
- Do not impose the lightweight investigator's 200-record/two-query cap.
- If telemetry is missing, continue with available evidence and document limitations.

## Final Copilot Chat Output

1. Total E2E latency and final outcome.
2. Top five measured child operations.
3. LLM call count and measured durations.
4. Observable tool count and slowest tool.
5. Largest unexplained observation gap.
6. Likely bottleneck and confidence.
7. Local HTML report path.

**Core question:** From initial request acceptance to final response, what happened, which tools were called, and where was the execution time spent?
