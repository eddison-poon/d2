# Agent Studio 2.0 — Daily Manual Testing Report

**Version:** v1  
**Date:** 2026-09-30  
**Status:** Draft for review

## Purpose

Provide a feature-oriented daily view of manual testing, aligned with the development team's category and feature list.

- Development completion is taken from the development feature list.
- Manual test counts are mapped from existing MTDs / execution variants by feature intent.
- No MTD or execution mapping is required for every feature; unmatched features remain at 0.
- Categories/features with no development progress are treated as 0% for this first version.
- This report covers manual testing only.

## Initial Feature / Role Breakdown

| Category | Feature | Development Completion | Tenant Owner | Space Owner | Agent Creator | Space User | Other | Total Cases |
|---|---|---:|---:|---:|---:|---:|---:|---:|
| Tenant Management 2.0 | Project Creation | 100% | 1 | 0 | 0 | 0 | 0 | 1 |
| Tenant Management 2.0 | Space | 100% | 1 | 2 | 0 | 0 | 0 | 3 |
| Tenant Management 2.0 | Agent | 100% | 0 | 1 | 6 | 1 | 0 | 8 |
| Tenant Management 2.0 | Project Creation Pipeline + NS Creation | 0% | 0 | 0 | 0 | 0 | 0 | 0 |
| Tenant Management 2.0 | Knowledge Base | 100% | 0 | 0 | 2 | 1 | 0 | 3 |

> **Review note:** Role/case counts above are the initial mapping for the v1 reporting concept. They should be reviewed against the complete MTD/execution dataset before being treated as the frozen daily-report baseline.

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
6. This version intentionally excludes automation and performance testing.

## Next Review

Review the first rows together and refine:
- feature-to-MTD/execution mapping;
- role columns and role naming;
- how execution completion should be represented per role;
- how daily progress/change should be shown;
- which indicators make problems visible at first glance.
