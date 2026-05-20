# contracts/ — API Contract Templates

> **Stage**: Plan (Stage 3)
> **Prerequisite**: Written after architecture.md + data-model.md are confirmed
> **Format**: OpenAPI 3.0 / Swagger (GraphQL Schema can also be used)
> **Organization**: By service or business domain into separate files (e.g. `auth-api.yaml`, `user-api.yaml`)
> **Update Timing**: Interface changes must update contract files first, before modifying implementation code

---

## Directory Structure

```
contracts/
├── auth-api.yaml       # Authentication related interfaces
├── user-api.yaml       # User management interfaces
├── [Domain]-api.yaml   # Other business domain interfaces
└── README.md           # This file (contract usage instructions)
```

## Usage

```bash
# Validate contract file format
npx @redocly/cli lint contracts/*.yaml

# Generate API documentation
npx @redocly/cli build-docs contracts/auth-api.yaml -o docs/api.html

# Generate Mock Server (for frontend/backend parallel development)
npx @stoplight/prism mock contracts/auth-api.yaml
```

---

## OpenAPI Template Example (auth-api.yaml)

```yaml
openapi: 3.0.3
info:
  title: "[Project Name] - Auth Service API"
  version: "1.0.0"
  description: "Authentication and authorization related interfaces"

servers:
  - url: http://localhost:8000/api
    description: Local development environment
  - url: https://api.[domain]/api
    description: Production environment

tags:
  - name: Auth
    description: Authentication related operations

paths:
  /auth/register:
    post:
      tags: [Auth]
      summary: User registration
      description: Create a new user account (linked to spec F-001)
      operationId: registerUser
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/RegisterRequest'
            example:
              email: "user@example.com"
              password: "SecurePass123!"
              display_name: "John Doe"
      responses:
        '201':
          description: Registration successful
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserResponse'
        '409':
          description: Email already registered
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
              example:
                code: "EMAIL_EXISTS"
                message: "This email is already registered"
        '422':
          description: Request parameter validation failed
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /auth/login:
    post:
      tags: [Auth]
      summary: User login
      operationId: loginUser
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/LoginRequest'
      responses:
        '200':
          description: Login successful
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/TokenResponse'
        '401':
          description: Authentication failed
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

components:
  schemas:
    RegisterRequest:
      type: object
      required: [email, password, display_name]
      properties:
        email:
          type: string
          format: email
          maxLength: 255
        password:
          type: string
          minLength: 8
          maxLength: 128
        display_name:
          type: string
          minLength: 1
          maxLength: 100

    LoginRequest:
      type: object
      required: [email, password]
      properties:
        email:
          type: string
          format: email
        password:
          type: string

    UserResponse:
      type: object
      properties:
        id:
          type: string
          format: uuid
        email:
          type: string
        display_name:
          type: string
        role:
          type: string
          enum: [user, admin]
        created_at:
          type: string
          format: date-time

    TokenResponse:
      type: object
      properties:
        access_token:
          type: string
        token_type:
          type: string
          example: "bearer"
        expires_in:
          type: integer
          example: 3600

    ErrorResponse:
      type: object
      properties:
        code:
          type: string
          description: Machine-readable error code
        message:
          type: string
          description: Human-readable error description

  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

security:
  - BearerAuth: []
```

---

## Error Code Standards

| Error Code | HTTP Status | Description |
| :--- | :--- | :--- |
| `EMAIL_EXISTS` | 409 | Email already registered |
| `INVALID_CREDENTIALS` | 401 | Incorrect email or password |
| `TOKEN_EXPIRED` | 401 | Token has expired |
| `FORBIDDEN` | 403 | No permission to access |
| `NOT_FOUND` | 404 | Resource not found |
| `VALIDATION_ERROR` | 422 | Request parameter validation failed |
