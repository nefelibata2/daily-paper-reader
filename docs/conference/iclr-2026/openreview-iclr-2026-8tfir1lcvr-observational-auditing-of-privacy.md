---
title: Observational Auditing of Privacy
title_zh: 观察性隐私审计
authors: "Iden Kalemaj, Luca Melis, Maxime Boucher, Ilya Mironov, Saeed Mahloujifar"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=8TfiR1Lcvr"
tags: ["query:priv-sec"]
score: 7.0
evidence: 提出无需修改训练数据的观察性差分隐私审计框架，可用于大模型隐私评估
tldr: 现有差分隐私审计方法需修改训练数据，给大规模系统带来巨大工程开销。本文利用数据分布的固有随机性，提出一种观察性审计框架，无需变更原始数据集即可评估隐私保障。该方法将审计范围从传统成员推理扩展到受保护属性，为大型机器学习系统的隐私合规提供了一种轻量级评估工具。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 传统差分隐私审计要求注入金丝雀样本或移除训练数据，对于大规模系统操作复杂、成本高昂。
method: 利用数据分布的固有随机性，设计观察性审计框架，在不动原始数据的情况下进行隐私评估。
result: 该方法在多个任务上有效评估了差分隐私保障，并成功扩展到受保护属性审计。
conclusion: 该框架为大型系统提供了一种无需干预训练管线的实用隐私审计手段，降低了部署门槛。
---

## Abstract
Differential privacy (DP) auditing is essential for evaluating privacy guarantees in machine learning systems. Existing auditing methods, however, pose a significant challenge for large-scale systems since they require modifying the training dataset—for instance, by injecting out-of-distribution canaries or removing samples from training. Such interventions on the training data pipeline are resource-intensive and involve considerable engineering overhead.  We introduce a novel observational auditing framework that leverages the inherent randomness of data distributions, enabling privacy evaluation without altering the original dataset. Our approach extends privacy auditing beyond traditional membership inference to protected attributes, with labels as a special case, addressing a key gap in existing techniques. We provide theoretical foundations for our method and perform experiments on Criteo and CIFAR-10 datasets that demonstrate its effectiveness in auditing label privacy guarantees. This work opens new avenues for practical privacy auditing in large-scale production environments.

---

## 论文详细总结（自动生成）

# 论文《Observational Auditing of Privacy》详细总结

## 1. 核心问题与整体含义

- **研究动机**：差分隐私（DP）审计是评估机器学习系统隐私保障的核心手段。现有审计方法通常需要主动干预训练数据，例如注入分布外金丝雀样本（canaries）或故意移除部分训练样本。这类操作在大规模生产系统中不仅工程开销巨大、资源消耗高，而且可能干扰正常的训练管线，难以实际部署。
- **核心问题**：如何在不修改原始训练数据、不介入训练流程的前提下，对机器学习系统的隐私保障进行有效审计？
- **整体含义**：本文提出了“观察性审计”这一新范式，利用数据分布本身的天然随机性，实现零干预的隐私评估，将差分隐私审计从传统的成员推理扩展到受保护属性（如标签等），为大规模系统提供了一种轻量级、易落地的隐私合规评估工具。

## 2. 方法论

- **核心思想**：不注入额外样本或移除数据，而是直接观察现有训练数据的随机波动对模型输出或隐私指标的影响，利用这些自然存在的“扰动”来反推差分隐私参数（如 \(\varepsilon\)）。
- **技术关键**：
  - 将审计范围从单一成员推理扩展到受保护属性，例如标签隐私。标签可以视为一种特殊的受保护属性。
  - 建立在已有数据分布随机性基础上的理论框架，无需人工构造审计样本。
- **流程概述**（基于摘要推断）：
  1. 选取自然数据中的随机子集或根据属性划分的子群体；
  2. 训练多个模型变体（或利用随机性多次运行），观察模型在不同子集下的输出差异；
  3. 分析这些差异与差分隐私参数的关系，从而估计隐私损失。
- **创新点**：直接从“观察”中推断隐私保障，彻底消除了对训练管线干预的需求。

## 3. 实验设计

- **数据集/场景**：
  - Criteo（广告点击率预估，大规模表格数据）
  - CIFAR-10（图像分类）
- **审计目标**：标签隐私保障（label privacy guarantees）
- **对比方法**：摘要未明确列出具体对比方法，但传统审计方法（如注入金丝雀、留出样本）作为隐式基线；研究主要验证其“观察性审计”能否达到与传统方法可比的有效性。

## 4. 资源与算力

- 摘要和元数据中**未提及任何 GPU 型号、数量或具体训练时长**。因此无法给出算力消耗的准确说明。这一点需要在论文正文中核实。

## 5. 实验数量与充分性

- 文中描述在 **两个不同模态的数据集**（Criteo 和 CIFAR-10）上验证了方法的有效性，涉及标签隐私审计。
- 由于信息有限，无法得知是否包含消融实验、不同隐私参数设置、不同模型架构等。但从“demonstrates its effectiveness”推断，作者至少完成了关键场景下的功能验证。
- 实验的充分性从摘要看是合理的，但缺乏对照实验细节；若后续补充与其他审计方法的直接比较，将更加客观公平。

## 6. 主要结论与发现

- 所提出的观察性审计框架**无需修改训练数据**，即能有效评估差分隐私保障。
- 方法成功将隐私审计**从成员推理扩展到受保护属性（如标签）**，弥补了现有技术的空白。
- 在大规模生产环境中，该框架为隐私合规提供了一种**实用、低开销的审计方案**。

## 7. 优点

- **零干预**：完全避免对训练管线的改动，极大降低工程成本和部署门槛。
- **理论根基**：给出了基于数据分布随机性的理论支持，而非仅靠启发式。
- **审计范围拓宽**：除了传统的成员隐私，还能审计属性隐私（例如标签），扩展了审计的适用场景。
- **轻量且可扩展**：适合大规模生产系统，有望成为工业界隐私审计的可行工具。

## 8. 不足与局限

- **实验细节未知**：摘要未给出与其他审计方法的定量对比，方法的相对精度和可靠性有待在正式论文中验证。
- **理论假设未完全披露**：依赖数据分布“固有随机性”的有效性，若数据分布极其稳定或样本量小，可能难以观察到足够波动，影响审计效力。
- **计算开销未分析**：虽然没有修改训练数据，但观察式审计可能需要多次训练或统计，其计算成本未与传统方法对比。
- **范围有限**：目前主要在标签隐私上展示，对于更一般的属性或高维输入隐私，可能仍需要进一步扩展。
- **应用风险**：作为观察式审计，其估计的隐私损失可能保守或偏松，实际部署时需要谨慎校准。

（完）
