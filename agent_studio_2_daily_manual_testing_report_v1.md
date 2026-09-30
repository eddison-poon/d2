# Agent Studio 2.0 — Daily Manual Testing Report

**Version:** v1  
**Date:** 2026-09-30  
**Status:** Draft for review

## Purpose

Provide a feature-oriented daily view of manual testing, aligned with the development team's category and feature list.

- Development completion is taken from the development feature list.
- Testing Completion is reserved for the percentage completion of the manual test cases mapped to the same feature row.
- Manual test counts are mapped from existing MTDs / execution variants by feature intent.
- No MTD or execution mapping is required for every feature; unmatched features remain at 0.
- Categories/features with no development progress are treated as 0% for this first version.
- This report covers manual testing only.

## Feature / Role Breakdown

| Category | Feature | Development Completion | Testing Completion | Tenant Owner | Space Owner | Agent Creator | Space User | Other | Total Cases |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Tenant Management 2.0 | Project Creation | 100% | — | 1 | 0 | 0 | 0 | 0 | 1 |
| Tenant Management 2.0 | Space | 100% | — | 1 | 2 | 0 | 0 | 0 | 3 |
| Tenant Management 2.0 | Agent | 100% | — | 0 | 1 | 6 | 1 | 0 | 8 |
| Tenant Management 2.0 | Project Creation Pipeline + NS Creation | 0% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Tenant Management 2.0 | Knowledge Base | 100% | — | 0 | 0 | 2 | 1 | 0 | 3 |
| Tenant Management 2.0 | User Role | 80% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Tenant Management 2.0 | Skill Management | 80% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Tenant Management 2.0 | Member Management | 80% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Tenant Management 2.0 | Credential Management | 80% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case1: Simple Agent Execution | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case2: Agent + MCP tool | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case3: Agent + Knowledge base | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case4: Agent + File input & output | 90% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case5: Natural Language to Agent | 90% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case6: Agent HITL | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case7: Agent + Memory (both short term + long term) | 20% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Case8: Agent + Skill | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | LLM Gateway 1.0 | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Gateway 2.0 | 50% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Streaming | 100% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Execution | Agent Harness Framework | 90% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Workspace | Sources Management | 0% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Workspace | Session input | 0% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agentic Workflow | — | 0% | — | 0 | 0 | 0 | 0 | 0 | 0 |
| Agent Monitoring & Evaluation | — | 0% | — | 0 | 0 | 0 | 0 | 0 | 0 |

> **Review note:** The first five role/case counts are the initial mapping from the v1 reporting concept. The remaining rows are now included to establish the complete development feature structure, with case counts left at 0 until a corresponding MTD/execution mapping is confirmed. Testing Completion is intentionally reserved and is not yet calculated.

## Terminology

- **Mng** = Management
- **NL2 Agent** = Natural Language to Agent
- **HITL** = User feedback interface

## Mapping Rules

1. The development team's category/feature list is the master reporting structure.
2. Existing manual MTDs and execution variants are mapped to a feature only when their test intent genuinely covers that feature.
3. Keyword similarity alone is not sufficient to map an MTD/execution to a feature.
4. A feature may legitimately have zero corresponding MTDs or executions.
5. Features/categories with no development progress are shown as 0% initially.
6. Testing Completion will represent the percentage completion of the manual test cases mapped to that feature row.
7. This version intentionally excludes automation and performance testing.

## Next Review

Review the complete feature table together and refine:
- feature-to-MTD/execution mapping;
- role columns and role naming;
- Testing Completion calculation;
- how daily progress/change should be shown;
- which indicators make problems visible at first glance.
