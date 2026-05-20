# Agentic Engineering Software Development Guide

> This guide uses **Agentic Engineering (AE)** as the main paradigm and **Spec-Driven Development (SDD)** as the supporting documentation system, integrating them into a complete software development framework for the AI era:
> - **AE is the main paradigm**: Defines the human-machine collaboration workflow — how to direct, orchestrate, and validate AI Agents.
> - **SDD is the supporting vehicle**: Provides a structured documentation system, offering traceable specification support for AE execution.
>
> This document deduces core practices from first principles, and grounds them in an actionable documentation system and execution workflow.

---

## I. Why do we need the AE + SDD System?

### 1.1 Software 3.0 and the Rise of Agentic Engineering

#### The Three Generations of Software Evolution

Andrej Karpathy divides software evolution into three generations:

| Era | Core Method | Programming Language | Typical Scenario |
| :--- | :--- | :--- | :--- |
| **Software 1.0** | Humans write explicit logic instructions | C++, Python, Java | Traditional app development |
| **Software 2.0** | Neural networks learn parameters from data | Datasets + Training goals | Tesla Autopilot, Recommender Systems |
| **Software 3.0** | Natural language drives LLMs to execute tasks | Natural Language (Prompt) | AI Agents writing and maintaining code |

#### The Operating System Analogy

In the Software 3.0 era, Karpathy proposed a precise architectural analogy to help engineers understand the new paradigm:

```
Model Weights = CPU        → Fixed processing engine (reasoning capability)
Context Window = RAM       → Limited working memory (all info for the current task)
Prompt = Programming Lang. → Controlling output via natural language "programming"
```

The key insight of this analogy is: **The Context Window is the core leverage point**. Just as programmers control program behavior by managing data in RAM, Software 3.0 engineers control AI output by managing information in the context window. The engineer's role shifts from "someone who writes code" to "an architect who manages AI context."

### 1.2 From Vibe Coding to Agentic Engineering

#### The Value and Limitations of Vibe Coding

Vibe Coding is a popular early practice in Software 3.0: developers describe requirements in natural language, directly accept AI output, and iterate quickly based on intuition.

**Value**: Greatly lowers the barrier to software development, allows fast prototype validation, and is suitable for personal projects and small tools. Karpathy calls this "raising the floor" — allowing more people to build software.

**Limitations**: The essence of Vibe Coding is **trading understanding and control for speed**, which cannot support the quality requirements of production-grade systems:
- **Inability to control quality**: AI black-box generation, no systematic acceptance mechanism.
- **Unscalable**: AI behavior is inconsistent during multi-person collaboration, leading to chaotic code styles.
- **Rapid accumulation of technical debt**: Code accepted by intuition often lacks edge cases and error handling.
- **Unfit for production**: No guarantees for security, performance, and maintainability.

#### Definition of Agentic Engineering

Agentic Engineering is the professional evolution of Vibe Coding, aimed at "raising the ceiling." The core shift is:

> **No longer "letting AI write code for you", but "systematically combining engineering discipline with AI capabilities"**

The unit of programming shifts from "writing lines of code" to "delegating macro actions" — such as "implement this feature", "refactor this subsystem", "design the API for this module". The engineer acts as the architect, orchestrator, and validator, while AI is the powerful but imperfect executor.

**The fundamental shift in bottlenecks**: In the AI era, the core value of developers is no longer coding speed, but **architectural taste, technical judgment, and validation capability**.

> "You can outsource your thinking, but you cannot outsource your understanding." — Karpathy quoted this in multiple presentations (original source is X user @kache)

| Dimension | Vibe Coding | Agentic Engineering |
| :--- | :--- | :--- |
| **Interaction Mode** | 1 Developer vs 1 AI Chatbox | 1 Architect vs N Autonomous Agents |
| **Core Logic** | See what → Say what → Run what | Define specs → Orchestrate tasks → Validate |
| **Programming Unit** | Hand-written lines of code | Delegated macro actions |
| **Code Control** | AI black-box generation, eyeball tests | Spec-driven generation, automated validation |
| **Key to Success** | Prompting tricks | Engineering Orchestration |
| **Applicable Scale** | Prototypes, MVP, small tools | Enterprise apps, complex refactors, long-term maintenance |

---

## II. First Principles: Three Axioms

> This chapter establishes the theoretical foundation for all subsequent practice deductions. The three axioms define the three basic elements of human-machine collaboration — **Activity** (what we are doing), **Tool** (what we use), **Human** (who is doing it) — each independent and cannot be deduced from one another.

### 2.1 Axiom 1: The Intent Translation Chain and Information Loss

> **The essence of software engineering is translating vague intents in human minds, through a series of information transformations, into precise machine-executable code. Every step in this chain can introduce information loss.**

```
Human Intent → NL Requirements → Structured Design → Formal Code → Executable Program
```

The inherent challenges of software engineering — misunderstood requirements, design deviations, implementation errors — are all manifestations of loss at different points in this chain. Decades of engineering methodologies (requirement reviews, design docs, code reviews, testing systems) are essentially setting up **checkpoints** at various links in the chain to capture and repair loss.

**Key Corollaries**:
- **Source loss propagates the furthest**: Deviations at the requirements and design stages are amplified in every subsequent step, and the cost of fixing them grows exponentially.
- **AI has not eliminated this chain**: AI has changed how each link is executed and the loss rate, but the chain itself always exists. AI's probabilistic nature introduces a new source of loss — not human misunderstanding, but AI's "plausible but incorrect" hallucinations.
- **The necessity of multi-layer validation**: "Correctness" means different things at each layer of the chain (Intent Correct ≠ Design Correct ≠ Function Correct ≠ Performance Met). Validation strategies must align with the chain's layers.

### 2.2 Axiom 2: The Three Essential Characteristics of LLMs

> **An LLM is a probabilistic reasoning system based on context, possessing three parallel essential characteristics.**

#### Characteristic 1: Context Determinism

An LLM's output is strictly determined by the context it receives — it reasons based on whatever information it is given. It knows nothing about knowledge outside its training data (team business logic, internal architectural decisions, coding standards) — it's not "not smart enough", it just "doesn't know".

**Corollary**: Model capability is a given constant; **context quality is the true efficiency lever the team can control**. What truly affects AI output is not the amount of code, but the knowledge behind the code — reasons for architectural decisions, implicit contracts between modules, subtle coding standards.

#### Characteristic 2: Probabilistic Nature

An LLM is essentially "predicting the next Token" based on probability. The same input can produce different outputs; this is not a defect but a fundamental architectural property. Capability boundaries are hard to predict precisely, and output correctness cannot be guaranteed.

**Corollary**:

**Error Accumulation Effect** — On the intent translation chain (Axiom 1), unchecked deviations at each step become the input premise for the next step. Deviations don't naturally dissipate; they tend to accumulate and amplify:

```
Small deviation → Unchecked → Becomes next input → Deviation amplified → Final result deviates heavily from intent
```

Asking AI to complete multi-step tasks all at once almost inevitably results in deviations from the original intent, and the more complex the task, the worse the deviation.

#### Characteristic 3: Finiteness and Volatility of Working Memory

An LLM's context window has both a capacity limit and is volatile:
- **Finite**: Ultra-long contexts suffer from the "Lost in the Middle" phenomenon — the model's accuracy in recalling middle-position information drops significantly.
- **Volatile**: Once a session ends, all discussion conclusions and decision histories are wiped to zero; there is no persistent memory across sessions.
- **Lossy Compression**: When context exceeds window limits, frameworks use compaction mechanisms, but deciding what information is "critical" is itself a lossy judgment.

**Corollary**: Without specification documents, AI will re-guess technical decisions in every new session. The same problem might get different answers in different sessions, leading to chaotic code styles and massive rework.

#### Combined Effects of the Three Characteristics

The three characteristics are not isolated; their **combination** produces the most profound impacts:

| Combination | Effect | Response Strategy |
| :--- | :--- | :--- |
| Context Determinism + Probabilistic | Context quality determines the upper limit of expected output quality, but doesn't guarantee correctness | High Signal-to-Noise Context + Validation |
| Probabilistic + Intent Chain | Exponential error accumulation in multi-step tasks | Small-step progression + Step-by-step validation |
| Volatile Memory + Context Determinism | Inconsistent behavior across sessions, AI cannot autonomously maintain decision continuity | Structured documents as persistent memory |
| Finite Memory + Context Determinism | Critical info squeezed out/diluted, decision quality drops late in long tasks | On-demand injection + Progressive disclosure |

### 2.3 Axiom 3: Human Cognition is a Scarce Resource

> **An engineer's attention, judgment, and decision-making capabilities are limited and constitute the bottleneck of the entire human-machine collaboration system.**

This is a fundamental conclusion of cognitive psychology — working memory capacity is limited, attention is a zero-sum resource, and decision fatigue is real — and it doesn't change with technological progress.

In the AI era, the main factor restricting output is no longer coding speed, but the upper limit of engineers' **reviewing, judging, and decision-making** capabilities. When AI generates hundreds of lines of code per hour waiting for review, the problem is no longer "can't write it", but "can't finish reading it, can't think clearly about it".

**Key Corollaries**:
- **The optimal strategy is not to maximize AI's output volume, but to optimize the allocation of engineer's cognitive bandwidth** — liberating engineers from mechanical work (looking up APIs, writing boilerplate, constructing test data) to focus on architectural judgment and system design.
- **Small changes are easier to review than large changes** — facing a massive unreviewed change, reviewers must rebuild context from scratch, incurring much higher cognitive costs than step-by-step reviews.
- **AI-guided > AI direct solutions** — letting humans understand the problem themselves under AI guidance costs less cognition than AI giving a solution directly and humans having to reconstruct understanding from scratch.

### 2.4 How the Three Axioms Point to AE + SDD

The three axioms respectively point to the necessity of two major solutions:

| Axiom | Core Challenge Revealed | Pointed Solution |
| :--- | :--- | :--- |
| **Axiom 1** (Intent Chain) | Source loss propagates furthest, multi-step deviations accumulate | **AE**: Multi-layer validation + AI full-chain participation |
| **Axiom 2** (LLM Traits) | Output determined by context, probablity can't be eliminated, volatile memory | **SDD**: Spec docs anchor context + **AE**: Small-step validation controls deviations |
| **Axiom 3** (Cognitive Scarcity)| Human review capacity is bottleneck, can't infinitely increase AI output | **AE**: Optimize cognitive allocation + Step-by-step review |

The complementary relationship between the two:

```
SDD (Foundation)                         AE (Way of Working)
──────────────────────────────           ──────────────────────────────
Spec docs anchor "what to do"      +     Context Engineering gives AI precise context
Docs constrain AI behavior bounds  +     Human-Machine Division decides what to give AI
Code is traceable to spec entries  +     Closed-loop validation ensures each step is reliable
```

> **In one sentence**: SDD solves the "AI doesn't know what to do" problem, and AE solves the "AI knows but how to ensure it's done right" problem.

---

## III. Core Practices

> The following six practices are deduced from the three axioms, forming a progressive structure: **Practice 1** builds the context generation and loading mechanism; **Practice 2** defines human-machine division based on knowledge asymmetry; **Practice 3** expands AI's involvement from coding to the full chain; **Practice 4** controls error accumulation through small tasks and multi-layer validation; **Practice 5** governs team knowledge using engineering methods; **Practice 6** extracts experience from errors to form a feedback loop.

### 3.1 Context Engineering

**Deduction Basis**: Axiom 2 (Context Determinism + Finite Memory) constitutes the core contradiction — complex systems require more context to guarantee quality, but the amount of context AI can consume is limited.

Context Engineering is the systematic method to solve this contradiction. Karpathy defines it generally as "the subtle art and science of packing the context window to get the right information for the next step"; Anthropic further systematized it in their engineering blog as:

> **The strategy for curating and maintaining the optimal set of Tokens during LLM reasoning** — covering system instructions, tools, external data, message history, and all other information that might enter the context window. Its guiding principle is: **Finding the minimal, high-signal Token set that maximizes the likelihood of producing the desired result.**

Unlike Prompt Engineering, which only focuses on writing single-turn instructions, Context Engineering focuses on **dynamic management of the entire context state** over multi-turn reasoning and long time spans. Specifically, it needs to solve three problems:

#### 3.1.1 Structured Persistence: Making Tacit Knowledge Explicit as Documents

What truly affects AI output quality is often not the code itself, but the knowledge behind it — reasons for architectural decisions ("why choose event-driven over synchronous calls"), implicit contracts between modules ("Service A must initialize before Service B"), subtle coding standards ("all DB operations must go through Repository layer"). This knowledge isn't in the code because code expresses "what to do", not "why do it this way".

**SDD's Solution**: Use structured documents like spec.md, architecture.md, AGENTS.md to explicitly turn tacit knowledge into persistent memory consumable by AI. Documents are persistent; when AI reloads documents each session, behavior becomes reproducible and predictable.

#### 3.1.2 Docs as Code: Documents and Code in the Same Repository

Completed specification documents are saved in the repository as code, version-controlled together with the source code:
- **Retrievable**: When AI needs context for a module, it retrieves the corresponding document directly from the repo, instead of relying on temporary human dictation.
- **Traceable**: Document changes have Git history, corresponding one-to-one with code changes.
- **Anti-stale**: Expired documents are more dangerous than no documents — they inject incorrect context. Same repo, same branch, same MR workflow naturally keeps them in sync.

#### 3.1.3 Progressive Injection: On-Demand Loading to Avoid Context Rot

As the number of Tokens in the context window increases, the model's ability to accurately recall information gradually declines — this isn't a sudden cliff, but a continuous decay of performance gradients (Context Rot).

**Solution**: Shift from pre-loading all data to a "just-in-time" context strategy — injecting context needed for the current task on-demand, rather than dumping everything at once:

| Context Type | Loading Strategy | Example |
| :--- | :--- | :--- |
| **Rules** (Global constraints)| Pre-load at session start | AGENTS.md, constitution.md |
| **Spec** (Task spec) | Reference on-demand for current task | Specific entries in spec.md |
| **Skills** (Domain knowledge)| Load only when triggered | Coding standards, design principles |
| **External Data** | Fetch dynamically via tool calls | API docs, DB Schema |

The goal isn't to stuff all information to AI, but to provide a **minimal, high signal-to-noise context set**: give the right knowledge, at the right time, in the right format.

### 3.2 Human-Machine Division Based on Knowledge Asymmetry (Johari Window Model)

**Deduction Basis**: Axiom 2 (Context Determinism) defines AI's knowledge boundary — abundant general knowledge, zero private knowledge; Axiom 3 defines human capability boundaries — limited cognitive resources, impossible to be an expert in all domains.

The **intersection** of these two boundaries produces four knowledge states, each corresponding to a different optimal collaboration strategy:

| | **AI Knows** (General Knowledge) | **AI Doesn't Know** (Private Knowledge) |
| :--- | :--- | :--- |
| **Human Knows** | **Open Area**: Extreme Automation | **Blind Area**: Context Injection |
| **Human Doesn't Know**| **Hidden Area**: Knowledge Leverage | **Unknown Area**: Collaborative Exploration |

#### Open Area: Human Knows + AI Knows → Extreme Automation

Intent is clear and belongs to general knowledge — AI has all information, human intervention only adds delay.

**Strategy**: Issue direct instructions, maximize automation.
**Scenarios**: Generating boilerplate code, writing unit tests, formatting refactors, standard CRUD implementation.

#### Blind Area: Human Knows + AI Doesn't Know → Context Injection

Tasks involving team private knowledge; AI has no way of knowing. Without explicit injection, AI can only guess based on general knowledge — this is the root cause of "AI generated code doesn't meet project standards".

**Strategy**: Inject private context through carriers like spec, Rules, Skills.
**Scenarios**: Tasks involving internal architectural constraints, specific coding standards, business logic.

#### Hidden Area: Human Doesn't Know + AI Knows → Knowledge Leverage

Human lacks professional knowledge in a domain, but AI's training data happens to cover it.

**Strategy**: Use AI's broad knowledge to fill human shortcomings and expand capability boundaries.
**Scenarios**: Taking over an unfamiliar tech stack, troubleshooting unfamiliar compiler errors, learning best practices of a new framework.

#### Unknown Area: Both Uncertain → Collaborative Exploration

Neither party can independently provide the answer.

**Strategy**: Iterative exploration — human provides hypotheses and direction judgments, AI provides verification ideas and solution generation, both gradually approach the answer in a loop.
**Scenarios**: Complex root cause analysis, brand new architecture design, unknown tradeoffs in tech selection.

**Core Principle of Division**: Identify which quadrant the current task falls into, and adopt the corresponding collaboration strategy. A simple heuristic — ask yourself two questions: (1) Does this task involve team private knowledge? (2) Do I know exactly how to do it? The combination of the two answers maps directly to the four quadrants.

### 3.3 AI Full-Chain Participation: Guide → Collaborator → Executor

**Deduction Basis**: Axiom 1 (Source loss propagates furthest) + Axiom 3 (Cognitive scarcity, early stages especially consume cognition).

AI shouldn't only participate in the coding phase. Looking at the intent translation chain, the cost of repairing loss in earlier stages is higher. When AI is provided with sufficient domain context, the marginal cost of participating in early stages is low (mostly conversational interaction), but the benefits are continuously amplified downstream.

Unfolding the Johari Window model along the intent translation chain, AI's role progresses across different stages as knowledge states change:

#### Requirement Clarification Stage: AI as "Guide"

Tasks mostly fall into the **Blind Area** (human has business intent but unstructured) and **Hidden Area** (AI can help discover omissions).

AI uses structured questioning to help engineers make vague intents explicit into specs, and uses general knowledge to discover what humans haven't considered:
- Edge conditions and exception paths
- Implicit constraints and prerequisite dependencies
- Design patterns and known pitfalls of similar systems

**Why "Guide" instead of "Solution Provider"**: Humans are the final approvers of all subsequent decisions — if they don't deeply understand the problem themselves, subsequent reviews and decisions become blind approvals. Letting humans arrive at conclusions themselves under AI guidance is the lowest cognitive cost path (Axiom 3).

#### Solution Design Stage: AI as "Collaborator"

After spec explicitly injects private knowledge, tasks move from the blind area to the **Open Area**. AI's role upgrades — actively analyzing solution tradeoffs, proposing alternative designs, checking consistency with architectural constraints, identifying scalability or performance risks. Humans make the final design decisions.

#### Coding & Testing Stage: AI as "Executor"

With spec and design documents serving as high-quality context, most of the task enters the **Open Area**. AI can take on greater autonomy — writing implementation code, generating test cases, executing refactoring tasks.

**Positive Loop**: Structured documents generated at each stage naturally become high-quality context for the next stage — requirement clarification outputs spec, spec guides design, design docs guide coding. Context Engineering requirements are progressively satisfied, not solved all at once.

### 3.4 Small-Task Progression + Multi-Layer Validation

**Deduction Basis**: Axiom 2 (Probability → Error accumulation + Finite memory → Context degradation) + Axiom 3 (Cognitive cost of reviewing large changes is much higher than step-by-step reviews).

#### Small-Task Progression: Controlling Error Accumulation

**Must break large tasks down into independently verifiable sub-tasks; each step executed by AI, validated by human, and only proceeding after passing.** This simultaneously controls three risks:

| Risk | Control Mechanism |
| :--- | :--- |
| Error Accumulation | Step-by-step validation prevents deviation amplification |
| Context Degradation| Build focused context for each sub-task, instead of continuously appending in bloated sessions |
| Validation Cost | Small changes are easier to review than large changes (Axiom 3) |

**Task Granularity**: 30min-2h is ideal (S/M/L). The denser the constraints (involving concurrency, auth, security), the shorter the steps should be; tasks with fewer constraints (boilerplate, formatting) can give AI more autonomy.

#### Multi-Layer Validation: Aligning with Intent Translation Chain

Axiom 1 tells us that intent undergoes multiple transformations on the chain, and the meaning of "correct" is different at each layer. Validation strategies must align with the chain layers; testing alone is not enough:

| Validation Layer | What to Verify | Method |
| :--- | :--- | :--- |
| **Intent Layer** | Doing the right thing | Requirement review, spec cross-check |
| **Implementation Layer** | Code meets standards | Code Review, compliance checks |
| **Behavior Layer** | Functionality is correct | Automated testing (Unit/Integration/E2E) |
| **System Layer** | Performance/Security met | Load testing, security review |

**Testing is a necessary condition, but not sufficient**. "Passing tests" only covers the behavior layer — it cannot catch design-layer deviations like "functionally correct but architecturally conflicting", nor can it find implementation-layer defects like naming standard violations or concurrency model issues.

### 3.5 Knowledge Governance (Knowledge as Code)

**Deduction Basis**: Axiom 3 (Cognitive scarcity → Team members' expertise is unevenly distributed) + Axiom 2 (Context determinism → AI can only use knowledge it can "see").

The team's most valuable shared knowledge — best practices, design principles, coding standards — is often locked in the brains of a few senior engineers. In traditional models, knowledge transfer relies on mentoring during Code Reviews, which is inefficient and unscalable.

**Solution**: Manage shared team knowledge like code — encode it into structured Skills and Rules, store it in the repo, version-controlled, reviewable, and iterable:

- **Publicization of Knowledge**: When a senior engineer's design principles are encoded as a Skill, AI becomes the carrier of knowledge distribution — every team member automatically gets the blessing of team best practices when collaborating with AI, largely leveling out internal capability differences.
- **Evolvability of Knowledge**: Skills and Rules share the same repo and workflow as code — propose changes via MR, reach consensus via Review, trace evolution via version history.

**Division of Skills and Rules**:

| Carrier | Loading Method | Applicable Content | Size Requirement |
| :--- | :--- | :--- | :--- |
| **Rules** | Full pre-load (at start of each session) | Extremely lightweight global constraints | Strictly control, dozens of lines |
| **Skills** | On-demand triggered loading | Coding standards, arch constraints, domain knowledge | Can be larger, only consumes context when relevant |

**Three-Layer Progressive Disclosure**: Large amounts of Skills won't drag down the context window:

| Level | Content | Loading Timing | Token Cost |
| :--- | :--- | :--- | :--- |
| **L1: Metadata** | YAML frontmatter (name, desc) | Agent startup | ~100/Skill |
| **L2: Instructions** | SKILL.md main instructions | When Skill is triggered | < 5k |
| **L3: Resources** | Ref docs, scripts, static assets | When explicitly referenced | On-demand |

### 3.6 Error-Driven Feedback Loop (Error-Driven Refinement)

**Deduction Basis**: Axiom 2 (Volatile memory → Errors corrected in Session A will likely happen again in Session B) + Axiom 1 (Many losses on the intent chain are patterned and repeatable) + Axiom 3 (Repeatedly correcting similar errors wastes cognitive resources).

Practice 3.5 is **top-down** knowledge supply — encoding existing best practices. But much critical knowledge doesn't exist at the start of a project; it emerges gradually through making and correcting mistakes during development.

**We must establish a feedback mechanism from errors to persistent rules**, triggered via two complementary paths:

#### Auto-Trigger: Proactive Extraction when AI is Corrected

When AI is corrected by the user during collaboration, it automatically evaluates the root cause of the error, searches existing Rules and Skills to see if there are already rules for this type of issue. If not, it suggests creating or updating the corresponding Rule/Skill, executing it upon user confirmation. This makes knowledge accumulation a natural byproduct of the development workflow.

#### Manual Trigger: Centralized Precipitation After Session Ends

The user proactively initiates a reflection; AI reviews the current conversation history, identifies corrected error patterns, diagnoses root causes, and proposes specific Rule/Skill modification suggestions. Suitable for centralizing and precipitating accumulated experience after a round of intensive collaboration.

**Core Loop**: Make a mistake → Diagnose root cause → Retrieve existing knowledge → Create/Update Rule/Skill → Prevent recurrence.

> Practice 3.5 encodes existing knowledge top-down, and Practice 3.6 grows new knowledge from errors bottom-up — together they form a complete knowledge lifecycle.

---

## IV. SDD Documentation System

> Use structured documents to constrain AI behavior, providing a traceable source of truth for all implementations. This chapter grounds core practices into a specific documentation system.

### 4.1 Five-Stage Overview and Task Complexity Grading

#### Five-Stage Document Workflow

```
Rules → Specify → Plan → Tasks → Execute
  ↓        ↓         ↓       ↓        ↓
Constraints  What to do  How to do  Breakdown Actions  Validation
```

| Stage | Core Documents | Questions Answered |
| :--- | :--- | :--- |
| **Rules** | AGENTS.md, constitution.md, README.md | How should AI act? What are the hard constraints? What is the project overview? |
| **Specify**| spec.md (+ ui-spec.md) | What to build? How to accept? |
| **Plan** | architecture.md, data-model.md, contracts/, plan.md, decisions.md, roadmap.md | What tech? How to construct? What to do first? |
| **Tasks** | tasks.md, checklist.md, seed-data/ (as needed) | What are the atomic tasks? Is quality met? |
| **Execute**| progress.md, changelog.md, proposal.md (post-MVP) | Current status? What was delivered? How to manage changes? |

#### Task Complexity Grading: Process rigor should scale with task risk

**Not all tasks require the full five-stage process.** Simple bug fixes don't need a full spec, but complex cross-module refactors must go through the full chain. Assess task complexity first, then decide process depth:

| Complexity | Characteristics | Required Documents | Skippable Documents |
| :--- | :--- | :--- | :--- |
| **Small** (S) | Single file, local change, clear intent | AGENTS.md (existing) | spec, architecture, plan |
| **Medium** (M) | Multi-file, single module, clear boundaries| AGENTS.md + spec.md + tasks.md | architecture, data-model |
| **Large** (L) | Multi-module, cross-service, design needed | Full 5-stage documents | None |
| **Critical** (XL)| Arch changes, security, data migrations | Full 5-stage + decisions.md + security review | None |

**Heuristic**: Ask yourself three questions — (1) How many files/modules involved? (2) Does it require design decisions? (3) How high is the cost of a mistake? The larger the answers, the more complete the process.

### 4.2 Rules Stage: Setting AI Behavior Constraints

> Before any development work begins, first set immutable constraints and context for AI and the team.

#### AGENTS.md — AI Coding Behavior Contract

Solidifies AI's cross-session coding behavior. File names vary by tool: Claude Code uses `CLAUDE.md`, Cursor uses `.cursorrules`, universal standard is `AGENTS.md`. Keep under 300 lines.

**Core Template**:

```markdown
## Coding Principles
- Think before coding: understand requirements, output plan, wait for confirmation
- Precise modification: only modify required code
- Define verifiable goals: provide verification steps after implementation

## Prohibited Behaviors
- Do not introduce new dependencies unless explicitly asked
- Do not delete existing tests
- Do not modify DB Schema without updating data-model.md

## Tech Stack Constraints
- Language: [Language & Version]
- Framework: [Framework & Version]
- Test Framework: [Framework]

## Project Structure
[Briefly describe directory structure and module responsibilities]
```

#### constitution.md — Highest Technical Constraints & Quality Baselines

The "constitution" of the project, constraining all technical decisions to prevent architectural drift:

```markdown
## Technical Constraints
- Language: Use only [Language & Version]
- Database: Use only [Database]
- Environment: [Environment description]

## Quality Baselines
- Test coverage must be ≥ [Threshold]%
- Any PR must pass all automated tests to merge
- Security code requires human review

## Immutable Constraints
- [List technical/security constraints that must never be violated]
```

#### README.md — Project Entry Document

Provides high-level project context for AI and new members; the first document everyone reads:
- Project background and goals
- Tech stack overview
- Environment setup steps (must be one-click runnable)
- Quick start guide
- Core document index

### 4.3 Specify Stage: Defining What to Do

#### spec.md — Single Source of Truth

All implementations must be traceable to specific entries in this document. AI references entry IDs (e.g., "Implement F-001") when generating code to maintain traceability. Any feature "in code but not in spec" is unauthorized scope creep.

**Core Template**:

```markdown
# [Project Name] Requirements Spec

## Project Overview
- Goal: [One-sentence problem statement]
- Core Users: [Target users]
- Success Metrics: [Quantifiable standards]

## Feature List
| ID | Feature | Priority | Status |
| :--- | :--- | :--- | :--- |
| F-001 | User Registration | P0 | Draft |
| F-002 | Email Verification | P0 | Draft |

## Feature Details

### F-001 User Registration
**Description**: [Detailed description]

**Acceptance Criteria**:
- **AC-001-01**:
  - Given: User on reg page, email not registered
  - When: User fills valid email/pass, clicks register
  - Then: Account created, verify email arrives in 60s
- **AC-001-02**:
  - Given: User on reg page, email already registered
  - When: User fills email, clicks register
  - Then: Shows "Email registered" error

## Out of Scope
- [Explicitly list features NOT doing this iteration, preventing AI auto-implementation]
```

#### ui-spec.md — UI Implementation Contract (As needed)

When the project involves frontend interfaces, supplement UI specs: page layouts, interaction flows, design system constraints.

### 4.4 Plan Stage: Planning How to Do It

Document writing order: `spec.md` → `architecture.md` → `data-model.md` + `contracts/` → `plan.md`

#### architecture.md — System Skeleton Blueprint

```markdown
## System Architecture Diagram
[C4 model or module diagram]

## Module Division & Responsibilities
| Module | Responsibility | External Interfaces |
| :--- | :--- | :--- |

## Communication Patterns
- Synchronous calls: [Scenario and protocol]
- Async messaging: [Scenario and message queue]
- Event-driven: [Scenario and event bus]

## Key Constraints
- [Performance, security, availability constraints]
```

#### data-model.md — Authoritative Persistence Model

ER diagrams, table structures and field definitions (including types, constraints, defaults), index strategies. **All DB Schema changes must update this doc first**.

#### contracts/ — Hard Contracts for Inter-Service APIs

OpenAPI / GraphQL Schema, separated by service. **Interface changes must update contract files before modifying implementations**.

#### plan.md — Technical Implementation Path

Detailed tech stack (with versions), module implementation order, third-party integration plans, error handling strategies. Focuses on "how to implement", does not repeat architectural decisions from architecture; API design is handled by `contracts/`, this only describes implementation ideas.

#### decisions.md — Architecture Decision Records (ADR)

Saves the "why do it this way" decision memory bank to avoid repeated discussions and support future traceability. **Append only, no deletion** (can mark "deprecated"); should be recorded at the time of decision:

```markdown
## ADR-001: Choose PostgreSQL over MongoDB
- Date: 2026-05-19
- Status: Accepted
- Background: [Why make this decision]
- Decision: [Final choice and reasons]
- Alternatives: [Rejected options and reasons]
- Impact: [Impact on arch and dev]
```

#### roadmap.md — Delivery Roadmap

Plans product delivery cadence at the milestone level, breaking spec features into iterative stage goals:
- Milestone breakdown (goals and timelines)
- MVP scope definition
- Delivery goals and priority sorting for each iteration
- Dependencies

Milestone granularity shouldn't be too fine; atomic tasks are handled by `tasks.md`.

### 4.5 Tasks Stage: Breaking Down Actions

#### tasks.md — Atomic Action Checklist

Each task contains a clear description, acceptance command, complexity, and dependencies:

```markdown
## Current Iteration Tasks

- [ ] T-001: Implement user reg API (Linked to F-001, AC-001-01~05)
  - Acceptance: `pytest tests/test_auth.py::test_register -v` passes
  - Complexity: M | Deps: None
- [ ] T-002: Implement email verification send (Linked to F-002)
  - Acceptance: run script, receive test email
  - Complexity: S | Deps: T-001
- [ ] T-003: Implement login API (Linked to F-003, AC-003-01~03)
  - Acceptance: `pytest tests/test_auth.py::test_login -v` passes
  - Complexity: M | Deps: T-001

## Task Dependencies
T-001 → T-002 (Serial)
T-001 → T-003 (Serial)
T-002 / T-003 (Parallelizable)
```

#### seed-data/ (As needed) — Test Baseline Data

Provides runnable baseline data for integration & E2E tests. Uses structured formats (JSON/SQL/YAML/CSV), filenames reflect scenario meaning (e.g. `user-normal.json`). Required if integration/E2E tests exist, prepare before writing tasks.

#### checklist.md — Pre-Release Quality Gate

Focuses on cross-task system-level acceptance, complementing single-feature acceptance. Every item must have clear pass/fail criteria:

```markdown
## Pre-Release Checklist
- [ ] All tasks in tasks.md completed and checked
- [ ] All automated tests pass
- [ ] Code Review completed
- [ ] All spec.md acceptance criteria verified
- [ ] No features "in code but not in spec"
- [ ] decisions.md updated with iteration decisions
- [ ] Documentation synced
```

### 4.6 Execute Stage: Execution Tracking & Change Management

#### progress.md — In-Flight Status Dashboard

Current task status, outstanding issues/owners, test result summaries, blocker reasons and ETA. Status enum: Pending / In Progress / Done / Blocked. Update immediately after each task.

#### changelog.md — Historical Archive of Delivered Results

Accumulated delivery records organized by version. Follows [Keep a Changelog](https://keepachangelog.com), append in reverse chronological order, history cannot be altered.

#### proposal.md (Post-MVP) — Change Management

Created when new requirements emerge post-MVP, manages feature evolution, ensures every change is recorded and reviewed:
- Change motivation and background
- Impact scope analysis
- Implementation plan
- Review status (Draft / Approved / Rejected)

After approval, triggers cascade updates: `proposal -> modify spec -> re-plan -> re-tasks`.

---

## V. Execution Loop

> SDD defines "what to do", AE defines "how to do it", the execution loop is where the two meet — the core daily workflow executed by engineers.

### 5.1 Single Task Standard Execution Flow

Every Task follows this standard loop:

```
┌─────────────────────────────────────────────────────┐
│             Single Task Execution Loop              │
│                                                     │
│  1. Read tasks.md, select next task                 │
│     ↓                                               │
│  2. Build Context: Load spec entry + design docs    │
│     ↓                                               │
│  3. Issue structured instructions to AI             │
│     ↓                                               │
│  4. AI generates code                               │
│     ↓                                               │
│  5. Run acceptance command                          │
│     ├─ Pass → 6a. Check tasks.md, update progress   │
│     │         → Return to Step 1                    │
│     └─ Fail → 6b. Analyze reason                    │
│                 ├─ Spec issue → Update spec/plan,   │
│                 │               record in decisions │
│                 └─ Impl issue → Re-instruct AI      │
│                                 (Reflect on context)│
└─────────────────────────────────────────────────────┘
```

**Key Rules**:
- **AI executes only one task at a time**, batch execution prohibited
- When validation fails, **first reflect if your instruction, orchestration, or context was flawed** — AI's output quality reflects the engineer's context management ability
- If AI repeats the same error, trigger Practice 3.6 feedback loop — precipitate error pattern into Rule/Skill

### 5.2 Structured Writing of AI Instructions

Structured instructions are the core practice of Context Engineering — giving AI precise, traceable context instead of vague verbal descriptions:

```
Implement T-001 from tasks.md: User Registration API Endpoint.

Reference:
- Feature Spec: spec.md F-001 (Acceptance criteria AC-001-01 ~ AC-001-05)
- API Definition: contracts/user-api.yaml POST /auth/register
- Data Model: data-model.md users table
- Impl Plan: plan.md 3.1 User Auth Module

Constraints:
- Follow coding standards in AGENTS.md
- Passwords must use bcrypt (constitution.md security constraints)

Provide runnable verification steps when done.
```

**Core elements of an instruction**:
1. **Explicit task**: Reference task ID in tasks.md
2. **Provide context**: Reference spec entries, API contracts, data models
3. **Declare constraints**: Reference constraints in AGENTS.md and constitution.md
4. **Demand verification**: Ask AI for runnable validation methods

### 5.3 Task Granularity and Breakdown Principles

#### Granularity Standard: 30min-2h, adjusted by constraint density

| Complexity | Time Est. | Characteristics | Example |
| :--- | :--- | :--- | :--- |
| **S** (Small) | < 30min | Single file, clear logic | Add a util function, fix formatting |
| **M** (Medium)| 30min - 1h| Multi-file, clear bounds | Implement an API endpoint, add component|
| **L** (Large) | 1h - 2h | Cross-module, needs design| Implement full auth flow, refactor DAO |

**Tasks exceeding 2h MUST be broken down further** — this is a rule, not a suggestion.

#### Task Dependencies

- **Serial tasks**: Upstream must complete and pass validation before starting downstream (e.g. Data Model → API → UI)
- **Parallel tasks**: Independent tasks can be assigned to different Agents simultaneously
- Explicitly mark dependencies in tasks.md to prevent AI from skipping prerequisites

### 5.4 Session Context Management

#### Session Start: Which documents to load

```
Must Load (Every Session):
├── AGENTS.md          → AI behavior constraints
├── constitution.md    → Technical baselines
└── Current task spec  → Task context

Load on Demand (When relevant):
├── architecture.md    → Arch-related tasks
├── data-model.md      → DB-related tasks
├── contracts/         → API-related tasks
└── decisions.md       → When historical decisions are needed
```

#### Session End: What decisions to precipitate

Before ending each session, check if you need to:
- Record important technical decisions into `decisions.md`
- Update task statuses in `progress.md`
- If AI was corrected, evaluate updating Rules/Skills (Practice 3.6)

#### Session Too Long: How to switch and continue

When a session gets too long (empirically over dozens of turns), context rot risk increases significantly. Thresholds vary by model/task complexity. You should:
1. Record current progress to `progress.md`
2. Record key decisions to `decisions.md`
3. Start a new session, reload context documents
4. **Do not continue in ultra-long sessions** — prevents "Lost in the Middle" effects

---

## VI. Change Management & Continuous Improvement

### 6.1 Standard Change Process

When new requirements arrive post-MVP, **directly modifying code is strictly prohibited**. You must follow the standard process:

```
Req Change → Review → Update spec.md → Update plan (if needed) → Re-break tasks → Execute
```

**Why change spec before code** (Axiom 2 · Context Determinism): If you directly change code, AI will read the old version of the spec in future sessions and make decisions based on stale context. As the Single Source of Truth, spec must always reflect current reality.

### 6.2 Grounding the Error Feedback Loop

Standard procedure when AI makes a mistake:

```
AI makes error
  ├─ 1. Reflect first: Were instructions clear? Context sufficient? Constraints missing?
  ├─ 2. Revise instructions, let AI re-execute
  ├─ 3. Evaluate if it's a systemic issue
  │     ├─ No → Continue
  │     └─ Yes → 4. Precipitate as rule
  │           ├─ Coding stds → Update AGENTS.md or Skill
  │           ├─ Arch constraints → Update constitution.md
  │           └─ Domain knowledge → Create new Skill
  └─ 5. Verify if AI behavior improves after update
```

---

## VII. Quick Start

### 7.1 New Project Kickoff Checklist

#### Step 1: Rule Setting (Rules - First thing on Day 1)

- [ ] Create `AGENTS.md`: Coding principles + Prohibited behaviors + Tech stack (5-10 rules)
- [ ] Create `constitution.md`: Quality baselines + Immutable constraints
- [ ] Create `README.md`: Project background, environment setup

#### Step 2: Specify Stage

- [ ] Collaborate with AI to finish `spec.md`:
  - Project overview and success metrics
  - Feature list (ID + Priority)
  - Acceptance criteria for every P0 feature (Given/When/Then)
  - Out of Scope list
- [ ] (If frontend exists) Create `ui-spec.md`

#### Step 3: Plan Stage

- [ ] Create `architecture.md`: Arch diagram + Module division
- [ ] Create `data-model.md`: Core table structures
- [ ] (If API exists) Create `contracts/`: OpenAPI / GraphQL Schema
- [ ] Create `plan.md`: Tech stack + Implementation ideas
- [ ] Create `decisions.md`: Initialize ADRs
- [ ] Create `roadmap.md`: Define milestones and priorities

#### Step 4: Tasks Stage

- [ ] Prepare `seed-data/` (as needed): Create baseline test data
- [ ] Create `tasks.md`: Break down plan/spec into 5-15 atomic tasks
- [ ] Create `checklist.md`: Pre-release quality gates

#### Step 5: Execute Stage

- [ ] Create `progress.md`: Initialize tracking dashboard
- [ ] Create `changelog.md`: Initialize delivery history
- [ ] Follow execution loop (5.1), complete tasks one by one, track progress
- [ ] (Post-MVP) Create `proposal.md`: Manage new requirement changes

### 7.2 MVP Minimal Document Set (Start with 3-4 docs)

For personal projects or small MVPs, **you don't need the full 5-stage document set**. These 4 are enough to start:

| Document | Minimum Content | Why it's necessary |
| :--- | :--- | :--- |
| **AGENTS.md** | 5-10 coding rules | Constrain AI cross-session consistency |
| **spec.md** | Feature list + ACs for core features | Stop AI guessing, provide validation baseline |
| **tasks.md** | Checklist of 5-10 atomic tasks | Control granularity, prevent error accumulation |
| **Tech Plan** | Tech stack + DB structure (Can merge into spec) | Constrain AI tech selection |

**Skippable Documents** (MVP stage):
- `README.md` (can skip for internal temp projects)
- `constitution.md` (merge rules into AGENTS.md)
- `architecture.md` (small projects are simple, can be verbally explained)
- `contracts/` (not needed if no microservices)
- `decisions.md` (few decisions, can backfill later)
- `roadmap.md` (MVP only has one milestone)
- `seed-data/` (can hardcode initially)
- `proposal.md` (MVP doesn't need strict change management)

### 7.3 Best Practices & Anti-Patterns

#### ✅ Should Do

| Practice | Description |
| :--- | :--- |
| **Spec First** | Before coding any feature, it must have a spec entry and ACs |
| **Small Steps** | Let AI implement one task at a time, validate immediately |
| **Structured Prompts**| Reference spec IDs to give AI precise context, not verbal descriptions |
| **Multi-Layer Val.** | Auto tests + Code Review + Arch checks; all three are essential |
| **Record Decisions** | Log important tech decisions in `decisions.md` immediately |
| **Understand Code** | Do not commit/deploy AI code if you don't understand the core logic |
| **Reflect First** | When AI errs, check your instructions/context before blaming AI |
| **Precipitate Errors**| Turn recurring AI errors into Rules/Skills to prevent recurrence |

#### ❌ Should Not Do

| Anti-Pattern | Consequence |
| :--- | :--- |
| **Skip spec to code** | AI guesses logic, almost guaranteeing massive rework |
| **Batch AI tasks** | Errors accumulate, hard to locate issues, hard to validate |
| **Verbal requirements**| Verbal descriptions lost as chat scrolls; only docs persist |
| **Accept "looks okay"**| Must run the acceptance commands explicitly written in tasks.md |
| **Code changes directly**| Must update spec first, then change code |
| **Ignore Out of Scope**| Features not explicitly marked "don't do" might be implemented |
| **Work in ultra-long chats**| Context rot causes late-stage decision quality to plummet |
| **Dump all code to AI**| Signal-to-noise ratio plummets, critical info gets drowned out |

---

## VIII. Paradigm Summary

The essence of Agentic Engineering is the **systematic combination of engineering discipline with AI capabilities** — drastically improving R&D efficiency while maintaining or even elevating quality standards:

| Core Element | Meaning |
| :--- | :--- |
| **Spec is the Product** | Spec is the Single Source of Truth; code is a renewable derivative |
| **Context is Capability** | Providing high-quality, high-signal context is the team's true efficiency lever |
| **Human is Architect** | AI executes; human handles arch decisions, taste, and final quality |
| **Task is the Unit** | Atomic tasks + closed-loop validation are fundamental to stop error accumulation |
| **Doc is Memory** | Docs as Code: team knowledge precipitates persistently, doesn't fade with chat |
| **Knowledge Grows** | Top-down best practices + bottom-up error extraction; continuous evolution |

> **Core Philosophy**: You can outsource execution to AI, but you cannot outsource understanding. SDD ensures "building the right thing", and AE ensures "building it right".
