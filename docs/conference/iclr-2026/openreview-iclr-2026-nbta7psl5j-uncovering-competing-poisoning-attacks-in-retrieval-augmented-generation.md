---
title: Uncovering Competing Poisoning Attacks in Retrieval-Augmented Generation
title_zh: 揭示检索增强生成中的竞争性投毒攻击研究
authors: "Liuji Chen, Xiaofang Yang, Yuanzhuo Lu, Jinghao Zhang, Xin Sun, Qiang Liu, Shu Wu, Jing Dong, Liang Wang"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=nBta7psl5J"
tags: ["query:priv-sec"]
score: 9.0
evidence: RAG系统中的竞争性投毒攻击
tldr: 本文针对检索增强生成（RAG）系统中的投毒攻击问题，引入多个攻击者竞争的新场景，形式化了威胁模型并提出竞争有效性指标。研究揭示了在多方对抗下攻击效力的变化，为实际部署中的RAG安全评估提供了更真实的视角。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有RAG投毒攻击研究主要假设单一攻击者，忽略了真实场景中多个攻击者竞争的现实。
method: 形式化竞争性攻击威胁模型，提出竞争有效性指标量化攻击者优势。
result: 实验揭示了竞争环境下攻击效果的变化规律。
conclusion: 为RAG系统在多对抗环境下的安全评估提供了新的分析框架。
---

## Abstract
Retrieval-Augmented Generation (RAG) systems improve the factual grounding of large language models (LLMs) but remain vulnerable to retrieval poisoning, where adversaries seed the corpus with manipulated content. Prior work largely evaluates this threat under a simplified single-attacker assumption. In practice, however, high-value or high-visibility queries attract multiple adversaries with conflicting objectives. Motivated by real cases, we introduce the setting of competing attacks, in which multiple attackers simultaneously attempt to steer the same (or closely related) query toward different targets. We formalize this threat model and propose competitive effectiveness, a metric that quantifies an attacker’s advantage under competition. Extensive experiments show that many strategies that succeed in the single-attacker regime degrade markedly under competition, revealing performance inversions and highlighting the limits of conventional metrics such as attack success rate and F1. Further more, we present PoisonArena, a standardized framework and benchmark for evaluating poisoning attacks and defenses under realistic, multi-adversary conditions. Our code is included in the supplementary materials.

---

## 论文详细总结（自动生成）

根据您提供的论文摘要和元数据，以下是对该研究工作的详细分析总结。

### 1. 论文的核心问题与整体含义
*   **研究动机**：当前的检索增强生成系统虽能提升大模型的事实准确性，但极易受到**检索投毒攻击**的威胁。现有的安全研究普遍基于一个过于简化的假设：**即系统中只存在单一的恶意攻击者**。
*   **核心问题**：在真实的互联网生态（如搜索引擎、百科知识库、社区问答）中，高价值查询往往会同时吸引**多个目标冲突、利益对抗的攻击者**。现有研究未能解释这种“多方竞争”环境下的攻击效能与行为变化。
*   **整体含义**：该文旨在揭示当多个攻击者“同台竞技”时，传统的投毒策略是否依然有效，以及攻击者之间的相互掣肘会如何重塑 RAG 系统的安全态势，为更真实的系统安全评估奠定基础。

### 2. 论文提出的方法论
*   **威胁模型形式化**：首次定义了**竞争性投毒攻击**场景，模型中多个攻击者针对相同或高度相关的查询，同时向检索语料库注入操纵性内容，以实现各自不同的攻击目标。
*   **核心评价指标**：提出 **“竞争有效性”** 指标。该指标旨在量化在存在其他攻击者干扰的对抗环境下，某特定攻击者相对于他人的攻击优势，弥补了传统指标（如攻击成功率、F1分数）在多方对抗场景下的评估盲区。
*   **标准化测试平台**：构建了名为 **PoisonArena** 的标准化框架与基准，用于在多对手条件下系统性地评估投毒攻击与防御策略。

### 3. 实验设计
*   **数据集/场景**：虽未在摘要中详述具体数据集名称，但根据“高可见度查询”、“多方攻击者”的描述，推测涵盖了开放域问答或事实验证等典型的 RAG 任务场景。
*   **Benchmark**：论文的核心贡献之一便是建立了 **PoisonArena** 基准，该基准模拟了具有现实意义的竞争性多攻击者环境。
*   **对比方法**：实验对比了当前主流的投毒攻击策略，并将它们在单攻击者场景下的表现与竞争性场景下的表现进行横评。

### 4. 资源与算力
*   **算力说明**：**文本未提及**。由于提供的材料仅限于摘要，未包含详细的 GPU 型号、卡数、训练时长或推理资源消耗等信息。

### 5. 实验数量与充分性
*   **实验规模**：摘要中提及进行了 **“大量实验”**。结合论文性质，实验应涵盖了不同的攻击目标组合、攻击策略组合以及防御方案的交叉测试。
*   **充分性与客观性**：研究试图揭露传统评估指标的局限性，并引入竞争有效性指标，逻辑上具备客观性。但由于缺乏正文细节，无法断定实验在规模上是否绝对充分。

### 6. 论文的主要结论与发现
*   **攻击效力的逆转**：很多在单攻击者场景下百试百灵的攻击策略，在竞争环境中效力会**显著退化**，即攻击效果被其他攻击者的存在严重削弱。
*   **传统指标的失效**：研究揭示了**攻击成功率**和 **F1** 等常规指标在多方对抗场景下的局限性，它们无法准确反映攻击者在竞争中的真实优劣势。
*   **分析框架的构建**：通过 PoisonArena 基准，提供了评估 RAG 系统在现实复杂对抗环境下的脆弱性的新范式。

### 7. 优点
*   **场景创新**：打破了学界普遍忽略多攻击者共存的现状，首个系统性地研究 RAG 投毒中的“竞争”维度，具有重要的现实指导意义。
*   **指标创新**：提出的“竞争有效性”指标，为解决多方对抗难评估的问题提供了新工具。
*   **平台贡献**：PoisonArena 标准化框架的开源（代码见补充材料），为社区后续在此复杂设定下的研究提供了公平的测试基础。

### 8. 不足与局限
*   **摘要信息缺失**：基于现有材料，无法得知实验是否覆盖足够多样化的数据模态、大模型架构以及检索算法。
*   **防御评估不明确**：摘要未详细阐述如何将防御方纳入竞争模型，以及不同防御在竞争下的表现对比。
*   **攻击策略泛化性**：结论可能依赖于所测试的特定攻击策略组合，对于未来出现的新型攻击，其竞争退化规律是否仍适用有待验证。
*   **应用限制**：PoisonArena 基准的真实性程度是否完美还原复杂的互联网博弈（如攻击成本、动态攻防）可能存在局限。

（完）
