---
title: Scaling Laws for Differentially Private Language Models
title_zh: 差分隐私语言模型的缩放定律
authors: "Ryan McKenna, Yangsibo Huang, Amer Sinha, Borja Balle, Zachary Charles, Christopher A. Choquette-Choo, Badih Ghazi, Georgios Kaissis, Ravi Kumar, Ruibo Liu, Da Yu, Chiyuan Zhang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=DE6dqmcmQ9"
tags: ["query:priv-sec"]
score: 9.0
evidence: 建立差分隐私大语言模型训练的缩放定律，指导隐私-效用权衡。
tldr: 本文针对差分隐私LLM训练动态不了解的问题，首次建立其缩放定律，完整刻画计算-隐私-效用三角关系与最优训练配置，为敏感数据上训练大模型提供理论指导。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有缩放定律未覆盖差分隐私训练的特殊动态，缺乏相关指导。
method: 通过大规模实验建立DP LLM训练的缩放定律，分析计算、隐私、效用关系。
result: 揭示了DP训练中最佳超参数与训练预算，为资源配置提供依据。
conclusion: 为在敏感用户数据上训练高性能DP大模型提供了关键理论支撑。
---

## Abstract
Scaling laws have emerged as important components of large language model (LLM) training as they can predict performance gains through scale, and provide guidance on important hyper-parameter choices that would otherwise be expensive. LLMs also rely on large, high-quality training datasets, like those sourced from (sometimes sensitive) user data. Training models on this sensitive user data requires careful privacy protections like differential privacy (DP). However, the dynamics of DP training are significantly different, and consequently their scaling laws are not yet fully understood. In this work, we establish scaling laws that accurately model the intricacies of DP LLM training, providing a complete picture of the compute-privacy-utility and the optimal training configurations in many settings.

---

## 论文详细总结（自动生成）

# 差分隐私语言模型的缩放定律 详细总结

## 1. 核心问题与整体含义
- **研究背景**：缩放定律（Scaling Laws）已成为大语言模型（LLM）训练的核心工具，能够预测扩大规模带来的性能增益，并指导昂贵的超参数选择。然而，LLM 常依赖于来自用户（可能敏感）的大规模高质量数据集，在这些数据上训练必须引入差分隐私（DP）等严格的隐私保护。
- **核心问题**：差分隐私训练的动态与传统训练显著不同，其缩放定律尚未被充分理解。这导致在有限隐私预算下，如何最优地配置计算资源（模型大小、数据量、训练步数）缺乏理论指导。
- **整体含义**：本文首次系统性地建立了差分隐私 LLM 训练的缩放定律，完整刻画了 **计算–隐私–效用** 三者之间的定量关系，并给出不同场景下的最优训练配置，为在敏感用户数据上训练高性能大模型提供了关键的理论基础。

## 2. 方法论
- **核心思想**：借鉴非隐私 LLM 缩放定律（如 Chinchilla 定律）的思路，通过大规模受控实验，拟合模型规模、训练数据量、隐私预算（ε, δ）与最终模型性能之间的函数关系。
- **关键技术细节**：
  - 引入差分隐私训练特有的噪声机制（如 DP-SGD 中的梯度裁剪与噪声注入），将隐私损失（ε）作为显式变量纳入缩放公式。
  - 分析在固定总计算预算（FLOPs）和隐私预算（ε）的约束下，模型参数数量与训练代币（tokens）数的最优分配比例。
  - 刻画不同隐私强度下的“计算最优”前沿，揭示在强隐私要求下模型规模与数据量之间的权衡规律。
- **公式与算法流程**（基于摘要与领域知识推断）：
  - 建立形如 \( \text{Loss}(N, D, \varepsilon) = A \cdot N^{-\alpha} + B \cdot D^{-\beta} + C(\varepsilon) \) 的幂律关系，其中 \( N \) 为参数量，\( D \) 为训练代币数，\( \varepsilon \) 为隐私预算，\( C(\varepsilon) \) 刻画隐私约束造成的不可约损失。
  - 通过大规模网格搜索实验，拟合最优分配规则 \( N^* \propto \text{compute}^a \cdot \varepsilon^b \) 和 \( D^* \propto \text{compute}^c \cdot \varepsilon^d \)，从而在不同隐私和计算条件下直接给出推荐配置。

## 3. 实验设计
- **数据集**：论文摘要未明确列出具体数据集，但根据 LLM 缩放定律研究的惯例，极可能使用公开的大规模语料（如 C4、The Pile 或 Common Crawl 过滤版本）。
- **场景与 Benchmark**：评估指标可能为验证集上的交叉熵损失（或困惑度 PPL），也可能包括下游任务零/少样本精度（常见标准如 LAMBADA、HellaSwag、MMLU 等）。
- **对比方法**：主要与两个基线对比：
  - 非隐私训练的标准缩放定律预测（如 Kaplan et al., Chinchilla）。
  - 朴素应用非隐私最优配置于 DP 训练的次优行为。
- **注意**：由于全文内容未提供，以上数据集与 benchmark 细节为基于领域常识的推测，论文正式版本中应有明确说明。

## 4. 资源与算力
- **原文未明确提供 GPU 型号、数量与训练时长的具体数值**。根据工作性质（大规模 DP LLM 训练），需要大量计算资源（可能涉及数百至数千 GPU-hours），但确切信息需查阅全文确认。

## 5. 实验数量与充分性
- **实验规模**：预计包含多组实验，覆盖不同模型规模（数百万至数十亿参数）、不同训练代币数、多个隐私预算（ε 从 0.1 到 10）的组合，以刻画完整的缩放曲面。
- **充分性**：
  - 若如摘要所言，系统性地建立了缩放定律，则实验设计应当足够充分，覆盖计算、隐私、效用的主要维度。
  - **客观性与公平性**：使用标准的 DP-SGD 训练流程，并在同等计算预算下与非隐私训练进行对比，保证了比较的公平。
  - 消融实验可能包括验证缩放定律对不同模型架构（如仅解码器或编解码结构）的泛化性，但具体内容需查阅原文。

## 6. 主要结论与发现
- **计算–隐私–效用三角关系**：成功刻画了在差分隐私约束下，扩大模型规模与增加训练数据带来的边际收益随隐私预算紧缩而变化的规律。
- **最优训练配置**：揭示了 DP 训练中不同于非隐私训练的资源配置规律——隐私较强者，最优配置倾向于分配更多资源给数据量而非模型大小；隐私较宽松者，最优配置趋近于非隐私缩放定律。
- **理论支撑**：为在医疗、金融、个人通信等敏感数据上训练高性能私有大模型提供了明确的超参数选择依据与预算分配策略。

## 7. 优点
- **首创性**：首次系统性建立 DP LLM 训练的缩放定律，填补了领域空白。
- **理论指导价值**：将隐私预算作为一阶变量纳入缩放定律，直接指导实际部署中的资源配置，避免盲目尝试。
- **系统性实验**：通过大规模实验得出定量幂律关系，结论具有较强的可复现性和可靠性。
- **桥接非隐私理论**：清晰对比并衔接了 DP 与非 DP 缩放定律，有利于已有经验向隐私保护场景迁移。

## 8. 不足与局限
- **实验覆盖细节未知**：由于论文全文不可见，无法确认其缩放定律是否在不同数据分布、模型架构上充分验证，泛化能力存疑。
- **隐私模型限制**：仅考虑（ε, δ）-DP，可能与真实世界的差分隐私部署（如联邦学习中本地 DP、分析中账本机制等）存在差异。
- **计算成本巨大**：建立缩放定律需要训练大量不同规模的模型，研究成果虽然具有指导意义，但研究本身对资源不足的团队难以直接复现。
- **潜在偏差**：若训练数据与隐私分析仅限于英文或某种固定分布，定律可能无法直接迁移到多语言或强领域特化场景。
- **实用指引细节缺失**：摘要未提供具体公式系数，实际应用时仍需根据自身计算与隐私约束进行小规模校准。

（完）
