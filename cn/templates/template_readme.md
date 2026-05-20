# [项目名称]

> [一句话描述项目解决的核心问题]

---

## 项目背景

[2-3 句话描述项目的业务背景和目标用户]

## 核心功能

- **[功能1]**：[简要描述]
- **[功能2]**：[简要描述]
- **[功能3]**：[简要描述]

## 技术栈

| 类别 | 技术 | 版本 |
| :--- | :--- | :--- |
| 编程语言 | [如 Python] | [如 3.12] |
| Web 框架 | [如 FastAPI] | [如 0.115] |
| 数据库 | [如 PostgreSQL] | [如 16] |
| ORM | [如 SQLAlchemy] | [如 2.0] |
| 测试框架 | [如 pytest] | [如 8.x] |
| 包管理器 | [如 uv] | [如 latest] |

## 环境搭建

### 前置要求

- [如 Python 3.12+]
- [如 PostgreSQL 16+]
- [如 Docker（可选）]

### 一键启动

```bash
# 1. 克隆仓库
git clone [仓库地址]
cd [项目目录]

# 2. 安装依赖
[如 uv sync / npm install / pip install -r requirements.txt]

# 3. 配置环境变量
cp .env.example .env
# 编辑 .env 文件，填入必要配置

# 4. 初始化数据库
[如 alembic upgrade head / prisma migrate dev]

# 5. 启动开发服务器
[如 uvicorn src.main:app --reload / npm run dev]
```

### 验证安装

```bash
# 运行测试
[如 pytest tests/ -v]

# 检查服务状态
[如 curl http://localhost:8000/health]
```

## 核心文档索引

> 本项目遵循 **Agentic Engineering + SDD** 开发体系（五阶段：Rules → Specify → Plan → Tasks → Execute）。

| 阶段 | 文档 | 说明 | 路径 |
| :--- | :--- | :--- | :--- |
| **Rules** | AGENTS.md | AI 编码行为契约 | `AGENTS.md` |
| | constitution.md | 最高技术约束与质量红线 | `constitution.md` |
| **Specify** | spec.md | 唯一真理来源（需求规范） | `docs/spec.md` |
| | ui-spec.md | UI 实现契约（按需） | `docs/ui-spec.md` |
| **Plan** | architecture.md | 系统架构蓝图 | `docs/architecture.md` |
| | data-model.md | 数据持久化模型 | `docs/data-model.md` |
| | contracts/ | API 硬契约 | `contracts/` |
| | plan.md | 技术实施路径 | `docs/plan.md` |
| | decisions.md | 架构决策记录 | `docs/decisions.md` |
| | roadmap.md | 交付路线图 | `docs/roadmap.md` |
| **Tasks** | tasks.md | 原子化行动清单 | `docs/tasks.md` |
| | checklist.md | 发布前质量关卡 | `docs/checklist.md` |
| **Execute** | progress.md | 在途状态仪表盘 | `docs/progress.md` |
| | changelog.md | 已交付成果档案 | `CHANGELOG.md` |

## 目录结构

```
[项目名]/
├── src/                    # 源代码
├── tests/                  # 测试代码
├── docs/                   # SDD 文档体系
│   ├── spec.md
│   ├── ui-spec.md          # 按需
│   ├── architecture.md
│   ├── data-model.md
│   ├── plan.md
│   ├── decisions.md
│   ├── roadmap.md
│   ├── tasks.md
│   ├── checklist.md
│   ├── progress.md
│   ├── proposal.md         # MVP 后
│   └── manifest.md
├── contracts/              # API 契约
├── seed-data/              # 测试基础数据（按需）
├── .env.example            # 环境变量模板
├── AGENTS.md               # AI 行为契约
├── constitution.md         # 技术约束
├── CHANGELOG.md            # 交付记录
└── README.md               # 本文件
```

## License

[如 MIT / Apache 2.0 / 私有]
