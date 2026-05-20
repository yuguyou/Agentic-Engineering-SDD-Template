# Agentic Engineering + SDD 软件开发范式

**[English](README.md)** | 中文

> **以工程纪律驾驭 AI 能力，以结构化文档锚定 AI 行为。**
>
> 本项目提供一套完整的 Agentic Engineering（AE）软件开发范式实践指导，涵盖范式的核心理论、最佳实践说明，以及一套开箱即用的 18 份标准化模板文件。

---

## 项目简介

在 Software 3.0 时代，AI Agent 已具备编写和维护代码的能力，但「让 AI 辅助编码」与「将工程纪律与 AI 能力系统性结合」之间仍存在显著差距。本项目提供一套从第一性原理出发推导的开发体系，旨在帮助工程师从 **Vibe Coding**（基于直觉的 AI 编程）演进至 **Agentic Engineering**（工程化的 AI 编排）。

**核心定位**：

- **AE 为范式主线**：定义人机协作的工作方式——如何指挥、编排和验收 AI Agent
- **SDD 为配套载体**：提供结构化文档体系（Spec-Driven Development），为 AE 的执行提供可追溯的规范支撑

> SDD 解决「AI 不知道该做什么」的问题，AE 解决「AI 知道了但如何确保做对」的问题。

---

## 理论基础与核心实践

本体系建立在三条第一性原理之上：

| 公理 | 核心洞察 | 指向的解法 |
| :--- | :--- | :--- |
| **意图转化链** | 从人类意图到可执行代码，每一步均可能引入信息损耗，源头偏差传播最远 | 多层验证 + AI 全链条参与 |
| **LLM 三特征** | 上下文决定性、概率性、记忆有限且易失——三者组合产生错误累积效应 | 结构化文档锚定上下文 + 小步验证 |
| **认知稀缺** | 工程师的注意力与判断力是有限的瓶颈资源 | 最优化认知分配 + 分步审查 |

由此推导出六条核心实践：

1. **上下文工程**（Context Engineering）— 按需注入高信噪比上下文
2. **基于知识不对称的人机分工**（乔哈里窗模型）— 四象限协作策略
3. **AI 全链条参与** — 引导者 → 协作者 → 执行者
4. **小任务推进 + 多层验证** — 控制错误累积
5. **知识治理**（Knowledge as Code）— 团队知识工程化管理
6. **错误驱动的反馈闭环** — 从错误中持续沉淀新知识

---

## 仓库结构

```
agentic-engineering/
├── README.md                        # 英文版 README
├── README_CN.md                     # 本文件：项目入口
├── cn/                              # 中文文档
│   ├── agentic_engineering.md       # 核心指南：AE+SDD 完整实践手册
│   ├── agentic_engineering_files.md # 文档指南：全部文档的速查参考
│   └── templates/                   # 模板文件：开箱即用的标准化模板
│       ├── template_agents.md           # AGENTS.md 模板
│       ├── template_constitution.md     # constitution.md 模板
│       ├── template_readme.md           # README.md 模板
│       ├── template_spec.md             # spec.md 模板
│       ├── template_ui-spec.md          # ui-spec.md 模板
│       ├── template_architecture.md     # architecture.md 模板
│       ├── template_data-model.md       # data-model.md 模板
│       ├── template_contracts.md        # contracts/ 模板
│       ├── template_plan.md             # plan.md 模板
│       ├── template_decisions.md        # decisions.md 模板
│       ├── template_roadmap.md          # roadmap.md 模板
│       ├── template_seed-data.md        # seed-data/ 模板
│       ├── template_tasks.md            # tasks.md 模板
│       ├── template_checklist.md        # checklist.md 模板
│       ├── template_progress.md         # progress.md 模板
│       ├── template_changelog.md        # changelog.md 模板
│       ├── template_proposal.md         # proposal.md 模板
│       └── template_manifest.md         # manifest.md 模板
└── en/                              # 英文文档
    ├── agentic_engineering.md       # Core guide: complete AE+SDD practice manual
    ├── agentic_engineering_files.md # Document guide: quick reference for all documents
    └── templates/                   # Template files (英文对照模板)
```

---

## 使用指南

### 1. 理解体系

阅读 [`cn/agentic_engineering.md`](cn/agentic_engineering.md)，该文档为核心指南，涵盖以下内容：

- AE + SDD 体系的必要性分析（第一章）
- 三条第一性原理公理（第二章）
- 六条核心实践的推导与说明（第三章）
- SDD 文档体系的五阶段详解（第四章）
- 单任务执行循环与指令规范（第五章）
- 变更管理与持续改进（第六章）
- 新项目启动检查清单（第七章）
- 范式总结（第八章）

### 2. 查阅文档规范

参考 [`cn/agentic_engineering_files.md`](cn/agentic_engineering_files.md)，该文档以表格形式列出每份文档的：

- 文档作用
- 核心内容
- 编写规范
- 用法说明

### 3. 在项目中应用

将 `cn/templates/` 目录中的模板文件复制至目标项目，按需裁剪并填充具体内容：

```bash
# 示例：为新项目初始化最小文档集
cp cn/templates/template_agents.md       your-project/AGENTS.md
cp cn/templates/template_spec.md         your-project/docs/spec.md
cp cn/templates/template_tasks.md        your-project/docs/tasks.md
```

> **提示**：并非所有项目均需全部 18 份文档。详见核心指南第 7.2 节「MVP 最小文档集」，4 份文档即可启动小型项目。

---

## 五阶段文档流程

```
Rules → Specify → Plan → Tasks → Execute
  ↓        ↓         ↓       ↓        ↓
约束行为   定义做什么   规划怎么做  拆解行动   执行验收
```

| 阶段 | 核心文档 | 回答的问题 |
| :--- | :--- | :--- |
| **Rules** | AGENTS.md、constitution.md、README.md | AI 应如何行动？有哪些不可逾越的约束？ |
| **Specify** | spec.md（+ ui-spec.md） | 需要构建什么？如何验收？ |
| **Plan** | architecture.md、data-model.md、contracts/、plan.md、decisions.md、roadmap.md | 采用何种技术？如何构建？优先级如何？ |
| **Tasks** | tasks.md、checklist.md、seed-data/ | 原子任务是什么？质量是否达标？ |
| **Execute** | progress.md、changelog.md、proposal.md | 当前状态如何？已交付什么？如何管理变更？ |

### 任务复杂度分级

流程严格程度应与任务风险成正比：

| 复杂度 | 必需文档 | 可省略文档 |
| :--- | :--- | :--- |
| **S**（简单） | AGENTS.md（已有） | spec、architecture、plan |
| **M**（中等） | AGENTS.md + spec.md + tasks.md | architecture、data-model |
| **L**（复杂） | 完整五阶段文档 | 无 |
| **XL**（关键） | 完整五阶段 + decisions.md + 安全审查 | 无 |

---

## 适用场景

### 推荐采用

- **生产级项目**：对可维护性、可追溯性和质量保证有明确要求的正式软件工程
- **团队协作**：多人使用 AI Agent 协同开发，需保证行为一致性
- **复杂系统**：涉及跨模块、多服务、架构决策的工程项目
- **长周期维护**：需跨会话保持 AI 决策连贯性的持续迭代项目

### 可简化使用

- **个人 MVP / 原型验证**：采用最小文档集（4 份文档）即可快速启动
- **小型工具 / 脚本**：仅需 AGENTS.md 与简要 spec

### 无需使用

- **一次性脚本**：直接采用 Vibe Coding 方式即可
- **学习与实验**：探索性编程无需文档约束

---

## 核心哲学

> **可以委托 AI 执行，但不可委托 AI 理解。**

| 核心要素 | 含义 |
| :--- | :--- |
| **规范是产品** | Spec 是唯一事实来源，代码是可再生的衍生物 |
| **上下文即能力** | 高质量、高信噪比的上下文是团队真正可控的提效杠杆 |
| **人类是架构师** | AI 是执行者，人类负责架构决策、品味判断与最终质量 |
| **任务是单元** | 原子化任务与闭环验证是控制 AI 错误累积的根本手段 |
| **文档即记忆** | 文档与代码同仓库（Docs as Code），团队知识持续沉淀，不随对话消散 |
| **知识在生长** | 自上而下编码最佳实践，自下而上从错误中提炼，知识持续演进 |

---

## 致谢与参考

本体系的理论基础受以下工作启发：

- **Andrej Karpathy** — Software 3.0 概念、Vibe Coding 定义、操作系统类比
- **Anthropic** — Context Engineering 系统化方法论
- **Spec-Driven Development** — 结构化文档驱动的开发范式

---

## License

MIT
