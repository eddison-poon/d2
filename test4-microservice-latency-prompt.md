# Test 4 — Microservice Latency Attribution

Continue the previous UAT performance investigation.

Goal: Identify which microservice or operation consumed the most execution time.

Focus on:
- The 18,496 ms `latency_ms` measurement
- The 17.778-second observation gap
- The previously discovered `correlation_id` and `query_name`

Tasks:

1. Identify the service, operation, `event_name`, and timestamp associated with the 18,496 ms latency.
2. Determine what `latency_ms` measures: full service request, downstream dependency call, LLM execution, MCP tool execution, internal processing, or unknown.
3. Inspect sanitized metadata around the two events bounding the 17.778-second gap.
4. Search for additional logs within that interval using the validated `correlation_id`, `trace_id`, and relevant service identifiers.
5. Look for evidence of:
   - Request received / response completed
   - Downstream call start / end
   - Queue or scheduling delay
   - LLM processing
   - MCP tool execution
   - Network or gateway waiting
6. Build a service-level latency table: Service | Operation | Start | End | Duration | Evidence | Confidence.
7. Rank the slowest operations using only supported duration measurements.
8. Explain whether the 18,496 ms latency and 17.778-second gap refer to the same operation.
9. If exact microservice duration cannot be determined, identify the most likely waiting boundary and the specific missing evidence needed.

Important:
- Do not equate adjacent log timestamps with service duration.
- Do not infer that the largest metric is the root cause.
- Do not expose sensitive log contents.
- Read-only. Do not modify GCP resources or repository files.
