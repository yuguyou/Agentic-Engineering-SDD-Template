# proposal.md — Change Proposal

> **Stage**: Execute (Stage 5)
> **Applicable Conditions**: Create when new requirements emerge after MVP release
> **Review Status**: 📝 Draft | ✅ Approved | ❌ Rejected
> **Cascade Updates**: Triggered after approval → modify spec → re-plan → re-tasks

---

## PROP-001: [Change Title]

### Basic Information

| Field | Content |
| :--- | :--- |
| **Proposal ID** | PROP-001 |
| **Proposer** | [Name] |
| **Proposal Date** | YYYY-MM-DD |
| **Review Status** | 📝 Draft |
| **Reviewer** | [Name] |
| **Review Date** | — |

### Motivation for Change

[Why is this change needed? User feedback, business requirement, tech debt, or market shift?]

### Change Description

[Detailed description of features to be added/modified/deleted]

### Impact Scope Analysis

| Impact Dimension | Affected Files/Entries | Impact Level |
| :--- | :--- | :--- |
| spec.md | F-XXX (Modify) / F-YYY (Add) | Medium |
| architecture.md | [Module Name] | Low/None |
| data-model.md | [Table/Field name] | High (Schema change) |
| contracts/ | [Interface files] | Medium (Add/Modify endpoints) |
| plan.md | [Implementation path tweaks] | Low |
| tasks.md | Added [X] tasks | Medium |

### Implementation Plan

[Briefly describe technical implementation ideas; for complex plans, cite ADRs in decisions.md]

### Estimated Workload

| Task | Complexity | Estimated Time |
| :--- | :--- | :--- |
| [Sub-task 1] | S/M/L/XL | [X]h |
| [Sub-task 2] | S/M/L/XL | [X]h |
| **Total** | — | **[X]h** |

### Risk Assessment

| Risk | Likelihood | Impact | Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| [Risk Description] | High/Medium/Low | High/Medium/Low | [Mitigation Plan] |

### Review Conclusion

- **Conclusion**: ✅ Approved | ❌ Rejected | 🔄 Needs Revision & Re-review
- **Reason**: [Reason for approval/rejection]
- **Additional Conditions**: [If any, list prerequisites for approval]

---

## PROP-002: [Change Title]

[Copy the template above, increment ID]

---

<!--
Change Management Workflow:
1. Submit Proposal (this file)
2. Review → Approve/Reject
3. Upon approval, cascade updates via SDD standard workflow:
   proposal → modify spec.md → update plan.md (if needed) → re-breakdown tasks.md → execute
4. Directly modifying code while skipping any steps is prohibited
-->
