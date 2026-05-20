# decisions.md — Architecture Decision Records (ADR)

> **Stage**: Plan (Stage 3)
> **Nature**: Decision memory bank — append-only, do not delete (can be marked as "deprecated")
> **Update Timing**: Append immediately whenever an important technical decision is made, to avoid losing details due to retrospective writing

---

## ADR-001: [Decision Title, e.g.: Choose PostgreSQL as the Primary Database]

- **Date**: YYYY-MM-DD
- **Status**: Accepted | Deprecated | Under Discussion
- **Decision Maker**: [Name/Role]

### Background

[Why is this decision needed? What is the problem? What is the specific scenario triggering this decision?]

### Alternatives

| Option | Pros | Cons |
| :--- | :--- | :--- |
| Option A: [e.g. PostgreSQL] | [e.g. ACID transactions, JSON support, mature ecosystem] | [e.g. Slightly higher operational complexity] |
| Option B: [e.g. MongoDB] | [e.g. Flexible schema, easy horizontal scaling] | [e.g. Weak transaction support, hard to guarantee data consistency] |
| Option C: [e.g. SQLite] | [e.g. Zero config, embedded] | [e.g. Concurrent write limits, not suitable for production] |

### Decision

Choose **Option A: [Option Name]**.

Rationale: [Detailed rationale for the decision, combining specific project needs and constraints]

### Impact

- Impact on architecture: [e.g. Requires configuring connection pools, requires ORM support]
- Impact on development: [e.g. Team needs to understand SQL, needs to write migration scripts]
- Impact on operations: [e.g. Needs backup strategies, monitoring configuration]

### Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| [Risk Description] | Medium | High | [Mitigation Plan] |

---

## ADR-002: [Decision Title]

- **Date**: YYYY-MM-DD
- **Status**: Accepted
- **Decision Maker**: [Name/Role]

### Background

[Problem description]

### Alternatives

| Option | Pros | Cons |
| :--- | :--- | :--- |
| Option A | | |
| Option B | | |

### Decision

Choose **Option [X]**. Rationale: [Rationale]

### Impact

- Impact on architecture: [Impact description]
- Impact on development: [Impact description]
- Impact on operations: [Impact description]

### Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| [Risk Description] | High/Medium/Low | High/Medium/Low | [Mitigation Plan] |

---

<!-- 
Template tips:
- When adding a new decision, copy the ADR template above and increment the ID
- Do not delete deprecated decisions; change status to "Deprecated" and note the deprecation reason and replacement ADR ID
- AI should consult this file first when encountering technical selection issues, to avoid repeated discussions
-->
