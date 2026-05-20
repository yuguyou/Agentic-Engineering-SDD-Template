# spec.md — [Project Name] Requirements Specification

> **Stage**: Specify (Stage 2)
> **Nature**: Single Source of Truth. All implementations must be traceable to specific entries in this document.
> **Update Timing**: Must be completed before coding begins; when requirements change, update this document first, then drive plan/tasks updates

---

## Project Overview

- **Goal**: [One-sentence description of the core problem the project solves]
- **Core Users**: [Target user groups]
- **Success Metrics**:
  - [Quantifiable metric 1, e.g.: Registration conversion rate ≥ 30%]
  - [Quantifiable metric 2, e.g.: API average response time ≤ 200ms]
  - [Quantifiable metric 3, e.g.: System availability ≥ 99.9%]

---

## Feature List

> ID Rule: F-XXX (Feature), Priority: P0 (Must-have) / P1 (Important) / P2 (Nice-to-have)

| ID | Feature Name | Priority | Status | Associated Module | Notes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| F-001 | [Feature Name] | P0 | Draft | [e.g. Auth] | |
| F-002 | [Feature Name] | P0 | Draft | [e.g. User] | |
| F-003 | [Feature Name] | P1 | Draft | [e.g. Core] | |
| F-004 | [Feature Name] | P1 | Draft | | |
| F-005 | [Feature Name] | P2 | Draft | | |

---

## Feature Details

### F-001 [Feature Name]

**Description**: [Detailed description of the feature, including business context and user value]

**User Story**:
> As a [Role], I want to [Action], so that [Value].

**Business Rules**:
- BR-001-01: [Rule description, e.g.: Username length 3-20 chars, alphanumeric and underscore only]
- BR-001-02: [Rule description, e.g.: Same email cannot be registered multiple times]

**Acceptance Criteria**:

- **AC-001-01** (Happy Path):
  - Given: [Precondition, e.g.: User is on registration page, email not registered]
  - When: [Trigger action, e.g.: User fills valid email and compliant password, clicks register]
  - Then: [Expected result, e.g.: Account created, returns 201, verification email sent within 60s]

- **AC-001-02** (Exception Path - Duplicate Registration):
  - Given: [Precondition, e.g.: User is on registration page, email already registered]
  - When: [Trigger action, e.g.: User fills that email, clicks register]
  - Then: [Expected result, e.g.: Returns 409, shows "Email already registered" error]

- **AC-001-03** (Edge Case):
  - Given: [Precondition]
  - When: [Trigger action]
  - Then: [Expected result]

---

### F-002 [Feature Name]

**Description**: [Detailed description of the feature]

**User Story**:
> As a [Role], I want to [Action], so that [Value].

**Business Rules**:
- BR-002-01: [Rule description]

**Acceptance Criteria**:

- **AC-002-01** (Happy Path):
  - Given: [Precondition]
  - When: [Trigger action]
  - Then: [Expected result]

- **AC-002-02** (Exception Path):
  - Given: [Precondition]
  - When: [Trigger action]
  - Then: [Expected result]

- **AC-002-03** (Edge Case):
  - Given: [Precondition]
  - When: [Trigger action]
  - Then: [Expected result]

---

## Non-Functional Requirements

> Defines business-level non-functional metrics **specific to this project**. Universal tech baselines (e.g. test coverage, password algorithms) are constrained in `constitution.md` and are not repeated here.

| ID | Category | Requirement Description | Acceptance Criteria |
| :--- | :--- | :--- | :--- |
| NF-001 | Performance | [e.g. Search result return time] | P95 ≤ [Threshold]ms |
| NF-002 | Capacity | [e.g. Supported concurrent online users] | ≥ [Value] |
| NF-003 | Availability | [e.g. System uptime] | ≥ 99.9% |
| NF-004 | Compatibility | [e.g. Browser support] | Chrome/Firefox/Safari last 2 versions |

---

## Out of Scope

> **IMPORTANT**: The following features are explicitly out of scope for the current iteration. AI must not implement these features.

- ❌ [Explicit non-feature 1, e.g. Third-party login (Google/GitHub OAuth)]
- ❌ [Explicit non-feature 2, e.g. Internationalization/Multi-language]
- ❌ [Explicit non-feature 3, e.g. Mobile adaptation]
- ❌ [Explicit non-feature 4, e.g. Real-time push notifications]

---

## Glossary

| Term | Definition |
| :--- | :--- |
| [Term 1] | [Definition] |
| [Term 2] | [Definition] |

---

## Revision History

| Version | Date | Change Description | Author |
| :--- | :--- | :--- | :--- |
| 1.0 | YYYY-MM-DD | Initial version | [Name] |

---

*Status Enum: Draft → Reviewed → Implemented → Deprecated*
