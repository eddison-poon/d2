# Operations Manager — Phase C2.1: Minimal Jira Preflight Enhancement

## Objective

Complete the missing read-only preflight capabilities required to validate Jira Story creation through the existing Operations Manager.

Keep the implementation lightweight, reuse the verified Jira connectivity launcher, and preserve the existing company Jira Assistant scripts.

Do not create, update, or delete Jira issues during this phase.

## Current Verified State

- Jira Search and Fetch work through `jira_assistant.py`.
- Project key `ETIVAI` has been confirmed.
- Jira Story issues exist in the project.
- Jira connectivity uses the approved exact-host routing.
- Phase C1.3 changes have been committed locally.
- Git push remains unconfirmed due to a separate proxy connectivity failure.

The existing launcher does not expose sufficient read-only capabilities to verify issue creation metadata, permissions, or assignee identity and assignability.

## Part A — Read-only Capability Investigation

Inspect the current Operations Manager repository, launcher, company Jira Assistant integration, and available Jira REST API documentation.

Determine whether the existing approved Jira REST API integration can retrieve:

1. **Create metadata**
   - Whether Story is creatable in project ETIVAI
   - Mandatory creation fields
   - Supported field values
   - Default values, where available
2. **Permissions**
   - Whether the configured Jira account has Create Issues permission in ETIVAI
   - Any relevant Assign Issues permission requirements
3. **Current-user identity**
   - Authenticated Jira username or account identifier
   - Display name
   - Identifier format expected by the existing create command
4. **Assignee validation**
   - Whether the authenticated user can be assigned to a new Story
   - Whether the existing create command accepts the verified identifier

Use only read-only Jira REST operations.

Do not assume that an existing Story proves that new Stories can be created.

## Part B — Minimal Implementation Proposal

Propose the smallest enhancement to the existing `jira_assistant.py` launcher.

Requirements:
- Reuse the approved Jira routing.
- Reuse existing authentication.
- Prefer extending the existing launcher rather than creating new scripts.
- Do not modify company Jira Assistant scripts.
- Do not introduce Jira MCP.
- Do not introduce new dependencies.
- Do not change system-wide proxy settings.
- Do not expose credentials.
- Preserve Search, Fetch, Create, and Update behavior.

Only propose read-only capabilities that are necessary for the current E2E validation.

Explain the exact files, commands, and REST endpoints involved.

**Stop and request approval before modifying any files.**

## Part C — Implementation and Verification (After Approval Only)

After explicit approval:
1. Implement only the approved read-only capabilities.
2. Run existing launcher tests.
3. Verify the new capabilities against Jira using the approved routing.
4. Confirm that existing Search and Fetch still work.
5. Confirm no Jira issues were created or modified.
6. Report unsupported endpoints or permission restrictions without inventing workarounds.

Do not automatically commit or push changes.

## Part D — Complete Phase C2 Preflight (After Approval Only)

Use the following target Story:
- Project: ETIVAI
- Issue Type: Story
- Summary: [TEST] PT TPM upper limit issue
- Description: Validate Jira ticket creation, duplicate checking, read-back verification, and reporting through Operations Manager.
- Assignee: My verified Jira account
- Sprint: Optional, omitted
- Epic: Optional, omitted

Once mandatory fields, create permissions, and assignee identity are verified, perform the previously requested duplicate searches.

Search for exact and similar summaries within ETIVAI.

Report matching issues and clearly state any pagination limitations.

Prepare an exact ticket preview.

If a likely duplicate is found, stop and request a decision.

## Mandatory Approval Gates

**Approval Gate 1 — Implementation**

Present the proposed launcher enhancement and wait for approval before changing repository files.

**Approval Gate 2 — Jira Creation**

Even after the enhancement is implemented and preflight succeeds, do not create a Jira Story.

Present the final ticket preview and wait for separate, explicit creation approval.

## Expected Output for This Run

A. Existing Capability Assessment
B. Supported Jira REST Read-only Endpoints
C. Proposed Minimal Launcher Changes
D. Security and Compatibility Considerations
E. Verification Plan
F. Approval Required Before Implementation

## Restrictions

- No Jira MCP.
- No Jira write operations.
- No Git push or commit during this investigation.
- No changes to company Jira Assistant scripts.
- No new dependencies unless separately approved.
- No unrelated refactoring.
- Preserve the existing lightweight Markdown-first architecture.

Stop after presenting the implementation proposal.
