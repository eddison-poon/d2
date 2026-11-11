# GCP Performance Investigator — Final RCA Prompt

Run a v1.3 Extended Performance Investigation.

## Input
- Environment: UAT
- Query Name: `<QUERY_NAME>`
- Start Time: `<YYYY-MM-DD HH:MM HKT>`
- End Time: `<YYYY-MM-DD HH:MM HKT>`

## Instructions
1. Follow the latest gcp-performance-investigator v1.3 skill.
2. Use read-only GCP Cloud Logging queries with the configured UAT project.
3. Identify the correct correlation ID, request ID, execution ID and trace ID where available. Do not assume these identifiers are interchangeable.
4. Use Adaptive Time Slicing to collect all relevant records throughout the specified time window. Automatically split capped intervals and deduplicate records. Do not stop at the initial 200-record limit.
5. Reconstruct the execution flow across microservices, from request initiation to final completion.
6. Identify measured durations for each microservice and operation, including LLM, MCP tools, memory, gateway and executor where evidence exists.
7. Produce a Latency Breakdown showing:
   - Total execution duration
   - Top five slowest measured child operations
   - Microservice/operation duration comparison
   - Individual percentage relative to total execution time
   - Major unattributed observation gaps
   - Evidence and confidence levels
8. Identify errors, retries, timeouts and potential root causes. Distinguish confirmed causes from hypotheses.
9. Use one targeted follow-up query for major unexplained latency when justified (Option B).
10. Generate a standalone HTML RCA report under `reports/`, containing:
    - Executive Summary
    - Execution Timeline
    - Visual Latency Breakdown
    - Microservice Performance Analysis
    - Error and Retry Analysis
    - Root Cause Analysis
    - Conclusion
    - Data Coverage and Confidence

## Important Rules
- Keep the investigation focused and efficient.
- Do not run unrelated repository analysis.
- Do not add overlapping child durations together.
- Do not classify observation gaps as confirmed service processing time.
- Do not claim a root cause without supporting evidence.
- If multiple executions share the query name, identify them separately and do not merge their timelines.
- Do not modify GCP resources.
- Do not commit or push repository files.

## Final Output
Provide a concise RCA summary in Copilot Chat and the local path to the generated HTML report.
