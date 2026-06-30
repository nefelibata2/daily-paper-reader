---
title: Differential Privacy for Transformer Embeddings  with Nonparametric Variational Information Bottleneck
title_zh: 基于非参数变分信息瓶颈的Transformer嵌入差分隐私
authors: "Dina El Zein, James Henderson"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=f4B4ohWO53"
tags: ["query:priv-sec"]
score: 8.0
evidence: 通过非参数变分差分隐私保护Transformer嵌入的隐私
tldr: 针对Transformer嵌入可能泄露输入敏感信息的问题，提出非参数变分差分隐私(NVDP)方法，将非参数变分信息瓶颈层集成到Transformer中，生成带噪嵌入用于共享。实验表明NVDP在保证强隐私的同时维持了嵌入的可用性，为文本数据的安全共享提供了新途径。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: Transformer嵌入多向量特性加剧了隐私泄露风险，攻击者可能重构输入。
method: 提出NVDP，将非参数变分信息瓶颈层与差分隐私结合，对嵌入加噪。
result: NVDP在保护隐私的同时保持了嵌入在下游任务中的有效性。
conclusion: NVDP为文本数据的隐私保护共享提供了一个理论保证且实用的方法。
---

## Abstract
We propose a privacy-preserving method for sharing text data by sharing noisy versions of their transformer embeddings.
It has been shown that hidden representations learned by deep models can encode sensitive information from the input, making it possible for adversaries to recover the input data with considerable accuracy.  This problem is exacerbated in transformer embeddings because they consist of multiple vectors, one per token. To mitigate this risk, we propose Nonparametric Variational Differential Privacy (NVDP), which ensures both useful data sharing and strong privacy protection.  We take a differential privacy approach, integrating a Nonparametric Variational Information Bottleneck (NVIB) layer into the transformer architecture to inject noise into its multi-vector embeddings and thereby hide information, and measuring privacy protection with Rényi divergence and its corresponding Bayesian Differential Privacy (BDP) guarantee.  Training the NVIB layer calibrates the noise level according to utility.  We test NVDP on the GLUE benchmark and show that varying the noise level gives us a useful tradeoff between privacy and accuracy.  With lower noise levels, our model maintains high accuracy while offering strong privacy guarantees, effectively balancing privacy and utility.

---

## 论文详细总结（自动生成）

# 基于非参数变分信息瓶颈的Transformer嵌入差分隐私

## 1. 论文的核心问题与整体含义

- **背景动机**：Transformer 模型生成的嵌入（embedding）在共享时可能泄露原始输入中的敏感信息。已有研究表明，深度模型的隐藏表示能够被攻击者利用，以较高精度重构输入数据。
- **问题聚焦**：Transformer 嵌入由多个向量（每个词符一个向量）组成，这种多向量特性加剧了隐私泄露风险，因为更多维度的信息暴露给了潜在攻击者。
- **整体含义**：论文旨在提出一种既能保证嵌入可用性、又能提供强隐私保护的方法，使得文本数据能够在保护用户隐私的前提下安全共享。

## 2. 论文提出的方法论

- **核心思想**：将**非参数变分信息瓶颈（NVIB）**与**差分隐私（DP）**相融合，直接在 Transformer 架构中加入一个 NVIB 层，对多向量嵌入注入噪声，从而掩盖敏感信息。隐私保护程度通过 **Rényi 散度**及对应的**贝叶斯差分隐私（BDP）**理论来量化。
- **关键技术细节**：
  - 在 Transformer 中嵌入一个 **非参数变分信息瓶颈层**（NVIB 层），该层利用非参数先验（例如基于狄利克雷过程）学习对嵌入进行压缩。
  - 训练过程中，NVIB 层会根据下游任务的效用（utility）自动校准噪声水平，从而动态平衡隐私与精度。
  - 噪声的注入满足**差分隐私**要求，具体通过计算 Rényi 散度来给出 **BDP** 保证，从而为隐私损失提供可解释的理论界。
- **算法流程（文字描述）**：
  1. 将输入文本送入 Transformer 编码器，生成原始的多向量嵌入序列。
  2. 在嵌入序列上施加 NVIB 层，通过变分推断得到压缩后的隐含表示，同时引入随机噪声（由差分隐私机制控制）。
  3. 输出的带噪嵌入可直接共享或用于下游任务。
  4. 训练目标同时考虑下游任务损失与信息瓶颈约束，并通过调整温度或正则化参数来改变噪声量级，实现隐私‑效用权衡。

## 3. 实验设计

- **数据集/场景**：使用 **GLUE 基准**（General Language Understanding Evaluation），包含多种自然语言理解任务，如文本蕴含、情感分析、语义相似度等。
- **Benchmark 与基线**：论文主要考察噪声水平变化时，下游任务准确率的保持情况。虽然没有明确列出对比方法，但预期会对比：
  - **无隐私保护的基线**：原始的 Transformer 嵌入，不注入噪声。
  - 可能还对比了其他简单的加噪方案或信息瓶颈方法。
- **评价指标**：
  - **任务准确率**（Accuracy）或 GLUE 各子任务对应的指标。
  - **隐私保护程度**：通过 Rényi 散度导出的 BDP 参数 ε 来衡量（通常 ε 越小，隐私保护越强）。

## 4. 资源与算力

- 论文摘要及提供的元数据**未提及**所使用的 GPU 型号、训练卡数、训练时长等算力相关信息，因此无法给出具体算力消耗。

## 5. 实验数量与充分性

- **实验规模**：至少覆盖了 GLUE 基准中的多个任务，并在不同噪声水平（对应不同隐私预算）下进行了测试，以绘制“隐私‑效用”权衡曲线。
- **充分性分析**：
  - 通过调节噪声水平展示了一条完整的权衡曲线，能够很好地说明方法在不同隐私需求下的表现。
  - 缺少与其它隐私保护嵌入方法（如基于随机响应的差分隐私、对抗训练等）的直接对比，可能使得方法的相对优势不够突出。
  - 仅在 GLUE 上测试，未涉及其他领域（如医疗、法律文本）或跨语言场景，泛化性有待验证。
- **客观公平性**：使用标准 GLUE 评估协议，噪声水平的控制透明，隐私度量有理论支撑，实验设计基本客观。

## 6. 论文的主要结论与发现

- NVDP 能够有效保护 Transformer 嵌入中的隐私，防止输入信息被重构，同时通过噪声校准维持了下游任务的可用性。
- 通过改变噪声水平，可以获得一条**明确的隐私‑效用权衡曲线**：在较低噪声水平下，模型能保持高准确率，并提供较强的隐私保证，从而在实际应用中做到平衡。
- 该方法为文本数据的安全共享提供了一种**兼具理论保证和实用价值**的方案。

## 7. 优点

- **理论严密**：结合非参数变分信息瓶颈与贝叶斯差分隐私，用 Rényi 散度提供可计算的隐私界，使隐私保护具有可解释性。
- **端到端训练**：NVIB 层集成在 Transformer 内部，可以联合优化隐私与效用，避免后处理噪声导致的次优问题。
- **灵活可控**：通过调节噪声水平，用户能够根据应用场景在隐私和精度之间做出弹性选择。
- **多向量嵌入适配**：方法特别针对 Transformer 的多向量特性进行设计，比简单地对固定维向量加噪更具针对性。

## 8. 不足与局限

- **实验覆盖有限**：仅在通用 NLP 基准 GLUE 上验证，未在领域特定数据（如金融、医疗）或需要更强隐私保证的场景中测试，无法评估其对极端隐私攻击的防护效果。
- **对比基线欠缺**：摘要中未提与其他隐私保护技术（如局部差分隐私、对抗正则化等）的横向对比，难以判断 NVDP 在同类方法中的竞争力。
- **应用限制**：方法依赖于训练一个 Transformer + NVIB 模型，对于无训练授权或计算资源不足的场景可能难以直接使用；此外，贝叶斯差分隐私的保证依赖特定分布假设，实际部署时可能需额外校验。
- **时态说明**：本文提交至 ICLR 2026 被拒，其结论与实验可能尚未经过同行严格纠偏，且文中提及日期为 2025 年，具有一定前瞻性，需注意其技术成熟度。

（完）
