# manifest.md — Document Map & Metadata

> **Category**: Supplementary Document
> **Nature**: Parseable document map supporting automated dependency analysis
> **Update Timing**: Sync updates whenever a core document is added or modified

---

## Document Status Overview

> Status Enum: 📝 Draft | 👀 Reviewed | ✅ Implemented | ⚠️ Needs Update | ❌ Deprecated

| Stage | Document | Path | Version | Status | Created | Last Updated |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Rules** | AGENTS.md | `./AGENTS.md` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |
| | constitution.md | `./constitution.md` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |
| | README.md | `./README.md` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |
| **Specify** | spec.md | `./docs/spec.md` | 1.0 | 👀 Reviewed | YYYY-MM-DD | YYYY-MM-DD |
| | ui-spec.md | `./docs/ui-spec.md` | — | 📝 Draft | — | — |
| **Plan** | architecture.md | `./docs/architecture.md` | 1.0 | 👀 Reviewed | YYYY-MM-DD | YYYY-MM-DD |
| | data-model.md | `./docs/data-model.md` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |
| | contracts/ | `./contracts/` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |
| | plan.md | `./docs/plan.md` | 1.0 | 👀 Reviewed | YYYY-MM-DD | YYYY-MM-DD |
| | decisions.md | `./docs/decisions.md` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |
| | roadmap.md | `./docs/roadmap.md` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |
| **Tasks** | seed-data/ | `./seed-data/` | — | 📝 Draft (if needed) | — | — |
| | tasks.md | `./docs/tasks.md` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |
| | checklist.md | `./docs/checklist.md` | 1.0 | 📝 Draft | YYYY-MM-DD | YYYY-MM-DD |
| **Execute** | progress.md | `./docs/progress.md` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |
| | changelog.md | `./CHANGELOG.md` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |
| | proposal.md | `./docs/proposal.md` | — | — | — | — |
| **Supplement** | manifest.md | `./docs/manifest.md` | 1.0 | ✅ Implemented | YYYY-MM-DD | YYYY-MM-DD |

---

## Document Relationships

> Format: Document A → Relationship → Document B

```
# Rules Stage Constraints (spans entire process)
constitution.md  → constrains → AGENTS.md
constitution.md  → constrains → architecture.md
constitution.md  → constrains → plan.md (tech stack baseline)

# Specify → Plan
spec.md          → drives     → architecture.md
spec.md          → drives     → roadmap.md
ui-spec.md       → drives     → tasks.md (UI related tasks)

# Plan Internal Dependencies
architecture.md  → outputs    → data-model.md
architecture.md  → outputs    → contracts/
architecture.md  → outputs    → plan.md
data-model.md    → inputs     → plan.md (Schema constrains implementation)
contracts/       → inputs     → plan.md (Interfaces constrain implementation)
decisions.md     → records    → architecture.md (Decision basis)

# Plan → Tasks
plan.md          → breaks into→ tasks.md
roadmap.md       → schedules  → tasks.md
seed-data/       → provides   → tasks.md (Test data support)

# Tasks → Execute
tasks.md         → acceptance → checklist.md
tasks.md         → tracks     → progress.md

# Execute Internal
progress.md      → aggregates → changelog.md
checklist.md     → gating     → changelog.md

# Change Feedback Loop
proposal.md      → triggers   → spec.md (Change closed-loop)
```

---

## Change History

| Date | Changed Document | Change Type | Description |
| :--- | :--- | :--- | :--- |
| YYYY-MM-DD | manifest.md | Creation | Initialize document map |
| YYYY-MM-DD | spec.md | Update | Added F-006 feature entry |
