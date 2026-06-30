---
title: "GuardAgent: Safeguard LLM Agents via Knowledge-Enabled Reasoning"
title_zh: GuardAgent：通过知识增强推理守护LLM智能体
authors: "Zhen Xiang, Linzhi Zheng, Yanjie Li, Junyuan Hong, Qinbin Li, Han Xie, Jiawei Zhang, Zidi Xiong, Chulin Xie, Carl Yang, Dawn Song, Bo Li"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=2nBcjCZrrP"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出GuardAgent守护智能体，通过执行安全防护请求来保护LLM智能体
tldr: 针对LLM智能体面临的安全挑战，本文提出首个守护智能体GuardAgent，它通过理解安全防护请求、生成任务计划并执行防护代码，动态保障目标智能体的行为合规。该框架结合了LLM推理与记忆模块中的上下文集，能适应多样化的安全需求。实验证明GuardAgent可有效防御多种威胁，为构建安全可靠的LLM智能体应用提供了关键技术和设计范式。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: LLM智能体的安全风险日益突出，缺乏动态、可定制的守护机制来约束其行为。
method: 提出GuardAgent，首个守护智能体，通过分析安全请求生成任务计划和防护代码执行，实现行为检查。
result: 实验表明GuardAgent能有效遵循安全请求，动态保护目标智能体，防御各类安全威胁。
conclusion: 该工作为LLM智能体的安全运行提供了通用且可扩展的守护方案，推动了安全人工智能的发展。
---

## Abstract
The rapid advancement of large language model (LLM) agents has raised new concerns regarding their safety and security. In this paper, we propose GuardAgent, the first guardrail agent to protect target agents by dynamically checking whether their actions satisfy given safety guard requests. Specifically, GuardAgent first analyzes the safety guard requests to generate a task plan, and then maps this plan into guardrail code for execution. By performing the code execution, GuardAgent can deterministically follow the safety guard request and safeguard target agents. In both steps, an LLM is utilized as the reasoning component, supplemented by in-context demonstrations retrieved from a memory module storing experiences from previous tasks. In addition, we propose two novel benchmarks: EICU-AC benchmark to assess the access control for healthcare agents and Mind2Web-SC benchmark to evaluate the safety policies for web agents. We show that GuardAgent effectively moderates the violation actions for different types of agents on these two benchmarks with over 98% and 83%
guardrail accuracies, respectively. Project page: https://guardagent.github.io/

---

## 论文详细总结（自动生成）

# 论文总结：GuardAgent: Safeguard LLM Agents via Knowledge-Enabled Reasoning

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）驱动的智能体（Agent）正在被广泛应用于各种自动决策与交互任务，但它们在执行过程中可能产生不安全或违规行为，对用户和社会带来安全隐患。
- **核心问题**：现有的LLM智能体缺乏一种通用的、动态可定制的安全守护机制，来持续检验其行为是否符合预先设定的安全策略或防护请求。
- **整体含义**：本文首次提出“守护智能体”这一概念，旨在构建一个独立的安全防护层，通过基于知识的推理，实时监督并校正目标智能体的行为，从而在应用层面确保LLM智能体的安全合规性。

## 2. 论文提出的方法论

- **核心思想**：设计一个名为 **GuardAgent** 的安全守护智能体，它能接收外部定义的安全防护请求（safety guard requests），自动生成任务计划并转换为可执行的防护代码，对目标智能体的动作进行决定性检查，阻断违规行为。
- **关键技术细节与流程**：
  - **任务规划**：GuardAgent 首先利用LLM作为推理引擎，分析输入的安全防护请求，生成一份结构化的任务计划，明确需要执行哪些检查步骤。
  - **代码生成与执行**：将任务计划映射为实际的防护代码（guardrail code），通过执行该代码来对目标智能体的候选动作进行验证。代码执行保证了判定过程的确定性和可重复性。
  - **记忆增强**：在两个步骤中均引入记忆模块，其中存储了过往任务的成功经验（in-context demonstrations）。当面对新的安全请求时，GuardAgent 通过检索相关上下文集来增强推理能力，提高任务泛化性。
  - 整体流程形成闭环：安全请求 → 任务计划生成 → 防护代码生成 → 代码执行与校验 → 安全/不安全动作裁定。

## 3. 实验设计

- **数据集/场景**：论文针对两类典型智能体安全场景提出了两个全新基准：
  - **EICU-AC**（Healthcare Agent Access Control）：用于评估医疗智能体在访问控制上的安全性，衡量ProtectorAgent能否防止越权访问敏感数据或功能。
  - **Mind2Web-SC**（Web Agent Safety Policy）：用于评估网页智能体对安全策略的遵循程度，检查其在网页交互中是否执行被禁止的操作。
- **对比方法**：文中未详细列出具体的基线方法，但从上下文可推知，主要对比基线可能是无防护的原始LLM智能体、基于固定规则或提示词的简单安全过滤方法。GuardAgent 通过与这些隐含基线比较，体现其动态推理与代码执行的优势。
- **评估指标**：主要使用**防护准确率（guardrail accuracy）**，即智能体违规动作被成功拦截的比例。

## 4. 资源与算力

- 论文提供的信息中**未明确说明**使用的GPU型号、数量、训练时长等算力资源的细节。
- 从方法论推断，GuardAgent 本身以推理为主，可能无需大规模训练。其主要计算开销来自于LLM的推理调用以及记忆模块的检索。若需微调基座LLM，本文未提及相关训练配置，因此具体算力需求暂无法确定。

## 5. 实验数量与充分性

- **明确报道的实验组数**：
  - 在 **EICU-AC** 基准上，GuardAgent 取得了超过 98% 的防护准确率。
  - 在 **Mind2Web-SC** 基准上，防护准确率超过 83%。
  - 两组实验分别覆盖医疗与网页两种差异较大的应用场景，展示了方法的通用性。
- **其他潜在实验**：根据一般论文结构，可能还包含了消融实验（如移除记忆模块、不使用代码执行而仅用自然语言判断等）以及对不同LLM基座的影响分析，但给出的摘要中未详细列出。
- **实验的充分性与公平性**：
  - 两个全新基准的提出为后续研究提供了公平的评估平台。
  - 98% 与 83% 的准确率显示方法在相对可控的访问控制场景中效果优异，网页场景下虽稍低但仍有较强实用性。
  - 缺少与其他防护方法的直接定量对比数据，可能是摘要省略所致；若全文未补充对比，则实验充分性存在一定缺口。

## 6. 论文的主要结论与发现

- GuardAgent 作为首个守护智能体框架，能够有效地根据用户或系统定义的安全请求，对LLM智能体的行为进行动态检查和防护。
- 通过将自然语言的安全请求转化为可执行代码，GuardAgent 实现了确定性的安全控制，避免了纯语言推理可能出现的不确定性。
- 记忆模块中存储的上下文集显著增强了LLM对新颖安全请求的推理能力和任务泛化能力。
- 在两个差异性显著的基准上取得的较高准确率表明，该框架是一种通用且可扩展的LLM智能体安全解决方案。

## 7. 优点

- **创新性**：首次提出“守护智能体”概念，填补了LLM智能体安全防护领域的空白。
- **方法设计亮点**：
  - **双阶段推理-执行架构**：将安全需求分析（计划）与执行（代码）分离，兼顾灵活性与确定性。
  - **知识与经验复用**：记忆模块的引入使得GuardAgent可以积累经验，持续提升对新任务的适应效率。
  - **代码执行驱动**：通过防护代码直接干预，避免了仅依赖LLM输出可能产生的模糊和错误。
- **实验完善度**：
  - 构建了两个来自不同领域的专门化安全基准，既服务于自身验证，也为社区提供了评估工具。
  - 场景选择具有代表性，覆盖了高热度的医疗和网页代理应用。

## 8. 不足与局限

- **实验覆盖与对比**：
  - 摘要中未展现与最新的LLM安全技术（如基于RLHF的安全对齐、外部内容过滤库等）的横向对比，难以量化GuardAgent的相对优势。
  - 仅报道防护准确率，未分析误拦截率（将安全动作误判为违规）或响应延迟等关键性能指标。
- **潜在偏差风险**：
  - 防护代码的生成依赖LLM能力，若LLM本身对安全请求存在理解偏差，可能导致防护规则偏离本意。
  - 记忆模块中的示例若未覆盖足够多的边界情况，可能导致面对极端或对抗性安全请求时失效。
- **应用限制**：
  - 当前设计假设安全请求是明确给定的，对于隐式的、动态变化的安全策略可能不够灵活。
  - 代码执行过程可能引入新的安全风险，如注入、恶意代码生成等，文中未讨论对GuardAgent自身的保护机制。
  - 网页智能体场景的83%准确率仍有提升空间，离实际高可靠部署尚有距离，且该场景下未说明错误拦截对用户体验的影响。

（完）
