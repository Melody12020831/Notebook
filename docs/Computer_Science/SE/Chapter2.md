---
statistics: True
comments: true
---

# Chapter 2 | Software Engineering

## Defining the Discipline

**The IEEE Definition – Software Engineering**

1. The application of a **systematic, disciplined, quantifiable** approach to the **development, operation,** and **maintenance** of software; that is, the application of engineering to software.
2. The study of approaches as in (1).

**IEEE定义**强调，软件工程不仅仅是编写代码，而是要用系统化、规范化、可量化的方法来开发、运行和维护软件。这意味着软件开发要像传统工程一样，有明确的流程、标准和度量，确保软件的质量和可维护性。

**First Definition**

1. Software engineering is the establishment and use of sound engineering principles in order to obtain economically software that is reliable and works efficiently on real machines.

**第一条定义**进一步指出，软件工程的目标是通过合理的工程原则，经济高效地获得可靠且能在真实环境下高效运行的软件。也就是说，软件不仅要好用，还要成本可控、运行高效。

---

### A layered technology

软件工程是一种分层技术，主要包括以下几个层次：

1. **质量焦点（a "quality" focus）**：最底层，强调整个软件工程活动都要以质量为核心，贯穿始终。
2. **过程模型（process model）**：为软件开发提供路线图，帮助团队按时、高质量地完成目标。
3. **方法（methods）**：提供具体的技术方法和“怎么做”的指导，涵盖需求分析、设计、编码、测试等各个环节。
4. **工具（tools）**：最上层，指各种计算机辅助软件工程（CASE）工具，用于支持和自动化方法和过程的实施。

---

## The Software Process

### 基本定义

软件过程（process）是指为创建某个工作产品而执行的一系列活动（activities）、动作（actions）和任务（tasks）的集合。

- **活动（Activity）**：实现广泛目标的过程，如与利益相关者沟通，适用于各种项目规模和复杂度。
- **动作（Action）**：如架构设计，完成一组任务，产生主要工作成果。
- **任务（Task）**：关注于小而明确的目标，如单元测试，产生具体可交付成果。

---

### 过程框架

过程框架为完整的软件工程过程奠定基础，定义了适用于所有软件项目的一小组通用活动（framework activities）。

---

#### 通用过程框架

1. **Communication**：与客户协作、需求收集。
2. **Planning**：制定工程计划，描述技术风险、资源需求、工作产品和进度。
3. **Modeling**：建立模型，帮助开发者和客户理解需求和设计。
4. **Construction**：代码生成与测试。
5. **Deployment**：交付软件，客户评估与反馈。

---

### Umbrella Activities

伞形活动是对过程框架活动的补充，贯穿整个软件开发周期，包括：

1. 项目跟踪与控制（Software project tracking and control）
2. 风险管理（Risk management）
3. 软件质量保证（Software quality assurance）
4. 技术评审（Technical reviews）
5. 度量（Measurement）
6. 配置管理（Software configuration management）
7. 可复用性管理（Reusability management）
8. 工作产品准备与生产（Work product preparation and production）

---

### 过程适应性

过程适应性指根据项目特点调整活动、动作和任务的流程、细节和角色分工等，以适应不同项目需求。

---

## Software Engineering Practice

### The Essence of Practice

1. **Understand the problem**（理解问题）：通过沟通和分析，明确用户需求和问题本质。
2. **Plan a solution**（规划方案）：进行建模和软件设计，制定解决问题的具体方法。
3. **Carry out the plan**（执行方案）：进行代码实现，将设计转化为可运行的软件。
4. **Examine the result for accuracy**（检查结果）：通过测试和质量保证，验证软件的正确性和可靠性。

---

### General Principles

1. The reason it all exists — Provide **Value** to users（用户思维）
2. **KISS** — Keep It Simple, Stupid!（大道至简）
3. Maintain the **Vision**（不忘初心）
4. What you produce, others will consume（换位思考）
5. Be open to the future（面向未来）
6. Plan ahead for reuse（谋划复用）
7. Think!（凡事多思）

---

## 2.4 Software Development Myths

### Management Myths

**Myth:** 有标准和流程手册，大家就都知道怎么做了。
	
- **Reality:** 并非每个人都真正关心或遵循这些标准。

**Myth:** 进度落后时多加人手就能赶上。
	
- **Reality:** 软件开发不是机械化生产，盲目加人反而会拖慢进度（Brooks定律）。

**Myth:** 外包项目后管理者可以高枕无忧。
	
- **Reality:** 如果自身管理能力不足，外包也会遇到同样甚至更多的问题。

---

### Customer Myths

**Myth:** 只要有大致目标就能开始编程，细节可以后补。

- **Reality:** 需求不明确会导致项目延期和返工。

**Myth:** 需求不断变化没关系，软件灵活可以随时改。

- **Reality:** 变更越晚，代价越高。需求定义阶段变更成本最低，发布后最高。

---

### Practitioner’s Myths

**Myth:** 程序能跑就算完成。

- **Reality:** 60-80%的工作量发生在首次交付后，后续维护和修改同样重要。

**Myth:** 没跑起来就无法评估质量。

- **Reality:** 正式技术评审等活动可以提前发现问题。

**Myth:** 只有程序本身才是交付物。

- **Reality:** 文档、配置等同样重要，为后续开发和维护提供支持。

**Myth:** 软件工程只会带来繁琐文档，拖慢进度。

- **Reality:** 软件工程的核心是提升质量，减少返工，反而能加快交付。

---