# contracts/ — API 契约模板

> **所属阶段**：Plan（阶段三）
> **前置依赖**：architecture.md + data-model.md 确定后编写
> **格式**：OpenAPI 3.0 / Swagger（也可使用 GraphQL Schema）
> **组织方式**：按服务或业务域分文件（如 `auth-api.yaml`、`user-api.yaml`）
> **更新时机**：接口变更须先更新契约文件，再修改实现代码

---

## 目录结构

```
contracts/
├── auth-api.yaml       # 认证相关接口
├── user-api.yaml       # 用户管理接口
├── [业务域]-api.yaml   # 其他业务域接口
└── README.md           # 本文件（契约使用说明）
```

## 使用方式

```bash
# 验证契约文件格式
npx @redocly/cli lint contracts/*.yaml

# 生成 API 文档
npx @redocly/cli build-docs contracts/auth-api.yaml -o docs/api.html

# 生成 Mock Server（开发阶段前后端并行）
npx @stoplight/prism mock contracts/auth-api.yaml
```

---

## OpenAPI 模板示例（auth-api.yaml）

```yaml
openapi: 3.0.3
info:
  title: "[项目名称] - 认证服务 API"
  version: "1.0.0"
  description: "认证与授权相关接口"

servers:
  - url: http://localhost:8000/api
    description: 本地开发环境
  - url: https://api.[域名]/api
    description: 生产环境

tags:
  - name: Auth
    description: 认证相关操作

paths:
  /auth/register:
    post:
      tags: [Auth]
      summary: 用户注册
      description: 创建新用户账户（关联 spec F-001）
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
              display_name: "张三"
      responses:
        '201':
          description: 注册成功
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserResponse'
        '409':
          description: 邮箱已被注册
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'
              example:
                code: "EMAIL_EXISTS"
                message: "该邮箱已注册"
        '422':
          description: 请求参数校验失败
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResponse'

  /auth/login:
    post:
      tags: [Auth]
      summary: 用户登录
      operationId: loginUser
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/LoginRequest'
      responses:
        '200':
          description: 登录成功
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/TokenResponse'
        '401':
          description: 认证失败
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
          description: 机器可读的错误码
        message:
          type: string
          description: 人类可读的错误描述

  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

security:
  - BearerAuth: []
```

---

## 错误码规范

| 错误码 | HTTP 状态 | 说明 |
| :--- | :--- | :--- |
| `EMAIL_EXISTS` | 409 | 邮箱已被注册 |
| `INVALID_CREDENTIALS` | 401 | 邮箱或密码错误 |
| `TOKEN_EXPIRED` | 401 | Token 已过期 |
| `FORBIDDEN` | 403 | 无权限访问 |
| `NOT_FOUND` | 404 | 资源不存在 |
| `VALIDATION_ERROR` | 422 | 请求参数校验失败 |
