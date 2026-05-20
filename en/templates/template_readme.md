# [Project Name]

> [One-sentence description of the core problem the project solves]

---

## Project Background

[2-3 sentences describing the business background and target users of the project]

## Core Features

- **[Feature 1]**: [Brief description]
- **[Feature 2]**: [Brief description]
- **[Feature 3]**: [Brief description]

## Tech Stack

| Category | Technology | Version |
| :--- | :--- | :--- |
| Programming Language | [e.g. Python] | [e.g. 3.12] |
| Web Framework | [e.g. FastAPI] | [e.g. 0.115] |
| Database | [e.g. PostgreSQL] | [e.g. 16] |
| ORM | [e.g. SQLAlchemy] | [e.g. 2.0] |
| Test Framework | [e.g. pytest] | [e.g. 8.x] |
| Package Manager | [e.g. uv] | [e.g. latest] |

## Environment Setup

### Prerequisites

- [e.g. Python 3.12+]
- [e.g. PostgreSQL 16+]
- [e.g. Docker (optional)]

### Quick Start

```bash
# 1. Clone repository
git clone [repo_url]
cd [project_dir]

# 2. Install dependencies
[e.g. uv sync / npm install / pip install -r requirements.txt]

# 3. Configure environment variables
cp .env.example .env
# Edit the .env file and fill in required configurations

# 4. Initialize database
[e.g. alembic upgrade head / prisma migrate dev]

# 5. Start development server
[e.g. uvicorn src.main:app --reload / npm run dev]
```

### Verify Installation

```bash
# Run tests
[e.g. pytest tests/ -v]

# Check service status
[e.g. curl http://localhost:8000/health]
```

## Core Document Index

> This project follows the **Agentic Engineering + SDD** development system (Five stages: Rules → Specify → Plan → Tasks → Execute).

| Stage | Document | Description | Path |
| :--- | :--- | :--- | :--- |
| **Rules** | AGENTS.md | AI coding behavior contract | `AGENTS.md` |
| | constitution.md | Highest technical constraints and quality baselines | `constitution.md` |
| **Specify** | spec.md | Single Source of Truth (Requirements) | `docs/spec.md` |
| | ui-spec.md | UI implementation contract (if needed) | `docs/ui-spec.md` |
| **Plan** | architecture.md | System architecture blueprint | `docs/architecture.md` |
| | data-model.md | Data persistence model | `docs/data-model.md` |
| | contracts/ | API hard contracts | `contracts/` |
| | plan.md | Technical implementation path | `docs/plan.md` |
| | decisions.md | Architecture decision records | `docs/decisions.md` |
| | roadmap.md | Delivery roadmap | `docs/roadmap.md` |
| **Tasks** | tasks.md | Atomic action checklist | `docs/tasks.md` |
| | checklist.md | Pre-release quality gate | `docs/checklist.md` |
| **Execute** | progress.md | In-flight status dashboard | `docs/progress.md` |
| | changelog.md | Delivered results archive | `CHANGELOG.md` |

## Directory Structure

```
[Project Name]/
├── src/                    # Source code
├── tests/                  # Test code
├── docs/                   # SDD document system
│   ├── spec.md
│   ├── ui-spec.md          # If needed
│   ├── architecture.md
│   ├── data-model.md
│   ├── plan.md
│   ├── decisions.md
│   ├── roadmap.md
│   ├── tasks.md
│   ├── checklist.md
│   ├── progress.md
│   ├── proposal.md         # Post-MVP
│   └── manifest.md
├── contracts/              # API contracts
├── seed-data/              # Test baseline data (if needed)
├── .env.example            # Environment variables template
├── AGENTS.md               # AI behavior contract
├── constitution.md         # Technical constraints
├── CHANGELOG.md            # Delivery records
└── README.md               # This file
```

## License

[e.g. MIT / Apache 2.0 / Proprietary]
