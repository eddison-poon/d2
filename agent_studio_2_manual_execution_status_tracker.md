# Agent Studio 2.0 — Manual Execution Status Tracker

**Purpose:** Working status file for updating individual manual execution results and producing daily testing summaries.

**Source:** AS20 execution matrix / release scope  
**Total executions:** 111

## Status Values

Use one of: `PASSED`, `FAILED`, `BLOCKED`, `NOT EXECUTED`.

## Execution Status

| Exec ID | Execution Title | Parent MTD | Role | Status | Notes |
|---|---|---|---|---|---|
| EX-PAT-001 | Low Risk Pattern exists/identifiable | MTD-PAT-001 | Authorized pattern viewer/admin | NOT EXECUTED |  |
| EX-PAT-002 | SDLC Pattern exists/identifiable | MTD-PAT-001 | Authorized pattern viewer/admin | NOT EXECUTED |  |
| EX-PAT-003 | Pattern rule persists/inherits | MTD-PAT-002 | Authorized governance setup | NOT EXECUTED |  |
| EX-PAT-004 | Pattern rule remains effective | MTD-PAT-002 | Space Designer runtime | NOT EXECUTED |  |
| EX-GOV-001 | Can enable/disable Pattern | MTD-GOV-001 | U-TO-A | NOT EXECUTED |  |
| EX-GOV-002 | Cannot change Pattern enablement | MTD-GOV-001 | U-SO-A | NOT EXECUTED |  |
| EX-GOV-003 | Cannot change Pattern enablement | MTD-GOV-001 | U-SD-A | NOT EXECUTED |  |
| EX-GOV-004 | Cannot change Pattern enablement | MTD-GOV-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-GOV-005 | Defines permitted capability/types | MTD-GOV-002 | U-TO-A | NOT EXECUTED |  |
| EX-GOV-006 | Cannot define tenant capabilities | MTD-GOV-002 | U-SO-A | NOT EXECUTED |  |
| EX-GOV-007 | Cannot expand allowance | MTD-GOV-002 | U-SD-A | NOT EXECUTED |  |
| EX-GOV-008 | Creates Space B if in scope | MTD-GOV-003 | U-TO-A | NOT EXECUTED |  |
| EX-GOV-009 | Cannot create Space | MTD-GOV-003 | U-SO-A | NOT EXECUTED |  |
| EX-GOV-010 | Assign/change Space Owner | MTD-GOV-003 | U-TO-A | NOT EXECUTED |  |
| EX-GOV-011 | Add members/assign roles | MTD-GOV-004 | U-SO-A | NOT EXECUTED |  |
| EX-GOV-012 | Does not receive 6.3 | MTD-GOV-004 | U-TO-A | NOT EXECUTED |  |
| EX-GOV-013 | Cannot assign roles | MTD-GOV-004 | U-SD-A | NOT EXECUTED |  |
| EX-GOV-014 | Cannot assign roles | MTD-GOV-004 | U-SU-A1 | NOT EXECUTED |  |
| EX-GOV-015 | All 10 required tenants exist | MTD-GOV-005 | Tenant Owner/admin view | NOT EXECUTED |  |
| EX-GOV-016 | Required default Space exists for each tenant | MTD-GOV-005 | Tenant Owner/admin view | NOT EXECUTED |  |
| EX-GOV-017 | Required default Space protected | MTD-GOV-005 | Tenant Owner | NOT EXECUTED |  |
| EX-GOV-022 | Space prompt saves and persists | MTD-GOV-007 | U-SO-A | NOT EXECUTED |  |
| EX-GOV-023 | Precedence Pattern > Tenant > Space > Agent enforced | MTD-GOV-007 | U-SD-A | NOT EXECUTED |  |
| EX-GOV-018 | Tenant Member can view tenant configuration | MTD-GOV-006 | U-TM-A | NOT EXECUTED |  |
| EX-GOV-019 | Tenant Member cannot administer tenant | MTD-GOV-006 | U-TM-A | NOT EXECUTED |  |
| EX-GOV-020 | Existing Tenant Member can be assigned a Space role | MTD-GOV-006 | U-SO-A | NOT EXECUTED |  |
| EX-GOV-021 | Space membership cannot bypass tenant membership | MTD-GOV-006 | U-SO-A | NOT EXECUTED |  |
| EX-BLD-001 | Creates Agent from enabled Low Risk | MTD-BLD-001 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-002 | Cannot create Agent | MTD-BLD-001 | U-TO-A | NOT EXECUTED |  |
| EX-BLD-003 | Cannot create Agent | MTD-BLD-001 | U-SO-A | NOT EXECUTED |  |
| EX-BLD-004 | Cannot create Agent | MTD-BLD-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-BLD-013 | Assisted creation starts from supplied idea | MTD-BLD-005 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-014 | Focused required setup information collected | MTD-BLD-005 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-015 | One valid draft Agent created | MTD-BLD-006 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-016 | Required-field validation prevents invalid draft | MTD-BLD-006 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-017 | No unintended Agent/draft created | MTD-BLD-007 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-005 | Configure Agent | MTD-BLD-002 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-006 | Cannot configure | MTD-BLD-002 | U-TO-A | NOT EXECUTED |  |
| EX-BLD-007 | Cannot configure | MTD-BLD-002 | U-SO-A | NOT EXECUTED |  |
| EX-BLD-008 | Cannot configure | MTD-BLD-002 | U-SU-A1 | NOT EXECUTED |  |
| EX-BLD-009 | Attach approved MCP/skill | MTD-BLD-003 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-010 | Cannot attach MCP/skill | MTD-BLD-003 | U-SO-A | NOT EXECUTED |  |
| EX-BLD-018 | Tool selection and personal access setup persist | MTD-BLD-003 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-019 | Deferred credential setup does not grant usable access | MTD-BLD-003 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-011 | Cannot attach/use | MTD-BLD-004 | U-SD-A | NOT EXECUTED |  |
| EX-BLD-012 | Bypass rejected | MTD-BLD-004 | U-SD-A direct attempt | NOT EXECUTED |  |
| EX-ACC-001 | Can view, not edit/run | MTD-ACC-001 | U-TO-A | NOT EXECUTED |  |
| EX-ACC-002 | Can view | MTD-ACC-001 | U-SO-A | NOT EXECUTED |  |
| EX-ACC-003 | Can view | MTD-ACC-001 | U-SD-A | NOT EXECUTED |  |
| EX-ACC-004 | Can view | MTD-ACC-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-ACC-005 | No 6.6 from platform role | MTD-ACC-001 | U-PA | NOT EXECUTED |  |
| EX-ACC-006 | Catalogue access ≠ Agent visibility | MTD-ACC-001 | U-VR | NOT EXECUTED |  |
| EX-ACC-007 | Can edit | MTD-ACC-002 | U-SD-A | NOT EXECUTED |  |
| EX-ACC-008 | Cannot edit | MTD-ACC-002 | U-TO-A | NOT EXECUTED |  |
| EX-ACC-009 | Cannot edit | MTD-ACC-002 | U-SO-A | NOT EXECUTED |  |
| EX-ACC-010 | Cannot edit | MTD-ACC-002 | U-SU-A1 | NOT EXECUTED |  |
| EX-ACC-011 | Backend rejects edit | MTD-ACC-002 | Unauthorized direct request | NOT EXECUTED |  |
| EX-RUN-001 | Executes successfully | MTD-RUN-001 | U-SD-A | NOT EXECUTED |  |
| EX-RUN-002 | Executes successfully | MTD-RUN-002 | U-SU-A1 | NOT EXECUTED |  |
| EX-RUN-003 | View but cannot execute | MTD-RUN-003 | U-TO-A | NOT EXECUTED |  |
| EX-RUN-004 | View but cannot execute | MTD-RUN-003 | U-SO-A | NOT EXECUTED |  |
| EX-RUN-005 | Platform admin ≠ runtime | MTD-RUN-003 | U-PA | NOT EXECUTED |  |
| EX-RUN-006 | Service rejects invocation | MTD-RUN-003 | Unauthorized direct request | NOT EXECUTED |  |
| EX-RUN-007 | Own history visible | MTD-RUN-004 | U-SU-A1 | NOT EXECUTED |  |
| EX-RUN-008 | Own history visible | MTD-RUN-004 | U-SD-A | NOT EXECUTED |  |
| EX-RUN-009 | Other history protected | MTD-RUN-004 | U-SU-A2 | NOT EXECUTED |  |
| EX-RUN-010 | Object authorization | MTD-RUN-004 | Direct history URL/ID | NOT EXECUTED |  |
| EX-RUN-011 | Establish context | MTD-RUN-005 | U-SU-A1 | NOT EXECUTED |  |
| EX-RUN-012 | Context retained | MTD-RUN-005 | U-SU-A1 | NOT EXECUTED |  |
| EX-RUN-013 | Higher governance effective | MTD-RUN-005 | U-SU-A1 | NOT EXECUTED |  |
| EX-RUN-014 | Creator obeys same governance | MTD-RUN-005 | U-SD-A | NOT EXECUTED |  |
| EX-SRC-001 | Upload/select/use; original read-only | MTD-SRC-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-SRC-002 | Creator runtime source works | MTD-SRC-001 | U-SD-A | NOT EXECUTED |  |
| EX-SRC-003 | Owner sees/uses | MTD-SRC-002 | U-SU-A1 | NOT EXECUTED |  |
| EX-SRC-004 | Cannot see/use | MTD-SRC-002 | U-SU-A2 | NOT EXECUTED |  |
| EX-SRC-005 | Object access rejected | MTD-SRC-002 | Direct source ID as A2 | NOT EXECUTED |  |
| EX-SRC-006 | Context reflects selected set | MTD-SRC-003 | U-SU-A1 | NOT EXECUTED |  |
| EX-SRC-007 | B no longer selected context | MTD-SRC-003 | U-SU-A1 | NOT EXECUTED |  |
| EX-SRC-008 | Context updates | MTD-SRC-003 | U-SU-A1 | NOT EXECUTED |  |
| EX-GEN-001 | Artifact created | MTD-GEN-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-GEN-002 | Artifact created | MTD-GEN-001 | U-SD-A | NOT EXECUTED |  |
| EX-GEN-003 | Retrieves/opens | MTD-GEN-002 | U-SU-A1 | NOT EXECUTED |  |
| EX-GEN-004 | No unauthorized access | MTD-GEN-002 | U-SU-A2 | NOT EXECUTED |  |
| EX-GEN-005 | Object protection | MTD-GEN-002 | Direct artifact ID | NOT EXECUTED |  |
| EX-ISO-001 | Same-Space view/run | MTD-ISO-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-ISO-002 | Cross-Space discovery blocked | MTD-ISO-001 | U-SU-B | NOT EXECUTED |  |
| EX-ISO-003 | Direct access rejected | MTD-ISO-001 | U-SU-B direct URL | NOT EXECUTED |  |
| EX-ISO-004 | Execution rejected | MTD-ISO-001 | U-SU-B direct runtime | NOT EXECUTED |  |
| EX-ISO-005 | Authorized use | MTD-ISO-002 | U-SU-A1 | NOT EXECUTED |  |
| EX-ISO-006 | Cross-Tenant discovery blocked | MTD-ISO-002 | U-SU-TB | NOT EXECUTED |  |
| EX-ISO-007 | Invocation blocked | MTD-ISO-002 | U-SU-TB direct request | NOT EXECUTED |  |
| EX-PUB-001 | Draft remains outside Marketplace | MTD-PUB-001 | U-SD-A | NOT EXECUTED |  |
| EX-PUB-002 | Draft not discoverable/runnable by Space User | MTD-PUB-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-PUB-003 | Frozen v1 created | MTD-PUB-002 | U-SD-A | NOT EXECUTED |  |
| EX-PUB-004 | Publication metadata persists | MTD-PUB-002 | U-SD-A | NOT EXECUTED |  |
| EX-PUB-005 | Tenant Owner cannot publish from role alone | MTD-PUB-002 | U-TO-A | NOT EXECUTED |  |
| EX-PUB-006 | Space Owner cannot publish from role alone | MTD-PUB-002 | U-SO-A | NOT EXECUTED |  |
| EX-PUB-007 | Agent published to Space A Marketplace | MTD-PUB-003 | U-SD-A | NOT EXECUTED |  |
| EX-PUB-008 | Same-Space consumer discovers/runs | MTD-PUB-003 | U-SU-A1 | NOT EXECUTED |  |
| EX-PUB-009 | Cross-Space consumer cannot discover/run | MTD-PUB-003 | U-SU-B | NOT EXECUTED |  |
| EX-VER-001 | Frozen V1 created | MTD-VER-001 | U-SD-A | NOT EXECUTED |  |
| EX-VER-002 | V1 unchanged | MTD-VER-001 | U-SD-A | NOT EXECUTED |  |
| EX-VER-003 | Still receives V1 | MTD-VER-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-VER-004 | Frozen V2 created | MTD-VER-001 | U-SD-A | NOT EXECUTED |  |
| EX-VER-005 | Receives V2 | MTD-VER-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-MKT-001 | Opens permitted Space Marketplace set | MTD-MKT-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-MKT-002 | Discoverable after Space Designer publishes | MTD-MKT-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-MKT-003 | Correct published version opens | MTD-MKT-001 | U-SU-A1 | NOT EXECUTED |  |
| EX-MKT-004 | Unauthorized cross-Space listing absent | MTD-MKT-001 | U-SU-B | NOT EXECUTED |  |
| EX-E2E-001 | Governed Build-to-Run | MTD-E2E-001 | Governed role chain | NOT EXECUTED |  |
| EX-E2E-002 | Runtime Source-to-Artifact | MTD-E2E-002 | Space User + isolation user | NOT EXECUTED |  |

## Notes

- Update the **Status** column as testing progresses.
- Use **Notes** for defect IDs, blockers, observations, or other context needed for reporting.
- This tracker is intended as the working input for generating the daily testing summary.
