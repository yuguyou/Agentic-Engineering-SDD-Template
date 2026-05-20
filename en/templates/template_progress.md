# progress.md — In-Flight Status Dashboard

> **Stage**: Execute (Stage 5)
> **Prerequisite**: Initialize after tasks.md is created; the task list must perfectly match tasks.md
> **Update Timing**: Update immediately after each task is completed; record immediately when blockers occur
> **Status Enum**: 🟡 Pending | 🔵 In Progress | 🟢 Done | 🔴 Blocked

---

## Current Iteration: [Milestone Name, e.g. M2 - Core MVP]

> Task IDs and descriptions must remain consistent with `tasks.md`. When adding/removing tasks, update both places synchronously.

### Iteration Overview

| Metric | Value |
| :--- | :--- |
| Total Tasks | [X] |
| Done | [X] |
| In Progress | [X] |
| Blocked | [X] |
| Completion Rate | [X]% |
| Iteration Period | YYYY-MM-DD → YYYY-MM-DD |

### Task Status Details

| Task ID | Task Description | Status | Owner | Completion Date | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| T-001 | Initialize project scaffolding | 🟢 Done | [Name] | YYYY-MM-DD | — |
| T-002 | Configure DB connection and ORM | 🟢 Done | [Name] | YYYY-MM-DD | — |
| T-003 | Implement global middleware | 🔵 In Progress | [Name] | — | — |
| T-004 | Implement user registration API | 🟡 Pending | — | — | Depends on T-002 |
| T-005 | Implement user login API | 🔴 Blocked | [Name] | — | See blocker log |

---

## Blocker Log

> When a blocker occurs, reason and owner must be recorded; cannot be left blank

### BLOCK-001: [Blocker Title]

- **Associated Task**: T-005
- **Blocker Reason**: [Specific reason, e.g.: Third-party email service API Key not yet obtained]
- **Owner**: [Name]
- **Estimated Resolution Time**: YYYY-MM-DD
- **Current Status**: 🔴 Unresolved | 🟢 Resolved
- **Resolution Plan**: [Resolution description]

---

## Test Result Summary

| Test Type | Total | Passed | Failed | Skipped | Coverage |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Unit Tests | [X] | [X] | [X] | [X] | [X]% |
| Integration Tests | [X] | [X] | [X] | [X] | — |
| E2E Tests | [X] | [X] | [X] | [X] | — |

---

## Outstanding Issues

| ID | Issue Description | Priority | Status | Owner |
| :--- | :--- | :--- | :--- | :--- |
| ISSUE-001 | [Issue description] | P0/P1/P2 | Pending/Resolved | [Name] |

---

*Last Updated: YYYY-MM-DD HH:MM*
