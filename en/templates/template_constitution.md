# constitution.md — Project Highest Technical Constraints

> **Stage**: Rules (Stage 1)
> **Nature**: Once determined, cannot be modified without major changes. Prioritize consulting before all technical decisions.
> **Update Timing**: Modify only during architecture-level major changes; requires technical lead approval.

---

## Technical Constraints

### Programming Language

- Only use **[Language and Version]** for backend development
- Only use **[Language and Version]** for frontend development (if applicable)
- Prohibited from introducing other programming languages unless explicitly approved in this document

### Database

- Primary database: **[Database and Version]**
- Cache layer: **[Cache solution, e.g. Redis 7.x]** (if applicable)
- Prohibited from using in-memory databases as a persistence solution

### Deployment Environment

- Runtime environment: **[e.g. Docker / Kubernetes / Cloud Provider]**
- Operating system: **[e.g. Ubuntu 22.04 LTS]**
- Minimum compatible version: **[e.g. Node 18+ / Python 3.11+]**

---

## Quality Baselines

### Test Coverage

- Core business logic test coverage must be **≥ [Threshold, e.g. 80]%**
- All API endpoints must have corresponding integration tests
- Database migration scripts must have rollback tests

### Code Quality

- Any PR / MR must pass all automated tests before merging
- Lint check zero warnings (except those explicitly ignored in the config file)
- Security-related code (authentication, authorization, data encryption) must undergo human review

### Performance Baselines

- API response time P95 ≤ **[Threshold, e.g. 500ms]**
- Page first contentful paint time ≤ **[Threshold, e.g. 3s]** (if applicable)
- Database queries must not have full table scans (index coverage requirement)

---

## Security Requirements

- All user inputs must be validated and sanitized; directly concatenating SQL is prohibited
- Password storage must use **[Algorithm, e.g. bcrypt / argon2]**; plaintext or MD5 is prohibited
- API communication must use HTTPS; HTTP is prohibited
- Sensitive data (Tokens, secret keys) must not be committed to version control; use environment variables uniformly
- Dependencies must be scanned for security vulnerabilities regularly (**[Tool, e.g. Dependabot / Snyk]**)

---

## Architectural Constraints

- Circular dependencies between modules are prohibited
- The data access layer must be encapsulated through a unified abstraction layer; writing raw queries directly in business logic is prohibited
- All external service calls must have timeout configurations and retry mechanisms
- Log level standards: ERROR (requires immediate action) / WARN (needs attention) / INFO (business flow) / DEBUG (debugging info)

---

## Immutable Constraints

> The following constraints must absolutely not be violated during the project lifecycle:

1. **[Constraint 1, e.g.: Do not bypass authentication middleware to access protected resources]**
2. **[Constraint 2, e.g.: User data deletion must use soft deletion; physical deletion is prohibited]**
3. **[Constraint 3, e.g.: All financial calculations must use Decimal types; floating-point numbers are prohibited]**

---

*This document is the "constitution" of the project; any code violating the above constraints must not be merged into the main branch.*
