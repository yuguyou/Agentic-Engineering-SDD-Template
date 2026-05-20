# checklist.md — Pre-release Quality Gate

> **Stage**: Tasks (Stage 4)
> **Nature**: Focuses on cross-task, system-level acceptance, complementing the single-feature acceptance in spec.md / tasks.md
> **Update Timing**: Verify item by item before each release; failure of any single item prevents release

---

## Feature Completeness

- [ ] All tasks in `tasks.md` are completed and checked off
- [ ] All acceptance criteria (AC) for P0 features in `spec.md` have been verified and passed
- [ ] All acceptance criteria for P1 features in `spec.md` have been verified and passed (if included in this iteration)
- [ ] No features exist "in code but not in spec" (scope creep check)
- [ ] Features listed in Out of Scope in `spec.md` are confirmed not implemented

## Test Passing

- [ ] All unit tests pass: `[test command, e.g. pytest tests/unit/ -v]`
- [ ] All integration tests pass: `[test command, e.g. pytest tests/integration/ -v]`
- [ ] Code coverage meets standard (≥ [Threshold]%): `[coverage command]`
- [ ] E2E tests pass (if applicable): `[E2E command]`

## Security Review

> For specific security standards, refer to the security requirements section in `constitution.md`.

- [ ] All user inputs are validated and sanitized (prevent SQL injection / XSS)
- [ ] Authentication and authorization mechanisms are implemented and tested
- [ ] Sensitive data (passwords, Tokens, API Keys) do not appear in code or logs
- [ ] HTTPS is correctly configured (production environment)
- [ ] Dependency security scan passed: `[scan command, e.g. pip audit / npm audit]`

## Performance Benchmarks

> For specific thresholds, refer to the performance baselines section in `constitution.md`.

- [ ] API response time P95 ≤ [Threshold, e.g. 500ms]
- [ ] Page first contentful paint time ≤ [Threshold, e.g. 3s] (if applicable)
- [ ] No N+1 query issues
- [ ] Database queries are all covered by indexes (no full table scans)
- [ ] Load testing passed (if applicable): no errors under [Concurrency count]

## Code Quality

- [ ] Code Review completed
- [ ] Lint check shows zero errors: `[lint command, e.g. ruff check .]`
- [ ] Type check passed (if applicable): `[type check command, e.g. mypy src/]`
- [ ] No TODO/FIXME/HACK left in the code (or corresponding issues have been created)

## Documentation Sync

- [ ] `data-model.md` matches the actual Schema
- [ ] `contracts/` matches the actual APIs
- [ ] `decisions.md` has recorded the important technical decisions of this iteration
- [ ] The environment setup steps in `README.md` are still executable normally
- [ ] `changelog.md` has been updated with the contents of this release

## Deployment Verification

- [ ] Deployment scripts/workflows have been tested
- [ ] Environment variable configurations are complete (compare with `.env.example`)
- [ ] Database migration scripts execute normally (including rollback tests)
- [ ] Health check endpoint returns normally
- [ ] Log output format and levels are correct

---

## Release Decision

| Check Category | Passed Count | Total Count | Pass Rate |
| :--- | :--- | :--- | :--- |
| Feature Completeness | /5 | 5 | % |
| Test Passing | /4 | 4 | % |
| Security Review | /5 | 5 | % |
| Performance Benchmarks | /5 | 5 | % |
| Code Quality | /4 | 4 | % |
| Documentation Sync | /5 | 5 | % |
| Deployment Verification | /5 | 5 | % |

**Release Conclusion**: 🟢 Ready for Release | 🟡 Conditional Release (specify conditions) | 🔴 Not Ready for Release

**Approver**: [Approver Signature] | **Date**: YYYY-MM-DD
