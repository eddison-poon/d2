# Deep RCA — Gemini 3.5 Flash Latency Comparison: UK vs HK

## Background

Gemini 3.5 Flash is accessible through Agent Hub in two environments:
- **UK:** Approximately 50 seconds response time.
- **HK:** Approximately 15 seconds response time.
- **Observed difference:** Approximately 35 seconds (UK is 3.33× slower).

We need a thorough, evidence-based investigation to identify the causes of this significant performance difference. Do not assume the Gemini model itself is responsible.

## Investigation Inputs

- UK GCP Project: `<UK_PROJECT_ID>`
- HK GCP Project: `<HK_PROJECT_ID>`
- UK Execution Correlation / Query Name: `<UK_IDENTIFIERS>`
- HK Execution Correlation / Query Name: `<HK_IDENTIFIERS>`
- Investigation Time Window: `<START_TIME> – <END_TIME, TIMEZONE>`
- Model: Gemini 3.5 Flash (verify exact provider model ID and version)
- Workload: `<SAME_PROMPT_AND_AGENT_CONFIGURATION_IF_APPLICABLE>`

If multiple executions are available, compare several representative successful requests from both environments rather than relying on a single execution.

## Objective

Determine exactly where UK accumulates approximately 35 additional seconds compared with HK.

Identify whether the difference originates from:
1. LLM provider processing or token generation.
2. LLM endpoint location, routing or regional availability.
3. Network latency between Agent Hub and the LLM endpoint.
4. Agent Runtime / Executor / Orchestrator overhead.
5. Gateway, proxy, service mesh or MCP operations.
6. Infrastructure configuration, resource contention, scaling or queuing.
7. Different model configuration, token consumption or retry behavior.

## Phase 1 — Establish a Fair Comparison

1. Verify exact model ID, version, provider, endpoint and API method in both environments.
2. Confirm whether prompts, system instructions, agent definitions, tools, attachments and generation settings are identical.
3. Compare input/output tokens, reasoning/thinking tokens where reported, context size and response lengths.
4. Identify streaming versus non-streaming.
5. Check additional agent steps, tool calls, retries and fallback models.
6. Distinguish cold starts from warm executions.
7. Compare load conditions.

If workloads differ, explain why direct comparison is misleading. The display name "Gemini 3.5 Flash" does not prove identical underlying model deployments.

## Phase 2 — End-to-End Execution Reconstruction

Reuse this repository's existing observability runbooks, Cloud Logging correlation methodology and execution replay tools where appropriate.

For both UK and HK:
1. Locate complete executions using validated correlation_id, query_name, execution_id, request_id, trace_id and related identifiers.
2. Reconstruct Agent Hub → Orchestrator → Agent Runtime → Executor → LLM Gateway → provider and response path.
3. Extract start/end timestamps and explicit duration fields for major operations.
4. Identify queuing, retries, tool discovery, MCP execution, memory calls and response finalization.
5. Detect missing events, ambiguous correlations and incomplete logging.
6. Compare equivalent operations side by side.

Do not add overlapping child durations or attribute observation gaps to services without evidence.

## Phase 3 — Gemini Provider Latency

Compare:
- Executor-to-Gateway latency.
- Gateway request preparation and queueing.
- Gateway-to-provider request initiation.
- Time to First Token (TTFT), if observable.
- Streaming duration and inter-token delays.
- Time to last token / provider completion.
- Gateway response processing.
- Retries, backoff, throttling, timeouts and fallback routing.
- Provider status/errors.
- Input/output/thinking token counts and generation throughput (tokens/sec) where measurable.

Determine whether UK is slower before first token, during generation or after provider completion. Distinguish gateway-observed latency from provider-internal processing when provider timings are unavailable.

## Phase 4 — LLM Location and Regional Routing (High Priority)

Determine:
1. GCP project and deployment region.
2. Agent Runtime/GKE cluster region.
3. LLM Gateway region.
4. Actual Gemini API endpoint hostname and configured location.
5. Vertex AI regional, multi-regional or global endpoint usage.
6. Differences in UK/HK endpoint configuration.
7. Cross-region traffic.
8. Provider routing/regional capacity evidence.
9. Egress/proxy/service mesh differences.
10. Whether the exact model/version supports the configured endpoint location.

Do not infer physical inference location from hostname alone. Separate configured endpoint, observed destination and actual inference location. Mark provider-side inference location Unknown unless verified. Do not claim overload without evidence.

## Phase 5 — Network and Infrastructure Analysis

**Network:** gateway-to-provider round-trip latency; DNS, connection and TLS timings where logged; keep-alive/HTTP2/connection reuse; NAT, proxy, firewall and service mesh overhead; cross-region hops.

**Infrastructure:** GKE/node region; gateway/executor/orchestrator replicas; CPU/memory requests and limits; HPA/scaling; restarts, OOM, CPU throttling, scheduling delays; queue depth/concurrency/saturation; connection pool limits; software/config/deployment revisions.

Use approved read-only logs, traces, metrics and inspection tools. No intrusive tests or infrastructure modifications.

## Phase 6 — Comparative Latency Breakdown

Produce a side-by-side table:

| Stage | UK Duration | HK Duration | Difference | Evidence |
|---|---|---|---|---|
| Request acceptance | | | | |
| Orchestration | | | | |
| Executor initialization | | | | |
| LLM Gateway overhead | | | | |
| Provider TTFT | | | | |
| Token generation | | | | |
| MCP / Tool operations | | | | |
| Response finalization | | | | |
| Total E2E | | | | |

Only report evidenced durations. Highlight largest measured differences. Calculate contribution to the ~35-second difference only for comparable, non-overlapping stages. Keep unattributed intervals separate. Do not fabricate a residual by subtracting overlapping child durations.

## Phase 7 — Statistical Validation

If enough executions exist, compare at least 5–10 representative successes per environment, preferably more. Calculate median, mean, P95, min/max (qualify small samples); TTFT, tokens/sec, token counts; outliers, retries, cold starts, prompt sizes and output lengths. Determine whether the UK slowdown is consistent or time-dependent. Report sample sizes.

## Phase 8 — Root Cause Analysis

Classify each hypothesis as:
- **Confirmed:** directly evidenced.
- **Probable:** multiple supporting observations, incomplete proof.
- **Possible:** plausible but unverified.
- **Unknown:** insufficient evidence.

Rank suspected causes by their ability to explain the latency delta. For each, give evidence, measured impact if available, confidence, missing evidence and recommended verification/corrective action. Distinguish immediate bottleneck from underlying cause.

## Final Deliverables

Generate a readable, standalone local HTML report under `reports/` with:
1. Executive Summary — why UK is slower than HK.
2. Environment and Configuration Comparison.
3. UK vs HK Execution Timelines.
4. Visual Latency Breakdown and Difference Chart.
5. Gemini Model and Token Usage Comparison.
6. LLM Endpoint Geography and Routing Analysis.
7. Network and Infrastructure Findings.
8. Statistical Comparison (if sufficient data).
9. Root Cause Ranking with Evidence and Confidence.
10. Conclusions and Recommended Actions.
11. Data Coverage, Unknowns and Limitations.

Prominently answer: **"Where are the additional ~35 seconds spent, and what evidence explains the difference?"**

Provide concise findings in Copilot Chat and the local HTML path.

## Execution Rules

- Read-only investigation, explicit UK/HK GCP project IDs.
- Reuse colleague repository observability runbooks, tools and correlation rules.
- Do not modify GCP resources, IAM, APIs or deployments.
- No load tests without approval, no new dependencies.
- Do not modify or commit repository files except writing the requested local HTML report; do not automatically push it.
- Never expose sensitive prompts, credentials or raw payloads.
- Report telemetry/access limitations honestly.
- Do not impose the lightweight investigator's 200-record/two-query budget on this deep investigation.
- Keep queries time-bounded and avoid unnecessary full-project dumps.
- Start with one matched UK/HK pair, then expand to representative samples where possible.
