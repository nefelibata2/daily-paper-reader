---
title: Private Data Synthesis for Preference Alignment of Large Language Models
title_zh: 用于大型语言模型偏好对齐的隐私数据合成
authors: "Fengyu Gao, Jing Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=GqNgK7LXBn"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出差分隐私合成偏好数据，实现隐私保护LLM对齐
tldr: 偏好对齐训练涉及敏感用户提示和判断，存在隐私风险。DPPrefSyn 算法通过 DP 聚类、PCA 降维和公梯提示节约预算，生成差分隐私合成偏好数据。实验在三个基准上验证了合成数据的效用，同时保护隐私。该工作为 LLM 隐私保护对齐提供了实用解决方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 真实人类偏好数据包含敏感信息，偏好对齐引发隐私担忧。
method: 提出DPPrefSyn，通过DP聚类、PCA降维等生成合成偏好数据。
result: 合成数据在多个基准上保持模型性能，有效保护隐私。
conclusion: 实现隐私保护下的LLM偏好对齐，降低数据泄露风险。
---

## Abstract
Preference alignment has become a crucial technique for aligning large language models (LLMs) with human values. However, training on real human preference data raises privacy concerns, as these datasets often contain sensitive user prompts and human judgments. To address this, we propose **DPPrefSyn**, a novel algorithm for generating differentially private (DP) synthetic preference data to enable privacy-preserving preference alignment. DPPrefSyn addresses three key challenges: modeling diverse human preferences via DP clustering and per-cluster DP scoring models; reducing dimensionality with DP-PCA to improve efficiency; and conserving privacy budget by leveraging public prompts. We conduct extensive experiments on three standard benchmarks and compare our method with DP fine-tuning on real data. Our results show that our framework achieves competitive performance under strong privacy guarantees. These results open up new possibilities for preference alignment with privacy protection for a broad range of applications. To the best of our knowledge, this is the first work to generate DP synthetic preference data for LLM alignment.

---

## 论文详细总结（自动生成）

# 论文总结：用于大型语言模型偏好对齐的隐私数据合成

## 1. 论文的核心问题与整体含义

- **研究背景**：大型语言模型（LLM）的偏好对齐（如RLHF、DPO）依赖真实人类偏好数据，这类数据通常包含敏感的用户提示和人类判断，直接收集和使用会引发严重的隐私泄露风险。
- **核心问题**：如何在保护数据隐私的前提下，为LLM的偏好对齐训练提供高质量的偏好数据，以同时实现模型对齐与隐私保护。
- **整体意义**：该工作首次提出生成**差分隐私合成偏好数据**的方案，为隐私敏感场景下的LLM对齐提供了实用路径，拓宽了LLM安全部署的应用范围。

## 2. 论文提出的方法论

- **算法框架**：**DPPrefSyn**，一个面向LLM对齐的差分隐私合成偏好数据生成算法。
- **核心技术点**：
  - **多样化偏好建模**：通过**差分隐私聚类（DP clustering）** 将用户偏好分组，并为每个聚类训练独立的差分隐私评分模型，以捕捉偏好的多模态分布。
  - **降维提效**：采用**差分隐私主成分分析（DP-PCA）** 对高维表征进行降维，减少后续计算中的噪声注入量，提升效率。
  - **隐私预算节约**：借助**公开提示（public prompts）** 来引导合成过程，避免在生成式流程中消耗宝贵的隐私预算。
- **流程概述**：先对敏感偏好数据执行DP聚类与DP-PCA，得到低维聚类结构；再基于各聚类训练DP评分模型；最后利用公开提示和DP模型生成差分隐私保证的合成偏好样本，用于下游LLM对齐训练。

## 3. 实验设计

- **数据集/场景**：在**三个标准基准（three standard benchmarks）** 上进行评估，但摘要未列出具体数据集名称。
- **对比方法**：与在真实数据上进行**差分隐私微调（DP fine-tuning on real data）** 的方法进行直接比较。
- **评估指标**：关注模型性能的保持程度，即在强隐私保证下合成数据对齐效果是否接近真实数据训练。

## 4. 资源与算力

- 文中（摘要及元数据）**未明确提及**所使用的GPU型号、数量或训练时长等算力信息。原文可能因截断而缺失，需查阅完整论文获取详细资源配置。

## 5. 实验数量与充分性

- **实验组数**：摘要提到“广泛实验”，至少包括三个基准数据集上的性能对比，以及与DP真实数据微调的对比；可能还包含消融实验（如不同隐私预算ε值的影响），但具体数量未给出。
- **充分性与公平性**：从信息推断，实验覆盖多个基准，对比了直接的隐私对齐基线，具备基本公平性。然而，因缺少细粒度实验设置说明，难以全面判断实验是否充分（如是否涵盖不同模型规模、合成数据量等）。

## 6. 主要结论与发现

- DPPrefSyn能够在**强隐私保证**下，使合成数据训练的LLM获得**有竞争力的性能**，效果可与在真实数据上应用差分隐私微调的方法相媲美。
- 该方法为隐私保护下的LLM偏好对齐开启了新可能，首次实现了以合成方式生成满足差分隐私的对齐数据。

## 7. 优点与亮点

- **创新性**：首个提出通过合成差分隐私偏好数据解决LLM对齐隐私问题的框架，填补了研究空白。
- **技术综合性**：巧妙结合DP聚类、DP-PCA与公开提示，在严格隐私预算内捕捉偏好多样性并提升效率。
- **实用性**：无需访问原始敏感数据即可训练对齐模型，适用于医疗、金融等隐私敏感领域。
- **性能实证**：在多个基准上验证了方法的有效性，且有明确的对比基线。

## 8. 不足与局限

- **实验细节缺失**：现有摘要未披露具体基准数据集、模型规模、超参数设置，限制了对实验充分性的评估。
- **偏差风险**：依赖公开提示可能引入分布偏移，若公开提示不能良好覆盖目标领域，合成数据质量会下降；DP聚类阶段的噪声可能导致偏好组态失真。
- **应用限制**：方法仅在标准基准上验证，未展示在极端隐私预算（如ε<1）或大规模部署下的表现；合成数据的语义一致性、对抗鲁棒性未深入讨论。
- **未讨论计算开销**：DP聚类与DP-PCA的实际隐私-效率权衡未量化，可能在大规模数据上计算成本较高。

（完）
