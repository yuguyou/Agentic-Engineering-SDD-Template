# roadmap.md — Delivery Roadmap

> **Stage**: Plan (Stage 3)
> **Prerequisite**: Complete after spec.md is finalized and before tasks.md is broken down
> **Nature**: Plans product delivery cadence at the milestone level; atomic tasks are handled by tasks.md
> **Update Timing**: Update status upon milestone completion

---

## Roadmap Overview

```mermaid
gantt
    title Project Delivery Roadmap
    dateFormat  YYYY-MM-DD
    axisFormat  %m/%d

    section MVP
    Milestone 1: Infrastructure        :m1, YYYY-MM-DD, 5d
    Milestone 2: Core Features         :m2, after m1, 10d

    section v1.0
    Milestone 3: Full Features         :m3, after m2, 10d
    Milestone 4: Polish & Release      :m4, after m3, 5d
```

---

## Milestone Details

### 🏁 M1: Infrastructure Setup

- **Goal**: Project skeleton runnable, dev environment ready
- **Timeframe**: YYYY-MM-DD → YYYY-MM-DD
- **Status**: 🟡 Pending | 🔵 In Progress | 🟢 Done
- **Deliverables**:
  - [ ] Project scaffolding initialization
  - [ ] Database connection and migration config
  - [ ] CI/CD pipeline
  - [ ] Health check endpoint
- **Associated Spec Entries**: Infrastructure (No direct F ID)
- **Acceptance Criteria**: Service starts after `docker compose up`, health check returns 200

---

### 🏁 M2: Core Features (MVP)

- **Goal**: Core business flows can be run through
- **Timeframe**: YYYY-MM-DD → YYYY-MM-DD
- **Status**: 🟡 Pending
- **Deliverables**:
  - [ ] F-001: [Feature Name]
  - [ ] F-002: [Feature Name]
  - [ ] F-003: [Feature Name]
- **Associated Spec Entries**: F-001 ~ F-003 (P0 features)
- **Acceptance Criteria**: All acceptance criteria (AC) for P0 features pass

---

### 🏁 M3: Full Features

- **Goal**: Complete P1 features, cover the full user journey
- **Timeframe**: YYYY-MM-DD → YYYY-MM-DD
- **Status**: 🟡 Pending
- **Deliverables**:
  - [ ] F-004: [Feature Name]
  - [ ] F-005: [Feature Name]
- **Associated Spec Entries**: F-004 ~ F-005 (P1 features)

---

### 🏁 M4: Polish & Release

- **Goal**: Performance meets standards, security audit passed, ready for launch
- **Timeframe**: YYYY-MM-DD → YYYY-MM-DD
- **Status**: 🟡 Pending
- **Deliverables**:
  - [ ] Performance optimization (NF-001 met)
  - [ ] Security review (checklist.md all passed)
  - [ ] Deployment and launch

---

## Dependencies

| Milestone | Depends On | Notes |
| :--- | :--- | :--- |
| M2 | M1 | Core features depend on ready infrastructure |
| M3 | M2 | P1 features depend on completed P0 features |
| M4 | M3 | Polish and release depend on all features completed |

---

## Prioritization Principles

1. **P0 Features First**: First implement core features marked as P0 in the spec
2. **Dependency Driven**: Depended-upon modules are implemented first
3. **Risk Front-loading**: Features with high technical risk are verified early
4. **Value Delivery**: At the end of each milestone, the system should be in a demonstrable/acceptable state
