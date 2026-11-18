# Operations Manager — Phase C1: Jira Operational Readiness (Read-only)

## Updated business decision
Sprint and Epic are **optional**. Tickets may be created before they are scheduled or linked to an Epic. The user can add Sprint and Epic manually during later ticket review. Missing Sprint/Epic must NOT block ticket creation, and the agent must never claim those fields were assigned.

## Architecture
- Use the existing company Jira Assistant scripts and Jira REST API only.
- Do not use Jira MCP or introduce new dependencies.
- Keep the lightweight Markdown-first Operations Manager workflow.

## Read-only investigation
1. Identify the configured Jira site, project key, and relevant issue types without exposing secrets.
2. Verify read-only connectivity and permissions with existing approved tools.
3. Inspect the implemented create, update, search and fetch commands, their accepted fields, and limitations.
4. Check whether duplicate searches are project-scoped, reliable, and paginated; note the current default result limit of 8.
5. Review preview/approval requirements and how an agent avoids accidental or duplicate ticket creation.
6. Determine which supported fields can be read back after creation and how to verify them.
7. Optionally report whether Sprint/Epic can be set later, but do not spend implementation effort on them or make them prerequisites.
8. Recommend a safe, minimal Phase C2 end-to-end validation: search for duplicates -> preview -> explicit user approval -> create -> fetch -> verify -> report partial failures. Do NOT run it yet.

## Deliverables
A. Site, project, and connectivity findings (live-verified vs inferred)
B. Create / Search / Update / Fetch capability table
C. Duplicate prevention and pagination gaps
D. Preview and approval safeguards
E. Supported-field read-back verification
F. Minimal Phase C2 test plan and readiness blockers
G. Optional Sprint/Epic notes (non-blocking)

## Restrictions
- Read-only Jira requests only; no create, update, comment, or other writes.
- Do not modify repository files.
- Do not use Jira MCP.
- Do not reveal credentials or tokens.
- Do not guess site-specific configuration or field IDs.
- If connectivity is blocked, report the blocker rather than claiming verification.
- Wait for explicit approval before any Phase C2 write operation.
