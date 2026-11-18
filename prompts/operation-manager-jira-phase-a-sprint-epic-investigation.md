# Operations Manager — Phase A: Sprint and Epic Investigation

Investigate how the existing company Jira Assistant scripts can support Sprint and Epic assignment without using Jira MCP.

## Architecture Decision
- Use the existing company Jira Assistant scripts and Jira REST API.
- Do not use Jira MCP.
- Do not introduce new MCP dependencies.
- Preserve the lightweight Operations Manager architecture.
- Prefer existing company-supported tools over custom implementation.

## Investigation
1. Inspect the company Jira Assistant skill and its available scripts.
2. Identify existing commands for creating, updating, searching, and reading Jira issues.
3. Determine whether Sprint and Epic can be assigned during creation or through a subsequent update.
4. Identify the actual Jira field IDs, supported REST endpoints, and required permissions where verifiable.
5. Determine how to verify Sprint and Epic after assignment.
6. Identify whether the company scripts already provide the necessary capabilities.
7. Recommend the smallest reliable implementation approach.

## Expected Output
A. Available Script Commands
B. Sprint Assignment Feasibility
C. Epic Assignment Feasibility
D. Recommended Create → Assign → Verify Workflow
E. Gaps and Risks
F. Proposed Minimal Changes for Phase C

## Restrictions
- Read-only investigation.
- No Jira write operations.
- No repository modifications.
- No new scripts or dependencies.
- No Jira MCP.
- Do not assume unsupported script capabilities exist.
- Clearly distinguish verified capabilities from assumptions.

Do not begin implementation. Wait for my approval.
