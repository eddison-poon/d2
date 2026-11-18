# PoC — Performance Load vs GCP Resource Utilization Analysis

## 1. Objective

Analyze **one Agent Hub performance test in one environment**, consisting of five planned load stages:
- Stage 1: 400 requests per 5 minutes
- Stage 2: 800 requests per 5 minutes
- Stage 3: 1,200 requests per 5 minutes
- Stage 4: 1,600 requests per 5 minutes
- Stage 5: 2,000 requests per 5 minutes

Correlate request-level response-time data with GCP resource metrics, investigate scaling and saturation, and produce an evidence-based, standalone HTML report. This is a read-only PoC.

## 2. Investigation Inputs

- Environment: `<ENVIRONMENT>`
- GCP Project: `<PROJECT_ID>`
- GKE Cluster: `<CLUSTER_NAME>`
- Cluster Region / Zone: `<REGION_OR_ZONE>`
- Test Start Time: `<YYYY-MM-DD HH:MM:SS HKT>`
- Performance Raw Data: `<CSV_FILE_PATH>`

### Raw data definition

The CSV contains **Elapsed Time** and **Response Time**.

**Elapsed Time is the request START offset relative to the overall performance-test start.** It is not request duration or completion time.

- Request Start Timestamp = Test Start Time + Elapsed Time
- Request Completion Timestamp = Request Start Timestamp + Response Time

Validate CSV headers, time units, missing values and time zone before processing. Use optional status/query/error fields if present; do not assume missing status means success.

### Actual load-stage boundaries — user-provided

**The user will provide all five actual stage start/end times or offsets.** Stage durations can vary and gaps may exist.

| Stage | Planned Load | Actual Start Offset or Timestamp | Actual End Offset or Timestamp |
|---|---|---|---|
| 1 | 400 requests / 5 min | `<START_1>` | `<END_1>` |
| 2 | 800 requests / 5 min | `<START_2>` | `<END_2>` |
| 3 | 1,200 requests / 5 min | `<START_3>` | `<END_3>` |
| 4 | 1,600 requests / 5 min | `<START_4>` | `<END_4>` |
| 5 | 2,000 requests / 5 min | `<START_5>` | `<END_5>` |

Confirm whether supplied boundaries are elapsed offsets or absolute timestamps and normalize accordingly. Validate ordering, overlaps, gaps and time zone. **Never assume five continuous five-minute intervals. Never infer exact boundaries from target rates.** If any required boundary is absent or ambiguous, request it before stage-level attribution.

Keep target load separate from measured achieved throughput. For variable-duration stages, report both actual request count and normalized requests per five minutes.

## 3. Repository and GCP Capability Assessment

Work within the existing `etiv-sre-observability` repository where possible.

1. Inspect existing observability tools and runbooks.
2. Verify approved read-only GCP Cloud Monitoring metric access and GKE resource visibility.
3. Confirm project/cluster identifiers, available metric types, labels and sampling intervals.
4. Prefer existing repository tooling and approved Cloud Monitoring API access.
5. Do not assume Cloud Logging access implies Cloud Monitoring access.
6. If metrics are inaccessible, clearly identify the blocker and smallest necessary permission/tooling change; do not fabricate values.

Do not install dependencies or modify repository source.

## 4. Performance CSV Processing

For each request:
1. Read elapsed offset and response duration.
2. Validate and normalize units.
3. Calculate absolute request start and completion times.
4. Assign stage by **request start timestamp** using supplied actual stage boundaries.
5. Label requests outside defined stages separately.

For each stage calculate:
- Target requests / 5 min
- Actual request count
- Actual stage duration
- Achieved RPS and normalized requests / 5 min
- Average, median, P95, P99 and maximum response time
- Error count/rate only if status is available

Include requests started in a stage even if they complete after its end. Avoid treating client-observed response time as measured server-side processing time. State percentile sample counts.

## 5. GCP Resource Metrics Collection

Retrieve time series spanning warm-up (if known), all five actual stages, inter-stage gaps, and a short cooldown where available.

Prioritize:
- **CPU:** usage in cores, utilization relative to CPU requests and limits (where available), throttling.
- **Memory:** working set/usage, requests, limits, utilization relative to limits, memory pressure.
- **GKE:** running pods, desired replicas/HPA events where available, restarts, OOM.
- **Optional:** network, node resource usage, queues, service-level errors.

Identify actual relevant Agent Hub deployments/services (e.g., runtime, orchestrator, LLM gateway, MCP gateway, resource service) rather than assuming all exist.

Differentiate cluster/node/pod/container/deployment metrics. Shared cluster resource use must not be attributed automatically to this test.

## 6. Time Alignment and Data Integrity

Normalize timestamps internally to UTC and display in HKT. Preserve metric type, monitored-resource type, unit, labels, aggregation method, alignment period and coverage.

Use consistent time axes. Do not fill missing samples with zero or silently interpolate. Do not sum utilization percentages across pods. Distinguish CPU cores from percentage relative to requests or limits. Disclose aggregation and sampling resolution. Avoid claiming finer temporal precision than Cloud Monitoring provides.

## 7. Stage-by-Stage Analysis

For each actual stage, where coverage permits:
- Average/peak CPU usage
- Average/peak memory usage
- Average/max running pod count
- Scaling events
- Actual throughput
- Average/P95/P99 response time

Compare consecutive stages (1→2, 2→3, 3→4, 4→5). Identify services with largest CPU/memory growth, scaling lag, latency increases, saturation signals and throughput plateaus.

Label gaps as transition/idle/unknown only when supported by evidence. **Exclude inter-stage gaps from active-stage averages** while retaining them on full-duration graphs.

## 8. Correlation and Bottleneck Assessment

Compare:
- CPU saturation vs P95 latency
- Memory pressure vs latency
- HPA/pod scaling vs achieved throughput
- CPU throttling, OOM/restarts and errors
- Performance degradation at high load

Rank up to three potential bottlenecks with evidence and confidence: Confirmed, Probable, Possible or Unknown.

Correlation is not proof of causation. Consider other cluster workloads, LLM provider latency, downstream dependencies and request-mix changes. Use targeted read-only logs/traces only where existing tooling supports validation; do not expand into unrelated deep RCA.

## 9. Standalone HTML Report

Create `reports/performance-resource-utilization-<ENV>-<TIMESTAMP>.html` locally, self-contained and usable offline without external dependencies.

Include:

### A. Executive Summary
Environment, start/end, five stages, total observed requests, latency statistics, resource findings and bottleneck candidates.

### B. Actual Load Profile
Actual throughput over time, with user-provided stage start/end boundaries and visible gaps; distinguish planned from achieved load.

### C. CPU Over Time
Per-service CPU cores and appropriately defined utilization; annotate stage intervals.

### D. Memory Over Time
Per-service working set/usage, requests/limits where available; annotate stage intervals.

### E. Pod Count and Scaling
Running pods, desired replicas/HPA events where available, against stage changes.

### F. Response Time Over Time
Time-bucketed mean/P95 and P99 where sample sizes suffice; show bucket sizes/counts.

### G. Stage Comparison
Target vs achieved throughput, actual stage duration, response-time stats, CPU, memory, pod metrics.

### H. Bottleneck Analysis
Evidence, confidence, competing explanations and limits.

### I. Data Coverage
Project/cluster, CSV row count, metric types, units, alignment periods, missing samples, stage-boundary validation, caveats.

All time-series charts share a consistent time axis. Shade/annotate actual load stages and gaps. Use separate charts for CPU, memory, pods, throughput and response time; avoid incompatible mixed units. Hover details where practical. Do not invent data.

## 10. PoC Success Criteria

Determine whether:
1. CSV request timestamps are reconstructed correctly.
2. Approved GCP metrics can be retrieved.
3. All five supplied stage boundaries align accurately.
4. CPU/memory/pods can be graphed over time.
5. Latency and throughput can be correlated with resources.
6. Evidence-backed saturation/scaling candidates can be identified.
7. The workflow can be reused.

State limitations and smallest practical changes needed if any criterion fails.

## 11. Constraints

- Read-only; exactly one environment and one test.
- No infrastructure, IAM or deployment changes.
- No new dependencies or repository source modifications.
- No automatic commits or pushes.
- No fabricated metrics, timestamps or stage boundaries.
- Avoid unrelated investigations.
- Generate local report and only necessary intermediate analysis artifacts.
- Sanitize sensitive data.

## 12. Final Copilot Chat Output

1. Test duration and total observed requests.
2. Five-stage planned vs achieved throughput and latency summary.
3. CPU/memory trends.
4. Pod scaling observations.
5. Top three potential bottlenecks and confidence.
6. Missing metrics/data limitations.
7. Local HTML report path.

**Core question:** As planned load increased from 400 to 2,000 requests per five minutes, how did GCP resource utilization and response latency change across the **user-supplied actual stage intervals**, including gaps, and which services showed saturation or delayed scaling?
