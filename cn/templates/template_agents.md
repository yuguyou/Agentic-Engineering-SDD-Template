# AGENTS.md — AI 编码行为契约

> **所属阶段**：Rules（阶段一）
> **文件别名**：Claude Code → `CLAUDE.md` | Cursor → `.cursorrules` | 通用 → `AGENTS.md`
> **建议行数**：≤ 300 行
> **更新时机**：项目启动时创建；发现新的编码约定时及时追加

---

## 编码原则

- **先思考再编码**：接收任务后，先输出实现方案摘要，等待人类确认后再编写代码
- **保持简单**：优先选择最简单的实现方式，避免过度设计
- **精准修改**：只修改任务要求的代码，不"顺便"重构或优化不相关的部分
- **定义可验证目标**：每次实现结束后，给出具体的验证步骤或测试命令

## 禁止行为

- 禁止在未明确要求时引入新的第三方依赖
- 禁止删除或修改现有测试用例（除非任务明确要求）
- 禁止修改数据库 Schema 而不同步更新 `data-model.md`
- 禁止在代码中硬编码环境配置（API Key、数据库连接串等）
- 禁止实现 `spec.md` 中 Out of Scope 列出的功能

## 技术栈约束

> 技术栈（语言、框架、数据库等）属于不可变约束，统一在 `constitution.md` 中定义。
> AI 执行任务前须同时读取 `constitution.md` 获取技术栈信息。

## 代码风格

- 使用 [语言对应的格式化工具，如 ruff / prettier / gofmt]
- 命名规范：[如 snake_case for Python, camelCase for JS]
- 最大行宽：[如 88 字符]
- 导入排序：[如 isort 标准]
- 类型注解：[如 所有公开函数必须有类型注解]

## 测试规范

- 单元测试命令：`[如 pytest tests/unit/ -v]`
- 集成测试命令：`[如 pytest tests/integration/ -v]`
- 代码覆盖率检查：`[如 pytest --cov=src --cov-report=term-missing]`
- 测试文件命名：`test_<模块名>.py`
- 每个公开函数至少有一个正向测试和一个异常测试

## Git 规范

- 分支命名：`feature/<功能名>` / `fix/<问题描述>` / `refactor/<模块名>`
- Commit 格式：`<type>(<scope>): <description>`
  - type: feat / fix / refactor / test / docs / chore
  - 示例：`feat(auth): implement user registration API`
- 每个 task 对应一个 commit，commit message 引用 task 编号

## 项目结构

```
[项目名]/
├── src/                    # 源代码
│   ├── [模块A]/            # [模块A职责描述]
│   ├── [模块B]/            # [模块B职责描述]
│   └── [入口文件]          # 应用入口（如 main.py / index.ts / main.go）
├── tests/                  # 测试代码
│   ├── unit/               # 单元测试
│   └── integration/        # 集成测试
├── docs/                   # 项目文档（SDD 文档体系）
├── seed-data/              # 测试基础数据
├── contracts/              # API 契约文件
├── .env.example            # 环境变量模板
├── AGENTS.md               # 本文件（AI 行为契约）
├── constitution.md         # 最高技术约束
└── README.md               # 项目入口文档
```

## 输出格式要求

- 代码变更时，说明修改了哪些文件以及修改原因
- 完成任务后，输出验证步骤
- 遇到不确定的技术决策时，列出备选方案并请求人类决策，不自行做主
