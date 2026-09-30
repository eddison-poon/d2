# Agent Studio 2.0 — Daily Manual Testing Report

**Version:** v1  
**Date:** 2026-09-30  
**Status:** Draft for review

## Purpose

Provide a feature-oriented daily view of manual testing aligned with the development team's category and feature list. Development Completion follows the development feature list; Testing Completion is reserved for execution progress of the cases mapped to each feature. This version covers manual testing only.

## Feature / Role Breakdown

| Category | Feature | Development Completion | Testing Completion | Tenant Owner | Space Owner | Agent Creator | Space User | Other | Total Cases |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Tenant Management 2.0 | Project Creation | 100% | — | 5 | 2 | 2 | 1 | 0 | 10 |
| Tenant Management 2.0 | Space | 100% | — | 2 | 2 | 1 | 0 | 0 | 5 |
| Tenant Management 2.0 | Agent | 100% | — | 5 | 5 | 16 | 20 | 3 | 49 |
| Tenant Management 2.0 | Project Creation Pipeline + NS Creation | 0% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Tenant Management 2.0 | Knowledge Base | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Tenant Management 2.0 | User Role | 80% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Tenant Management 2.0 | Skill Management | 80% | — | 0 | 1 | 1 | 0 | 0 | 2 |
| Tenant Management 2.0 | Member Management | 80% | — | 1 | 3 | 1 | 1 | 2 | 8 |
| Tenant Management 2.0 | Credential Management | 80% | — | 0 | 0 | 4 | 0 | 0 | 4 |
| Agent Execution | Case1: Simple Agent Execution | 100% | — | 1 | 1 | 2 | 3 | 3 | 10 |
| Agent Execution | Case2: Agent + MCP tool | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case3: Agent + Knowledge base | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case4: Agent + File input & output | 90% | — | 0 | 0 | 1 | 3 | 1 | 5 |
| Agent Execution | Case5: Natural Language to Agent | 90% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case6: Agent HITL | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case7: Agent + Memory (both short term + long term) | 20% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case8: Agent + Skill | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | LLM Gateway 1.0 | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Gateway 2.0 | 50% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Streaming | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Agent Harness Framework | 90% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Workspace | Sources Management | 0% | — | 0 | 0 | 1 | 6 | 1 | 8 |
| Workspace | Session input | 0% | — | 0 | 0 | 1 | 3 | 0 | 4 |
| Agentic Workflow | — | 0% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Monitoring & Evaluation | — | 0% | — | 0 | 0 | 0 | 0 | 0 | 0 |

## Feature-to-Test-Case Mapping

| Category | Feature | Test Case ID | Test Case Title | Role |
|---|---|---|---|---|
| Tenant Management 2.0 | Project Creation | EX-GOV-001 | Can enable/disable Pattern | U-TO-A |
| Tenant Management 2.0 | Project Creation | EX-GOV-002 | Cannot change Pattern enablement | U-SO-A |
| Tenant Management 2.0 | Project Creation | EX-GOV-003 | Cannot change Pattern enablement | U-SD-A |
| Tenant Management 2.0 | Project Creation | EX-GOV-004 | Cannot change Pattern enablement | U-SU-A1 |
| Tenant Management 2.0 | Project Creation | EX-GOV-005 | Defines permitted capability/types | U-TO-A |
| Tenant Management 2.0 | Project Creation | EX-GOV-006 | Cannot define tenant capabilities | U-SO-A |
| Tenant Management 2.0 | Project Creation | EX-GOV-007 | Cannot expand allowance | U-SD-A |
| Tenant Management 2.0 | Project Creation | EX-GOV-015 | All 10 required tenants exist | Tenant Owner/admin view |
| Tenant Management 2.0 | Project Creation | EX-GOV-016 | Required default Space exists for each tenant | Tenant Owner/admin view |
| Tenant Management 2.0 | Project Creation | EX-GOV-017 | Required default Space protected | Tenant Owner |
| Tenant Management 2.0 | Space | EX-GOV-008 | Creates Space B if in scope | U-TO-A |
| Tenant Management 2.0 | Space | EX-GOV-009 | Cannot create Space | U-SO-A |
| Tenant Management 2.0 | Space | EX-GOV-010 | Assign/change Space Owner | U-TO-A |
| Tenant Management 2.0 | Space | EX-GOV-022 | Space prompt saves and persists | U-SO-A |
| Tenant Management 2.0 | Space | EX-GOV-023 | Precedence Pattern > Tenant > Space > Agent enforced | U-SD-A |
| Tenant Management 2.0 | Agent | EX-BLD-001 | Creates Agent from enabled Low Risk | U-SD-A |
| Tenant Management 2.0 | Agent | EX-BLD-002 | Cannot create Agent | U-TO-A |
| Tenant Management 2.0 | Agent | EX-BLD-003 | Cannot create Agent | U-SO-A |
| Tenant Management 2.0 | Agent | EX-BLD-004 | Cannot create Agent | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-BLD-013 | Assisted creation starts from supplied idea | U-SD-A |
| Tenant Management 2.0 | Agent | EX-BLD-014 | Focused required setup information collected | U-SD-A |
| Tenant Management 2.0 | Agent | EX-BLD-015 | One valid draft Agent created | U-SD-A |
| Tenant Management 2.0 | Agent | EX-BLD-016 | Required-field validation prevents invalid draft | U-SD-A |
| Tenant Management 2.0 | Agent | EX-BLD-017 | No unintended Agent/draft created | U-SD-A |
| Tenant Management 2.0 | Agent | EX-BLD-005 | Configure Agent | U-SD-A |
| Tenant Management 2.0 | Agent | EX-BLD-006 | Cannot configure | U-TO-A |
| Tenant Management 2.0 | Agent | EX-BLD-007 | Cannot configure | U-SO-A |
| Tenant Management 2.0 | Agent | EX-BLD-008 | Cannot configure | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-ACC-001 | Can view, not edit/run | U-TO-A |
| Tenant Management 2.0 | Agent | EX-ACC-002 | Can view | U-SO-A |
| Tenant Management 2.0 | Agent | EX-ACC-003 | Can view | U-SD-A |
| Tenant Management 2.0 | Agent | EX-ACC-004 | Can view | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-ACC-005 | No 6.6 from platform role | U-PA |
| Tenant Management 2.0 | Agent | EX-ACC-006 | Catalogue access ≠ Agent visibility | U-VR |
| Tenant Management 2.0 | Agent | EX-ACC-007 | Can edit | U-SD-A |
| Tenant Management 2.0 | Agent | EX-ACC-008 | Cannot edit | U-TO-A |
| Tenant Management 2.0 | Agent | EX-ACC-009 | Cannot edit | U-SO-A |
| Tenant Management 2.0 | Agent | EX-ACC-010 | Cannot edit | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-ACC-011 | Backend rejects edit | Unauthorized direct request |
| Tenant Management 2.0 | Agent | EX-ISO-001 | Same-Space view/run | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-ISO-002 | Cross-Space discovery blocked | U-SU-B |
| Tenant Management 2.0 | Agent | EX-ISO-003 | Direct access rejected | U-SU-B direct URL |
| Tenant Management 2.0 | Agent | EX-ISO-004 | Execution rejected | U-SU-B direct runtime |
| Tenant Management 2.0 | Agent | EX-ISO-005 | Authorized use | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-ISO-006 | Cross-Tenant discovery blocked | U-SU-TB |
| Tenant Management 2.0 | Agent | EX-ISO-007 | Invocation blocked | U-SU-TB direct request |
| Tenant Management 2.0 | Agent | EX-PUB-001 | Draft remains outside Marketplace | U-SD-A |
| Tenant Management 2.0 | Agent | EX-PUB-002 | Draft not discoverable/runnable by Space User | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-PUB-003 | Frozen v1 created | U-SD-A |
| Tenant Management 2.0 | Agent | EX-PUB-004 | Publication metadata persists | U-SD-A |
| Tenant Management 2.0 | Agent | EX-PUB-005 | Tenant Owner cannot publish from role alone | U-TO-A |
| Tenant Management 2.0 | Agent | EX-PUB-006 | Space Owner cannot publish from role alone | U-SO-A |
| Tenant Management 2.0 | Agent | EX-PUB-007 | Agent published to Space A Marketplace | U-SD-A |
| Tenant Management 2.0 | Agent | EX-PUB-008 | Same-Space consumer discovers/runs | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-PUB-009 | Cross-Space consumer cannot discover/run | U-SU-B |
| Tenant Management 2.0 | Agent | EX-VER-001 | Frozen V1 created | U-SD-A |
| Tenant Management 2.0 | Agent | EX-VER-002 | V1 unchanged | U-SD-A |
| Tenant Management 2.0 | Agent | EX-VER-003 | Still receives V1 | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-VER-004 | Frozen V2 created | U-SD-A |
| Tenant Management 2.0 | Agent | EX-VER-005 | Receives V2 | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-MKT-001 | Opens permitted Space Marketplace set | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-MKT-002 | Discoverable after Space Designer publishes | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-MKT-003 | Correct published version opens | U-SU-A1 |
| Tenant Management 2.0 | Agent | EX-MKT-004 | Unauthorized cross-Space listing absent | U-SU-B |
| Tenant Management 2.0 | Skill Management | EX-BLD-009 | Attach approved MCP/skill | U-SD-A |
| Tenant Management 2.0 | Skill Management | EX-BLD-010 | Cannot attach MCP/skill | U-SO-A |
| Tenant Management 2.0 | Member Management | EX-GOV-011 | Add members/assign roles | U-SO-A |
| Tenant Management 2.0 | Member Management | EX-GOV-012 | Does not receive 6.3 | U-TO-A |
| Tenant Management 2.0 | Member Management | EX-GOV-013 | Cannot assign roles | U-SD-A |
| Tenant Management 2.0 | Member Management | EX-GOV-014 | Cannot assign roles | U-SU-A1 |
| Tenant Management 2.0 | Member Management | EX-GOV-018 | Tenant Member can view tenant configuration | U-TM-A |
| Tenant Management 2.0 | Member Management | EX-GOV-019 | Tenant Member cannot administer tenant | U-TM-A |
| Tenant Management 2.0 | Member Management | EX-GOV-020 | Existing Tenant Member can be assigned a Space role | U-SO-A |
| Tenant Management 2.0 | Member Management | EX-GOV-021 | Space membership cannot bypass tenant membership | U-SO-A |
| Tenant Management 2.0 | Credential Management | EX-BLD-018 | Tool selection and personal access setup persist | U-SD-A |
| Tenant Management 2.0 | Credential Management | EX-BLD-019 | Deferred credential setup does not grant usable access | U-SD-A |
| Tenant Management 2.0 | Credential Management | EX-BLD-011 | Cannot attach/use | U-SD-A |
| Tenant Management 2.0 | Credential Management | EX-BLD-012 | Bypass rejected | U-SD-A direct attempt |
| Agent Execution | Case1: Simple Agent Execution | EX-RUN-001 | Executes successfully | U-SD-A |
| Agent Execution | Case1: Simple Agent Execution | EX-RUN-002 | Executes successfully | U-SU-A1 |
| Agent Execution | Case1: Simple Agent Execution | EX-RUN-003 | View but cannot execute | U-TO-A |
| Agent Execution | Case1: Simple Agent Execution | EX-RUN-004 | View but cannot execute | U-SO-A |
| Agent Execution | Case1: Simple Agent Execution | EX-RUN-005 | Platform admin ≠ runtime | U-PA |
| Agent Execution | Case1: Simple Agent Execution | EX-RUN-006 | Service rejects invocation | Unauthorized direct request |
| Agent Execution | Case1: Simple Agent Execution | EX-RUN-007 | Own history visible | U-SU-A1 |
| Agent Execution | Case1: Simple Agent Execution | EX-RUN-008 | Own history visible | U-SD-A |
| Agent Execution | Case1: Simple Agent Execution | EX-RUN-009 | Other history protected | U-SU-A2 |
| Agent Execution | Case1: Simple Agent Execution | EX-RUN-010 | Object authorization | Direct history URL/ID |
| Agent Execution | Case4: Agent + File input & output | EX-GEN-001 | Artifact created | U-SU-A1 |
| Agent Execution | Case4: Agent + File input & output | EX-GEN-002 | Artifact created | U-SD-A |
| Agent Execution | Case4: Agent + File input & output | EX-GEN-003 | Retrieves/opens | U-SU-A1 |
| Agent Execution | Case4: Agent + File input & output | EX-GEN-004 | No unauthorized access | U-SU-A2 |
| Agent Execution | Case4: Agent + File input & output | EX-GEN-005 | Object protection | Direct artifact ID |
| Workspace | Sources Management | EX-SRC-001 | Upload/select/use; original read-only | U-SU-A1 |
| Workspace | Sources Management | EX-SRC-002 | Creator runtime source works | U-SD-A |
| Workspace | Sources Management | EX-SRC-003 | Owner sees/uses | U-SU-A1 |
| Workspace | Sources Management | EX-SRC-004 | Cannot see/use | U-SU-A2 |
| Workspace | Sources Management | EX-SRC-005 | Object access rejected | Direct source ID as A2 |
| Workspace | Sources Management | EX-SRC-006 | Context reflects selected set | U-SU-A1 |
| Workspace | Sources Management | EX-SRC-007 | B no longer selected context | U-SU-A1 |
| Workspace | Sources Management | EX-SRC-008 | Context updates | U-SU-A1 |
| Workspace | Session input | EX-RUN-011 | Establish context | U-SU-A1 |
| Workspace | Session input | EX-RUN-012 | Context retained | U-SU-A1 |
| Workspace | Session input | EX-RUN-013 | Higher governance effective | U-SU-A1 |
| Workspace | Session input | EX-RUN-014 | Creator obeys same governance | U-SD-A |

## Executions Not Yet Identified to a Development Feature

These executions are intentionally left unmapped for review rather than forcing them into a feature by keyword similarity.

| Test Case ID | Test Case Title | Role | Parent MTD | Parent MTD Title |
|---|---|---|---|---|
| EX-PAT-001 | Low Risk Pattern exists/identifiable | Authorized pattern viewer/admin | MTD-PAT-001 | Verify required Patterns exist and are assignable |
| EX-PAT-002 | SDLC Pattern exists/identifiable | Authorized pattern viewer/admin | MTD-PAT-001 | Verify required Patterns exist and are assignable |
| EX-PAT-003 | Pattern rule persists/inherits | Authorized governance setup | MTD-PAT-002 | Verify shared Pattern rules govern downstream behaviour |
| EX-PAT-004 | Pattern rule remains effective | Space Designer runtime | MTD-PAT-002 | Verify shared Pattern rules govern downstream behaviour |
| EX-E2E-001 | Governed Build-to-Run | Governed role chain | MTD-E2E-001 | Governed agent build and consumption |
| EX-E2E-002 | Runtime Source-to-Artifact | Space User + isolation user | MTD-E2E-002 | Runtime with personal source and generated artifact |

**Mapped executions:** 105  
**Unidentified executions:** 6  
**Total executions reviewed:** 111

## Mapping Rules

1. The development team's category/feature list is the master reporting structure.
2. Existing execution variants are mapped only where their test intent genuinely covers the feature.
3. Keyword similarity alone is not sufficient.
4. Each execution is mapped once in this first reporting version to avoid double counting.
5. Features may legitimately have zero mapped executions.
6. Testing Completion will be calculated from execution status after the feature mapping is agreed.
7. Automation and performance testing are excluded from this version.
