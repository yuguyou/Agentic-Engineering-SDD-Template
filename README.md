# Agentic Engineering + SDD Software Development Paradigm

English | **[中文](README_CN.md)**

> **Harness AI capabilities with engineering discipline. Anchor AI behavior with structured documentation.**
>
> This project provides a comprehensive practical guide to the Agentic Engineering (AE) software development paradigm, covering core theory, best practices, and a ready-to-use set of 18 standardized template files.

---

## Overview

In the Software 3.0 era, AI Agents are capable of writing and maintaining code, yet a significant gap remains between "having AI assist with coding" and "systematically integrating engineering discipline with AI capabilities." This project offers a development framework derived from first principles, designed to help engineers evolve from **Vibe Coding** (intuition-based AI programming) to **Agentic Engineering** (engineered AI orchestration).

**Core Positioning**:

- **AE as the paradigm backbone**: Defines the human-AI collaboration model — how to direct, orchestrate, and verify AI Agents
- **SDD as the supporting framework**: Provides a structured documentation system (Spec-Driven Development) that delivers traceable specifications for AE execution

> SDD addresses "AI doesn't know what to do"; AE addresses "AI knows what to do, but how to ensure it's done correctly."

---

## Theoretical Foundations and Core Practices

This framework is built upon three first-principle axioms:

| Axiom | Core Insight | Implied Solution |
| :--- | :--- | :--- |
| **Intent Transformation Chain** | Each step from human intent to executable code may introduce information loss; upstream deviations propagate furthest | Multi-layer verification + AI participation across the full chain |
| **Three LLM Characteristics** | Context-determinism, probabilistic nature, limited and volatile memory — their combination produces compounding errors | Structured documentation to anchor context + incremental verification |
| **Cognitive Scarcity** | Engineers' attention and judgment are finite bottleneck resources | Optimized cognitive allocation + stepwise review |

Six core practices are derived from these axioms:

1. **Context Engineering** — Inject high signal-to-noise context on demand
2. **Knowledge-Asymmetry-Based Human-AI Division of Labor** (Johari Window Model) — Four-quadrant collaboration strategy
3. **AI Participation Across the Full Chain** — Guide → Collaborator → Executor
4. **Small-Task Progression + Multi-Layer Verification** — Control error accumulation
5. **Knowledge Governance** (Knowledge as Code) — Engineered team knowledge management
6. **Error-Driven Feedback Loop** — Continuously distill new knowledge from mistakes

---

## Repository Structure

```
agentic-engineering/
├── README.md                        # This file: project entry point (English)
├── README_CN.md                     # 中文版 README
├── agentic_engineering.md           # Core guide: complete AE+SDD practice manual
├── agentic_engineering_files.md     # Document guide: quick reference for all documents
└── templates/                       # Template files: ready-to-use standardized templates
    ├── template_agents.md           # AGENTS.md template
    ├── template_constitution.md     # constitution.md template
    ├── template_readme.md           # README.md template
    ├── template_spec.md             # spec.md template
    ├── template_ui-spec.md          # ui-spec.md template
    ├── template_architecture.md     # architecture.md template
    ├── template_data-model.md       # data-model.md template
    ├── template_contracts.md        # contracts/ template
    ├── template_plan.md             # plan.md template
    ├── template_decisions.md        # decisions.md template
    ├── template_roadmap.md          # roadmap.md template
    ├── template_seed-data.md        # seed-data/ template
    ├── template_tasks.md            # tasks.md template
    ├── template_checklist.md        # checklist.md template
    ├── template_progress.md         # progress.md template
    ├── template_changelog.md        # changelog.md template
    ├── template_proposal.md         # proposal.md template
    └── template_manifest.md         # manifest.md template
```

---

## Getting Started

### 1. Understand the Framework

Read [`agentic_engineering.md`](agentic_engineering.md) — the core guide covering the following topics:

- Why the AE + SDD framework is necessary (Chapter 1)
- Three first-principle axioms (Chapter 2)
- Derivation and explanation of six core practices (Chapter 3)
- Five-stage SDD documentation system in detail (Chapter 4)
- Single-task execution loop and instruction specification (Chapter 5)
- Change management and continuous improvement (Chapter 6)
- New project startup checklist (Chapter 7)
- Paradigm summary (Chapter 8)

### 2. Consult the Document Specifications

Refer to [`agentic_engineering_files.md`](agentic_engineering_files.md), which presents each document in tabular form with:

- Document purpose
- Core content
- Authoring standards
- Usage instructions

### 3. Apply to Your Project

Copy the template files from the `templates/` directory into your target project, then tailor and populate as needed:

```bash
# Example: initialize the minimum document set for a new project
cp templates/template_agents.md       your-project/AGENTS.md
cp templates/template_spec.md         your-project/docs/spec.md
cp templates/template_tasks.md        your-project/docs/tasks.md
```

> **Note**: Not all projects require all 18 documents. See Section 7.2, "MVP Minimum Document Set," in the core guide — 4 documents are sufficient to bootstrap a small project.

---

## Five-Stage Document Workflow

```
Rules → Specify → Plan → Tasks → Execute
  ↓        ↓         ↓       ↓        ↓
Constrain  Define    Plan    Break    Execute &
behavior   what      how     down     verify
```

| Stage | Core Documents | Questions Addressed |
| :--- | :--- | :--- |
| **Rules** | AGENTS.md, constitution.md, README.md | How should AI behave? What constraints are inviolable? |
| **Specify** | spec.md (+ ui-spec.md) | What needs to be built? How is it accepted? |
| **Plan** | architecture.md, data-model.md, contracts/, plan.md, decisions.md, roadmap.md | What technology? How to build? What comes first? |
| **Tasks** | tasks.md, checklist.md, seed-data/ | What are the atomic tasks? Does quality meet the bar? |
| **Execute** | progress.md, changelog.md, proposal.md | Current status? What has been delivered? How to manage changes? |

### Task Complexity Tiers

Process rigor should be proportional to task risk:

| Complexity | Required Documents | Documents That May Be Omitted |
| :--- | :--- | :--- |
| **S** (Simple) | AGENTS.md (existing) | spec, architecture, plan |
| **M** (Medium) | AGENTS.md + spec.md + tasks.md | architecture, data-model |
| **L** (Complex) | Full five-stage documentation | None |
| **XL** (Critical) | Full five-stage + decisions.md + security review | None |

---

## Applicability

### Recommended

- **Production-grade projects**: Software with explicit requirements for maintainability, traceability, and quality assurance
- **Team collaboration**: Multi-person development with AI Agents where behavioral consistency is essential
- **Complex systems**: Projects spanning multiple modules, services, or involving architectural decisions
- **Long-lifecycle maintenance**: Projects requiring cross-session coherence of AI decisions

### Applicable with Simplification

- **Personal MVPs / prototyping**: Use the minimum document set (4 documents) for rapid startup
- **Small tools / scripts**: AGENTS.md plus a brief spec may suffice

### Not Necessary

- **One-off scripts**: Vibe Coding is adequate
- **Learning and experimentation**: Exploratory programming does not require documentation constraints

---

## Core Philosophy

> **You can delegate execution to AI, but you cannot delegate understanding.**

| Core Tenet | Meaning |
| :--- | :--- |
| **Specs are the product** | The spec is the single source of truth; code is a regenerable derivative |
| **Context is capability** | High-quality, high signal-to-noise context is the only leverage teams truly control |
| **Humans are the architects** | AI executes; humans own architectural decisions, taste, and final quality |
| **Tasks are the unit** | Atomic tasks with closed-loop verification are the fundamental mechanism for controlling AI error accumulation |
| **Documentation is memory** | Docs as Code — team knowledge accumulates persistently, not lost with conversations |
| **Knowledge grows** | Top-down encoding of best practices combined with bottom-up distillation from errors; knowledge evolves continuously |

---

## Acknowledgments and References

The theoretical foundations of this framework are inspired by the following work:

- **Andrej Karpathy** — Software 3.0 concept, Vibe Coding definition, operating system analogy
- **Anthropic** — Systematic Context Engineering methodology
- **Spec-Driven Development** — Structured documentation-driven development paradigm

---

## License

MIT
