# Operation Manager — Jira Capability Review

I want to resume development of the existing Copilot Operations Manager, focusing exclusively on Jira operations.

Before making any changes, inspect the current repository, agent instructions, Markdown skills, and Jira MCP integration.

**Read-only review: do not modify files or execute Jira write operations.**

## 1. Current Architecture
Explain:
- Files and folders used by Operations Manager
- Available agent instructions and skills
- How Copilot invokes Jira MCP tools
- Required configuration and prerequisites

## 2. Available Jira Operations
For every currently supported operation, provide purpose, Copilot invocation, required and optional inputs, expected result, and known limitations. Distinguish implemented functionality from planned functionality.

## 3. Jira Ticket Creation
Review project, issue type, summary, description, assignee, sprint, epic, labels, priority, and duplicate detection. Explain how each is populated, whether supported, and implementation gaps.

## 4. Usage Examples
Provide five practical Copilot prompts grounded in verified repository capabilities. Include ticket creation, lookup, and bulk operations only if supported.

## 5. Improvement Opportunities
Prioritize P0/P1/P2 improvements for ticket creation reliability, sprint/epic assignment, duplicate prevention, simpler prompts, execution feedback, and fewer unnecessary MCP calls.

## 6. Final Output
A. Current Architecture
B. Available Jira Commands
C. Step-by-Step Usage Guide
D. Known Issues and Limitations
E. Recommended Improvements
F. Suggested Next Steps

Constraints:
- Read-only; no code or Jira changes
- No new scripts or dependencies
- Preserve lightweight, Markdown-first architecture
- Mark verified findings versus assumptions
- Exclude Confluence and Dashboard scope

Goal: understand the current implementation before selecting improvements.
