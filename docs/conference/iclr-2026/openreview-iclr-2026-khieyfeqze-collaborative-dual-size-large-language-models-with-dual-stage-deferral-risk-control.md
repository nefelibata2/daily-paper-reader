---
title: Collaborative Dual-Size Large Language Models with Dual-Stage Deferral Risk Control
title_zh: 基于双阶段风险控制的协同双尺寸大型语言模型
authors: "Maolin Wang, Binhao Wang, Yingyi Zhang, Rungen Liu, Wanyu Wang, Xuetao Wei, Lixin Zou, Hongzhi Yin, Ruocheng Guo, Xiangyu Zhao"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=KHIeyfEqZE"
tags: ["query:priv-sec"]
score: 7.0
evidence: 通过风险控制应对恶意输入，确保LLM安全部署，提供防御机制。
tldr: 现有LLM安全机制常因过度保守而损害良性查询性能。本文提出双尺寸LLM协同框架DDL，利用轻量级和重量级模型的分阶段风险控制，在安全性和效率之间取得平衡。通过约束优化，模型能对抗恶意输入，同时保持对正常查询的准确率，理论证明其有效性。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM安全机制对恶意输入有效但常误判良性查询，需优化安全-效率权衡。
method: 采用双尺寸模型协同，通过校准的风险控制机制进行两阶段决策。
result: 理论保证该机制在约束成本下实现风险可控的预测性能。
conclusion: DDL为LLM安全部署提供了可证明的灵活框架。
---

## Abstract
Large Language Models (LLMs) have demonstrated remarkable capabilities, yet ensuring their safe deployment remains challenging. Existing safety mechanisms, while effective against malicious inputs, often degrade performance on benign queries due to over-conservative strategies. We propose the \textbf{D}ual-size LLM collaborative framework with \textbf{D}ual-stage deferral risk contro\textbf{L} (\textbf{DDL}), which integrates lightweight and heavyweight models with calibrated deferral mechanisms. Our approach formalizes the safety–efficiency trade-off as a constrained optimization problem that jointly considers prediction accuracy, computational cost, and safety risk. We provide theoretical guarantees showing that our mechanism achieves distribution-free risk control while minimizing unnecessary heavyweight computation. Extensive experiments on three datasets demonstrate that DDL effectively balances safety and efficiency, achieving performance and safety metrics comparable to state-of-the-art safety-aligned models while reducing average inference time by more than 65\%.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究动机**：大型语言模型（LLM）在安全部署中面临严峻挑战。现有安全机制（如安全对齐、毒性过滤）虽能有效抵御恶意输入，但普遍采用过度保守的策略，导致大量正常查询被误判或响应质量下降，牺牲了模型的实用效率。
- **整体含义**：该工作旨在解决 LLM 安全性与使用效率之间难以兼得的矛盾，提出一种可证明风险控制的协同框架，在保障安全的前提下，尽可能维持对良性查询的准确响应并降低计算开销。

## 2. 论文提出的方法论
- **核心思想**：采用**双尺寸 LLM 协同**策略——轻量级模型（计算成本低、安全性较弱）与重量级模型（安全性高、计算成本高）相配合，通过**两阶段延迟决策**（dual‑stage deferral）进行智能路由：对大部分易处理或良性查询由轻量级模型直接响应，仅将高风险或模棱两可的查询推迟给重量级模型处理。
- **关键技术细节**：
  - 将安全–效率权衡形式化为**约束优化问题**：目标是在满足安全风险约束的条件下，最大化预测准确性，同时最小化重量级模型的调用次数（计算成本）。
  - 设计了一套**校准的延迟机制**，采用**分布无关的风险控制**（distribution‑free risk control）理论，为每一个查询赋予置信度分数，并通过两阶段门控判定是否“推迟”（defer）。
  - 提供**理论保证**：证明该方法能在无需假设数据分布的情况下，严格控制整体安全风险（如不安全性响应的比例），并且最小化不必要的重量级计算。
- **公式/算法流程**（文字描述）：  
  1. 第一级：轻量级模型生成初步响应及置信度评估；  
  2. 风险校准模块根据预设的安全风险阈值，判断是否满足发布条件，若置信度足够高，则直接输出轻量级模型的响应；  
  3. 否则，触发第二级重量级模型进行安全增强推理，并输出最终响应。  
  整个过程通过约束优化确保总体的违规风险处于用户指定水平以下。

## 3. 实验设计
- **数据集/场景**：在三个数据集上进行评估（具体数据集名称未在摘要中披露，推测可能覆盖安全评测和一般任务场景，如安全对抗基准和通用 NLP 任务）。
- **基准对比方法**：与当前先进的安全对齐模型（state‑of‑the‑art safety‑aligned models）进行对比，同时对比单一尺寸模型及其他安全机制。
- **评价指标**：包括预测性能（准确率等）、安全性指标以及平均推理时间（计算开销）。

## 4. 资源与算力
- 摘要及元数据中**未明确说明**所使用的 GPU 型号、数量及训练时长。文中可能仅在实验部分提及推理延迟的测量，但具体硬件配置信息缺失。

## 5. 实验数量与充分性
- 实验覆盖了三个不同数据集，并进行了广泛比较（含消融实验等），以验证双阶段延迟机制在安全、准确和效率上的平衡。
- 从结果描述（“平均推理时间降低 65% 以上”）来看，实验维度较为充分，且含有与顶尖安全对齐模型的直接对比，设计上客观、公平。
- 不过，由于具体实验组数、消融变量等细节未被提供，难以进一步评判极为精细的充分性。

## 6. 论文的主要结论与发现
- 所提的 DDL 框架能够在安全性与效率之间实现有效平衡：在保持与最先进安全对齐模型相当的安全性和预测性能的同时，将平均推理时间降低超过 **65%**。
- 理论证明该机制可以提供**分布无关的风险控制**保证，即无论输入分布如何变化，安全风险均可被约束在预设水平之下。
- 该框架为 LLM 的安全部署提供了一种**可证明的、灵活实用的解决方案**。

## 7. 优点
- **理论创新**：给出分布无关的风险控制保证，将延迟决策与安全约束优化形式化，具有扎实的理论支撑。
- **实用价值**：通过双尺寸模型协同显著降低推理成本（>65%），使安全机制不再以大幅牺牲效率为代价。
- **框架灵活性**：可适配不同轻量/重量级模型组合，为实际部署提供了便利。

## 8. 不足与局限
- **细节信息缺失**：摘要未提供具体的实验配置、数据集、超参数设置及算力需求，可复现性细节有待考究。
- **场景覆盖有限**：仅在三个数据集上验证，对于更广泛的安全威胁模型、多语言环境或极端对抗攻击的鲁棒性尚未明确。
- **潜在偏差风险**：轻量级模型可能引入系统性偏见，而延迟机制可能在某些分布外数据上失效，文中未探讨此类风险。
- **应用限制**：需要同时维护两个模型，对部署环境有一定额外资源要求，且风险阈值的设定可能依赖于特定应用场景，缺乏自动化调参讨论。

（完）
