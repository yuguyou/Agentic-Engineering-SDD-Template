# seed-data/ — Test Baseline Data Usage Instructions

> **Stage**: Tasks (Stage 4)
> **Applicable Conditions**: Required when integration tests or E2E tests exist
> **Update Timing**: Prepare before writing tasks.md

---

## Directory Structure

```
seed-data/
├── README.md                    # This file
├── users-normal.json            # Normal user data
├── users-edge-cases.json        # Edge case user data
├── [Entity]-normal.json         # Normal business data
├── [Entity]-edge-cases.json     # Edge case business data
└── [Entity]-errors.json         # Error scenario data
```

## Naming Conventions

- Format: `<entity_name>-<scenario_type>.<format>`
- Scenario Types: `normal` / `edge-cases` / `errors`
- File Formats: JSON / SQL / YAML / CSV

## Data Requirements

- Data structure must align with table definitions in `data-model.md` (field names, types, enum values match)
- Data must be realistic; avoid meaningless placeholders like `test123`, `foo/bar`
- Each entity must at least cover: normal scenarios, boundary values, exception inputs
- Sensitive data uses desensitized values (e.g. use `user@example.com` for emails)
- `password` field stores **API request inputs** (plaintext), not database stored values; application layer handles hashing

---

## Example: users-normal.json

```json
[
  {
    "email": "alice@example.com",
    "password": "SecurePass123!",
    "display_name": "Alice Wang",
    "role": "user"
  },
  {
    "email": "bob.admin@example.com",
    "password": "AdminPass456!",
    "display_name": "Bob Zhang",
    "role": "admin"
  }
]
```

## Example: users-edge-cases.json

```json
[
  {
    "_scenario": "Shortest username",
    "email": "a@b.co",
    "password": "12345678",
    "display_name": "Li"
  },
  {
    "_scenario": "Longest username (100 chars)",
    "email": "very.long.email.address.that.reaches.the.maximum.length@example.com",
    "password": "VeryLongPasswordThatReachesTheMaximumAllowedLength123!",
    "display_name": "[100 character display name]"
  },
  {
    "_scenario": "Username with special characters",
    "email": "special+chars@example.com",
    "password": "P@$$w0rd!#%",
    "display_name": "User (Special Char Test)"
  }
]
```

---

## Loading Methods

```bash
# Method 1: Load via Test Fixture
# Read files under seed-data/ directory in conftest.py / setup.ts

# Method 2: Load via Script
python scripts/load_seed_data.py --dir seed-data/

# Method 3: Load via SQL
psql -d [database_name] -f seed-data/init.sql
```
