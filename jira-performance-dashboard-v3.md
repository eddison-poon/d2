# Jira Ticket — Performance Test Dashboard V3

## Summary
[Performance Test] Introduce V3 Performance Test Dashboard

## Description

### Objective
Update the performance test dashboard to support the new TPM-based capacity testing approach.

V3 focuses on identifying sustainable platform capacity and the required infrastructure configuration at different token-throughput levels.

### Scope
- Introduce V3 Level 1 dashboard for performance scenario and milestone tracking.
- Use TPM as the primary capacity measurement.
- Scenario 1 covers Simple Conversational workload from 1M to 5M TPM.
- Track milestone status as Achieved, In Progress or Not Started.
- Add Level 2 Capacity Summary for Scenario 1.
- Keep only the final selected result for each milestone in the Capacity Summary.
- Show final HPA, CPU, RAM and performance results for each TPM level.
- Allow M1–M5 selection to highlight the corresponding capacity result and sizing trend.
- Keep V2 reports separate as historical test evidence.

### Expected Result
Provide a simple management and engineering view showing platform capacity and the recommended infrastructure configuration for each TPM milestone.
