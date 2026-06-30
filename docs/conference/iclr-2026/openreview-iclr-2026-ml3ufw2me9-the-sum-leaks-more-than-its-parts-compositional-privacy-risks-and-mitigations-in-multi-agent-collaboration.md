---
title: "The Sum Leaks More Than Its Parts: Compositional Privacy Risks and Mitigations in Multi-Agent Collaboration"
title_zh: 总和比部分泄露更多：多智能体协作中的组合隐私风险与缓解
authors: "Vaidehi Patil, Elias Stengel-Eskin, Mohit Bansal"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=mL3uFW2ME9"
tags: ["query:priv-sec"]
score: 9.0
evidence: 研究多智能体LLM系统中的组合隐私泄露并提出缓解措施，推进LLM隐私解决方案。
tldr: 本文首次系统地研究了多智能体LLM系统中的组合隐私泄露问题，即使单次回复无害，跨交互的组合也能恢复敏感信息，并提出了相应的缓解方法。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 多智能体LLM交互中可能存在新型组合隐私泄露，此前未被系统性探索。
method: 构建了辅助知识+智能体交互的隐私风险放大模型，并提出评估与防御方法。
result: 验证了组合泄露的严重性，缓解方法有效降低风险。
conclusion: 多智能体环境需要新的隐私分析框架，该工作填补了空白。
---

## Abstract
As large language models (LLMs) become integral to multi-agent systems, new privacy risks emerge that extend beyond memorization, direct inference, or single-turn evaluations. In particular, seemingly innocuous responses, when composed across interactions, can cumulatively enable adversaries to recover sensitive information, a phenomenon we term compositional privacy leakage. 
We present the first systematic study of such compositional privacy leaks and possible mitigation methods in multi-agent LLM systems. First, we develop a framework that models how auxiliary knowledge and agent interactions jointly amplify privacy risks, even when each response is benign in isolation. Next, to mitigate this, we propose and evaluate two defense strategies: (1) Theory-of-Mind defense (ToM), where defender agents infer a questioner's intent by anticipating how their outputs may be exploited by adversaries,
and (2) Collaborative Consensus Defense (CoDef), where responder agents collaborate with peers who vote based on a shared aggregated state to restrict sensitive information spread.
Crucially, we balance our evaluation across compositions that expose sensitive information and compositions that yield benign inferences.
Our experiments quantify how these defense strategies differ in balancing the privacy-utility trade-off. 
We find that while chain-of-thought alone offers limited protection to leakage (39% sensitive blocking rate), our ToM defense substantially improves sensitive query blocking (up to 97%) but can reduce benign task success. CoDef achieves the best balance, yielding the highest Balanced Outcome (79.8%), highlighting the benefit of combining explicit reasoning with defender collaboration. 
Together, our results expose a new class of risks in collaborative LLM deployments and provide actionable insights for designing safeguards against compositional, context-driven privacy leakage.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当多个大语言模型（LLM）组成多智能体系统时，存在一种传统隐私研究尚未覆盖的新型风险——**组合隐私泄露**（Compositional Privacy Leakage）。即便每个智能体在单次对话中给出的回复看起来都是无害的，当多个交互回合的回复被恶意组合、交叉关联时，攻击者能够逐步还原出原本不可见的敏感信息。
- **研究动机**：现有LLM隐私研究多聚焦于记忆化泄露、直接推断或单轮评估，而多智能体协同场景中，多个“看似无害”的片段可以在上下文和辅助知识的催化下产生毒性更强的隐私推理链，这种现象在此前未被系统性探索和建模。
- **整体含义**：该工作首次将“总和泄露大于部分之和”的观念引入LLM隐私安全，意图为多智能体协作部署提供一套识别、评估和缓解组合式、上下文驱动隐私泄露的分析框架和防御工具。

### 2. 论文提出的方法论

- **核心思想**：将隐私风险建模为“辅助知识 + 多智能体交互”的联合放大过程。攻击者即使只能触达每个智能体孤立看无害的答复，也能利用外部背景知识和对交互序列的关联分析推断出受保护的敏感信息。
- **关键技术细节**：
  - **隐私风险放大模型**：构建一个框架，量化在给定辅助知识的条件下，多轮交互如何逐步提升敏感信息的可恢复性。
  - **防御策略一：心思理论防御（Theory‑of‑Mind, ToM）**：防御智能体主动推断提问者的意图，预测自己的输出可能被对手如何利用，从而在生成回复时提前阻断可能的泄露路径。
  - **防御策略二：协作共识防御（Collaborative Consensus Defense, CoDef）**：多个应答智能体之间互相协作，基于共享的聚合状态进行投票，以此限制敏感信息的扩散范围，使得单一智能体的输出即使被截获也无法单独还原全貌。
- **流程或公式说明**：论文中未提供详细数学公式，但从摘要可知，方法包含对“链路组合”的敏感度评估，以及ToM中的意图推理与CoDef中的投票聚合机制，强调在隐私与效用之间做平衡。

### 3. 实验设计

- **数据集/场景**：
  - 构建了多智能体交互场景，包含两类组合：**会暴露敏感信息的组合**（adversarial compositions）和**只会产生良性推断的组合**（benign compositions）。
  - 具体数据集名称在摘要中未披露，但从“暴露敏感信息 / 良性推断”的平衡评估可推断其构造了隐私-效用对抗基准。
- **Benchmark 与对比方法**：
  - 基准线：**仅使用链式思维（Chain‑of‑Thought）** 作为隐私保护手段（敏感拦截率 39%）。
  - 防御方法对比：ToM 防御、CoDef 防御，并与链式思维基线对比“敏感查询拦截率”和“良性任务成功率”。
  - 评价指标：敏感信息拦截率（sensitive blocking rate）、良性任务成功率，以及综合指标 **平衡结果（Balanced Outcome）**。
- **未公开的细节**：具体的智能体数量、交互轮数、辅助知识来源、敏感信息类型等在摘要中未说明。

### 4. 资源与算力

- 论文提供的摘要及元数据中**未提及任何GPU型号、数量、训练时长或计算资源消耗**。由于研究可能基于LLM的零样本/少样本推理而非大规模训练，算力需求可能相对较低，但无法从现有信息确认。

### 5. 实验数量与充分性

- 摘要中列举了两个主要防御策略与基线对比，并分别给出了单一指标（敏感拦截率从39%到97%）以及综合平衡指标（CoDef达到79.8%），可以推断至少完成了以下实验组：
  - 无防御/链式思维基线
  - ToM 防御
  - CoDef 防御
  - 跨不同组合类型（泄露型 vs. 良性型）的对比
- **充分性与客观性**：从定量结果看，实验覆盖了隐私和效用两个维度，并给出平衡分数以评估真实部署价值，设计相对客观公平。但由于全文未提供，无法判断是否有更多消融实验、不同辅助知识强度、不同LLM基座、不同攻击者能力的全面测试，因此**实验全面性存疑**。

### 6. 论文的主要结论与发现

- **组合隐私泄露确实严重**：多智能体系统中，单次无害回复的累积效应确实能够被攻击者利用，构成新的威胁类别。
- **链式思维有效但不足**：仅用链式思维作为防护，敏感查询拦截率仅39%，说明常规推理过程本身无法阻止组合泄露。
- **ToM防御强力但有代价**：心思理论防御可将敏感拦截率大幅提升至97%，但同时会降低良性任务的成功率，隐私-效用权衡存在明显偏斜。
- **CoDef实现最佳平衡**：协作共识防御在隐私和效用之间取得最均衡的结果，综合平衡得分最高（79.8%），说明结合显式推理与防御者之间的协作是应对组合泄露的有效路径。
- **实践启示**：多智能体LLM部署需要专门针对组合式、上下文驱动的隐私泄露设计安全防护，单点检查不够。

### 7. 优点

- **新颖性**：首次定义并系统研究多智能体LLM中的组合隐私泄露问题，填补了空白。
- **框架完整**：从风险建模、攻击面分析到防御方案设计和评估，形成闭环。
- **防御方案有层次**：提出两种机制截然不同的防御（个体意图推理 vs. 群体共识），并论证了协作的增益。
- **平衡评估**：不只看隐私拦截率，还关注对良性任务的影响，给出综合指标，避免片面追求安全性而牺牲可用性。

### 8. 不足与局限

- **实验细节缺失**：数据集、智能体数量、交互协议、敏感信息类别等关键实现细节在现有材料中不可见，复现性和说服力受影响。
- **攻击模型假定**：依赖辅助知识和组合推断能力的具体攻击者模型未详细阐述，威胁模型的现实性和强度无法判断。
- **扩展性未验证**：未提及多智能体规模扩大或更复杂任务流下的表现，实际多步协作场景可能更复杂。
- **基座模型泛化性**：仅在特定LLM上测试的可能性较大，未体现跨模型、跨架构的泛化验证。
- **用户研究缺失**：缺乏真实用户或红队评估，无法得知组合泄露在实际人机交互中的可感知性和利用难度。

（完）
