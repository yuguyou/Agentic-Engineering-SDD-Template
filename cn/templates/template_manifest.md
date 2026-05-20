# manifest.md — 文档地图与元数据

> **所属**：补充文档
> **性质**：可解析的文档地图，支持自动化依赖分析
> **更新时机**：每新增或修改核心文档时同步更新

---

## 文档状态总览

> 状态枚举：📝 草稿 | 👀 已评审 | ✅ 已实施 | ⚠️ 待更新 | ❌ 已废弃

| 阶段 | 文档 | 路径 | 版本 | 状态 | 创建日期 | 最后更新 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Rules** | AGENTS.md | `./AGENTS.md` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |
| | constitution.md | `./constitution.md` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |
| | README.md | `./README.md` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |
| **Specify** | spec.md | `./docs/spec.md` | 1.0 | 👀 已评审 | YYYY-MM-DD | YYYY-MM-DD |
| | ui-spec.md | `./docs/ui-spec.md` | — | 📝 草稿 | — | — |
| **Plan** | architecture.md | `./docs/architecture.md` | 1.0 | 👀 已评审 | YYYY-MM-DD | YYYY-MM-DD |
| | data-model.md | `./docs/data-model.md` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |
| | contracts/ | `./contracts/` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |
| | plan.md | `./docs/plan.md` | 1.0 | 👀 已评审 | YYYY-MM-DD | YYYY-MM-DD |
| | decisions.md | `./docs/decisions.md` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |
| | roadmap.md | `./docs/roadmap.md` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |
| **Tasks** | seed-data/ | `./seed-data/` | — | 📝 草稿（按需） | — | — |
| | tasks.md | `./docs/tasks.md` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |
| | checklist.md | `./docs/checklist.md` | 1.0 | 📝 草稿 | YYYY-MM-DD | YYYY-MM-DD |
| **Execute** | progress.md | `./docs/progress.md` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |
| | changelog.md | `./CHANGELOG.md` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |
| | proposal.md | `./docs/proposal.md` | — | — | — | — |
| **补充** | manifest.md | `./docs/manifest.md` | 1.0 | ✅ 已实施 | YYYY-MM-DD | YYYY-MM-DD |

---

## 文档关联关系

> 格式：文档A → 关系 → 文档B

```
# Rules 阶段约束（贯穿全流程）
constitution.md  → 约束   → AGENTS.md
constitution.md  → 约束   → architecture.md
constitution.md  → 约束   → plan.md（技术栈基线）

# Specify → Plan
spec.md          → 驱动   → architecture.md
spec.md          → 驱动   → roadmap.md
ui-spec.md       → 驱动   → tasks.md（UI 相关任务）

# Plan 内部依赖
architecture.md  → 产出   → data-model.md
architecture.md  → 产出   → contracts/
architecture.md  → 产出   → plan.md
data-model.md    → 输入   → plan.md（Schema 约束实现方案）
contracts/       → 输入   → plan.md（接口约束实现方案）
decisions.md     → 记录   → architecture.md（决策依据）

# Plan → Tasks
plan.md          → 拆解为 → tasks.md
roadmap.md       → 排期   → tasks.md
seed-data/       → 提供   → tasks.md（测试数据支撑）

# Tasks → Execute
tasks.md         → 验收   → checklist.md
tasks.md         → 追踪   → progress.md

# Execute 内部
progress.md      → 汇总   → changelog.md
checklist.md     → 门控   → changelog.md

# 变更闭环
proposal.md      → 触发   → spec.md（变更闭环）
```

---

## 变更历史

| 日期 | 变更文档 | 变更类型 | 说明 |
| :--- | :--- | :--- | :--- |
| YYYY-MM-DD | manifest.md | 创建 | 初始化文档地图 |
| YYYY-MM-DD | spec.md | 更新 | 新增 F-006 功能条目 |
