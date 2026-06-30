---
title: Deep Learning with Plausible Deniability
title_zh: 具有可否认性的深度学习
authors: "Wenxuan Bao, Shan Jin, Hadi Abdullah, Anderson C. A. Nascimento, Vincent Bindschaedler, Yiwei Cai"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=tVpneDH5ov"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出PD-SGD，一种基于拒绝采样的可否认性训练算法，抵御隐私攻击
tldr: 深度学习模型容易记忆训练样本，导致隐私泄露风险。本文提出PD-SGD算法，引入可否认性概念：通过拒绝采样技术，当小批量样本无法被否认时禁止参数更新，从而防止模型记忆特定数据。理论证明了其隐私保障，实验显示该方法在保持高准确率的同时有效抵御成员推断攻击，为生成模型等隐私敏感任务提供了实用且理论可靠的防御手段。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有隐私防御如差分隐私常牺牲模型性能，无理论保证的经验防御不足。
method: 提出PD-SGD，利用拒绝采样技术在训练中阻止不可否认小批量更新。
result: PD-SGD在理论和实验上均能提供可否认性，同时保持较好的模型效用。
conclusion: 为隐私保护提供了一种新的可否认性策略，平衡了性能与安全性。
---

## Abstract
Deep learning models are vulnerable to privacy attacks due to their tendency to memorize individual training examples. Theoretically-sound defenses such as differential privacy can defend against this threat, but model performance often suffers. Empirical defenses may thwart existing attacks while maintaining model performance but do not offer any robust theoretical guarantees.

In this paper, we explore a new strategy based on the concept of plausible deniability. We introduce a training algorithm called **P**lausibly **D**eniable **S**tochastic **G**radient **D**escent (PD-SGD). 
The core of this approach is a rejection sampling technique, which probabilistically prevents updating model parameters whenever a mini-batch cannot be plausibly denied. We provide theoretical results showing that PD-SGD effectively mitigates privacy leakage from individual data points. Experiments demonstrate the scalability of PD-SGD and the favorable privacy-utility trade-off it offers compared to existing defense methods.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：深度学习模型容易记忆个体训练样本，导致成员推断等隐私攻击可以从中提取敏感信息。
- **现有防御的问题**：
  - 理论可靠的防御（如差分隐私）常严重降低模型性能。
  - 仅凭经验的防御虽能保持较好模型效用，但缺乏严格的理论保证，可能被新攻击突破。
- **本文动机**：探索一种新的隐私保护策略——**可否认性（plausible deniability）**，在维持模型性能的同时提供可量化的隐私保障。
- **整体含义**：论文提出把“模型更新是否可以被否认”作为训练约束，对不可否认的小批次进行概率性拒绝，从而阻止模型“记住”个体数据。这种方法为隐私敏感任务（如生成模型）提供了一种实用且理论可证的防御范式。

## 2. 方法论

- **核心思想**：利用拒绝采样（rejection sampling）在训练过程中实施可否认性控制。
- **关键技术细节**：
  - 训练时对每个小批次（mini-batch）进行可否认性检验：若该批次的数据“不可被否认”（即模型参数更新会明显暴露该批样本的存在），则以一定概率拒绝本次参数更新。
  - 拒绝采样的决策依据基于可否认性条件，如小批次对参数的梯度是否显著偏离某一可否认范围。
  - 算法名称：**PD-SGD**（Plausibly Deniable Stochastic Gradient Descent），在标准 SGD 的更新步骤中插入概率拒绝机制。
- **理论结果**：论文提供了理论证明，表明 PD-SGD 能有效抑制来自个体数据点的隐私泄露，为方法的隐私保障奠定了形式化基础。

## 3. 实验设计

- **数据集/场景**：摘要和元数据中未明确列出使用的具体数据集名称，但提到“实验展示了 PD-SGD 的可扩展性及与现有防御方法相比更优的隐私-效用折衷”。
- **对比方法**：与已有的防御手段（很可能包括差分隐私训练、经验性防御等）进行了比较。
- **评估指标**：聚焦于隐私与效用的权衡（trade-off），推断隐私强度一般通过成员推断攻击等来衡量，而效用由模型准确率等任务指标体现。
- **场景**：方法被强调适用于生成模型等隐私敏感任务，暗示实验中可能包含生成建模场景。

## 4. 资源与算力

- 论文提供的摘要与元数据中**未明确给出任何算力信息**，例如 GPU 型号、数量、训练时长等。
- 无法从现有信息评估计算开销是否大规模。

## 5. 实验数量与充分性

- 根据文本描述，论文至少进行了**与多种现有防御方法的横向对比**，并验证了 PD-SGD 在不同设置下的可扩展性。
- 但对实验的具体组数、消融研究、不同数据集的数量等细节，摘要和元数据**未提供完整说明**，因此无法准确判断实验是否足够丰富、覆盖是否全面，也无法深入评估实验是否充分、客观、公平。
- 从“favorable privacy-utility trade-off”的结论看，实验设计应包含了关键维度的比较，但细节有限。

## 6. 主要结论与发现

- PD-SGD 在理论和实验层面均能提供有效的可否认性隐私保护。
- 与现有防御相比，PD-SGD 在保持较好模型效用（如准确率）的同时，能显著降低隐私泄露风险，实现了更优的隐私-效用平衡。
- 该方法在生成模型等任务中表现出实用性，为深度学习隐私防御引入了新的可否认性策略。

## 7. 优点

- **理论保证**：提供了可否认性的形式化理论结果，弥补了经验防御缺乏保障的缺陷。
- **新的隐私范式**：创新性地将拒绝采样引入训练过程，从“更新是否可否认”的角度解决记忆问题，思路新颖。
- **实用性强**：在维持模型性能方面优于传统理论防御（如差分隐私），更适合性能敏感的场景。
- **可扩展性**：实验显示方法可扩展至实际规模的训练。

## 8. 不足与局限

- **实验细节缺失**：从提供的摘要和元数据中，无法获知具体的基准数据集、攻击模型、超参数等，难以完全评估实验的严谨性和泛化能力。
- **隐私强度对比不明确**：可否认性与差分隐私的形式化关系、在最坏情况下的隐私保护强度尚未在摘要中阐明，可能在某些攻击模型下保护力度弱于差分隐私。
- **应用限制未知**：拒绝采样对训练效率的影响、对特定任务（如分类与回归）的适用条件、对小批量大小的敏感性等均未从摘要中体现，需要查看全文才能判断。
- **可能存在偏差风险**：由于实验设置细节缺失，无法确认对比是否公平（例如是否在同一效用水平下比较隐私强度），亦无法排除超参数调参等带来的潜在偏差。

（完）
