# AGENTS.md — AI Coding Behavior Contract

> **Stage**: Rules (Stage 1)
> **File Alias**: Claude Code → `CLAUDE.md` | Cursor → `.cursorrules` | Universal → `AGENTS.md`
> **Recommended Length**: ≤ 300 lines
> **Update Timing**: Create at project kickoff; append promptly when new coding conventions are discovered

---

## Coding Principles

- **Think before coding**: After receiving a task, output an implementation plan summary first, and wait for human confirmation before writing code
- **Keep it simple**: Prioritize the simplest implementation method, avoid over-engineering
- **Precise modification**: Only modify code required by the task, do not "by the way" refactor or optimize unrelated parts
- **Define verifiable goals**: After each implementation, provide specific verification steps or test commands

## Prohibited Behaviors

- Prohibited from introducing new third-party dependencies unless explicitly requested
- Prohibited from deleting or modifying existing test cases (unless explicitly required by the task)
- Prohibited from modifying Database Schema without simultaneously updating `data-model.md`
- Prohibited from hardcoding environment configurations in code (API Keys, database connection strings, etc.)
- Prohibited from implementing features listed in Out of Scope in `spec.md`

## Tech Stack Constraints

> The tech stack (languages, frameworks, databases, etc.) are immutable constraints, defined uniformly in `constitution.md`.
> AI must simultaneously read `constitution.md` to get tech stack information before executing a task.

## Code Style

- Use [Formatter for the specific language, e.g. ruff / prettier / gofmt]
- Naming convention: [e.g. snake_case for Python, camelCase for JS]
- Max line width: [e.g. 88 characters]
- Import sorting: [e.g. isort standard]
- Type annotations: [e.g. All public functions must have type annotations]

## Testing Standards

- Unit test command: `[e.g. pytest tests/unit/ -v]`
- Integration test command: `[e.g. pytest tests/integration/ -v]`
- Code coverage check: `[e.g. pytest --cov=src --cov-report=term-missing]`
- Test file naming: `test_<module_name>.py`
- Each public function must have at least one positive test and one exception test

## Git Standards

- Branch naming: `feature/<feature_name>` / `fix/<issue_description>` / `refactor/<module_name>`
- Commit format: `<type>(<scope>): <description>`
  - type: feat / fix / refactor / test / docs / chore
  - Example: `feat(auth): implement user registration API`
- Each task corresponds to one commit, commit message references the task ID

## Project Structure

```
[Project Name]/
├── src/                    # Source code
│   ├── [Module A]/         # [Module A responsibility description]
│   ├── [Module B]/         # [Module B responsibility description]
│   └── [Entry File]        # Application entry (e.g. main.py / index.ts / main.go)
├── tests/                  # Test code
│   ├── unit/               # Unit tests
│   └── integration/        # Integration tests
├── docs/                   # Project documentation (SDD document system)
├── seed-data/              # Test baseline data
├── contracts/              # API contract files
├── .env.example            # Environment variables template
├── AGENTS.md               # This file (AI behavior contract)
├── constitution.md         # Highest technical constraints
└── README.md               # Project entry document
```

## Output Format Requirements

- When code changes, explain which files were modified and the reasons for the modification
- After completing a task, output verification steps
- When encountering uncertain technical decisions, list alternative solutions and request human decision, do not decide on your own
