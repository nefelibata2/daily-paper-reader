---
title: Probabilistic Reasoning with LLMs for Privacy Risk Estimation
title_zh: 使用大语言模型进行隐私风险估计的概率推理
authors: "Jonathan Zheng, Alan Ritter, Sauvik Das, Wei Xu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=HMVQ00vabY"
tags: ["query:priv-sec"]
score: 9.0
evidence: 使用LLM估计文本隐私风险
tldr: 本文针对用户生成文档的隐私风险量化问题，提出BRANCH方法，利用大语言模型估计文本的k-隐私值。该方法将个人信息联合概率分布分解为因子，通过贝叶斯网络分别估计各因子概率并组合计算。实验表明，该方法能有效衡量文本的可重识别风险，为隐私保护提供新的度量工具。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 用户生成文档常含隐私信息，需量化其泄露风险。
method: 提出BRANCH方法，将个人信息联合分布因子化，用贝叶斯网络估计各因子概率。
result: 在合成和真实数据上，BRANCH能准确估计k-隐私值。
conclusion: BRANCH为LLM隐私风险评估提供了有效工具。
---

## Abstract
Probabilistic reasoning is a key aspect of both human and artificial intelligence that allows for handling uncertainty and ambiguity in decision-making. In this paper, we introduce a new numerical reasoning task under uncertainty for large language models, focusing on estimating the privacy risk of user-generated documents containing privacy-sensitive information. We propose BRANCH, a new LLM methodology that estimates the $k$-privacy value of a text—the size of the population matching the given information. BRANCH factorizes a joint probability distribution of personal information as random variables.  The probability of each factor in a population is estimated separately using a Bayesian network and combined to compute the final $k$-value. Our experiments show that this method successfully estimates the $k$-value 73% of the time, a 13% increase compared to o3-mini with chain-of-thought reasoning. We also find that LLM uncertainty is a good indicator for accuracy, as high variance predictions are 37.47% less accurate on average.

---

## 论文详细总结（自动生成）

# 论文总结：Probabilistic Reasoning with LLMs for Privacy Risk Estimation

## 1. 核心问题与整体含义
- **研究动机**：用户生成文本（如社交媒体帖子、私人笔记）常常隐含个人身份信息，但现有技术难以精确量化这些敏感信息在人群中的唯⼀性（即可重识别风险）。
- **核心问题**：如何利用大语言模型，对非结构化文本中蕴含的隐私风险进行**数值化、概率化的推理**，即估计文本的 **k-隐私值**（k-privacy）——指在⼀个参考人群中与该文本信息相匹配的个体数量。k 值越小，文本越独特，隐私泄露风险越⾼。
- **整体含义**：本文将隐私风险评估建模为概率推理任务，为大模型在不确定性下的数值推理提供了新的应用场景，同时为隐私保护提供了⼀种可量化的度量工具。

## 2. 提出的方法论：BRANCH
- **核心思想**：将文本所包含的个人信息（如属性、关系）视为随机变量，其联合概率分布对应于 k-隐私值。通过**因子分解**将联合分布拆解为多个条件概率的乘积，降低直接估计的复杂度。
- **关键技术环节**：
  - 利用基于 **贝叶斯网络** 的因子分解结构，将个人信息联合分布表示为若干因子的乘积。每个因子对应⼀组随机变量的条件概率。
  - 每个因子的概率由 LLM 分别估计（例如，基于已知人群统计数据或常识推理）。
  - 最终将各因子概率相乘，得到该文本在人群中的匹配概率，进而换算为 **k-隐私值**。
- **算法流程**（文字描述）：
  1. 输入⼀段用户生成文本，提取其中可关联到个人身份的属性集合。
  2. 构建适用于该属性集的贝叶斯网络，确定因子分解形式：P(属性集) = ∏ P(子集｜父节点集)。
  3. 对每个因子，利用 LLM 结合上下⽂（如人口统计知识）估计条件概率。
  4. 组合因子概率，计算整体匹配概率 p，输出 k = 1/p（或与之等价的 k-值）。
- **重要补充**：文中还利用 LLM 的不确定性（如预测方差）作为准确性指标，高方差的预测意味着 k-值估计更不可靠。

## 3. 实验设计
- **数据集**：
  - 使用**合成数据**和**真实数据**（具体数据集名称在给出的摘要和元数据中未提及）。合成数据用于构造已知真实 k 值的场景，真实数据则来自用户生成文档。
- **评估基准**：
  - 以 k-隐私值的估计准确率（例如“成功估计 k 值的比例”）为主要指标。文中报告“正确估计的比率为 73%”。
- **对比方法**：
  - 主要对比基线是 **o3-mini 结合链式思维推理（chain-of-thought）**，BRANCH 方法相较于该基线提升了 13% 的准确率。
- **其他实验**：
  - 考察 LLM 预测的不确定性与准确率的关系，发现高方差预测的平均准确率低 37.47%。

## 4. 资源与算力
- 在提供的摘要和元数据中，**没有明确提及**所使⽤的 GPU 型号、数量、训练/推理时长或任何算⼒消耗细节。

## 5. 实验数量与充分性
- **实验组数**：从描述看，至少包含合成数据和真实数据两类实验，以及⼀组关于不确定性与准确率的相关性分析。具体实验数量（如不同 k-值区间、不同领域文本）未详细给出。
- **充分性评估**：
  - 较难判断充分性，因为摘要仅提供了总体准确率和与⼀个基线的对比。未说明是否进行了消融研究（如去除贝叶斯因子分解、仅用单步概率估计）、超参数敏感度分析或不同 LLM 规模的对比。
  - 对比方法只提到了 o3-mini，缺乏与其他推理策略或传统匿名化方法的比较，客观公平性有待进⼀步验证（需要完整论文确认）。
- **潜在偏差**：数据集的具体分布、数量以及隐私属性种类未知，难以评估结果的可泛化性。

## 6. 主要结论与发现
- BRANCH 方法能够有效估计用户文本的 k-隐私值，准确率达到 **73%**。
- 相比 o3-mini + 链式思维推理，提升了 **13 个百分点**，证明了因子分解结合贝叶斯网络对于复杂概率推理的必要性。
- LLM 自身的**预测不确定性可以作为估计准确性的有效信号**：高方差预测对应的 k-值平均准确性降低 37.47%，为实际应用中的信任度评估提供了参考。

## 7. 优点
- **方法论创新**：将隐私风险估计转化为可因子化的概率推理任务，利用 LLM 的常识知识估计条件概率，避免了传统方法对结构化数据库的依赖。
- **任务设计价值**：引入“k-隐私值”作为 LLM 不确定性数值推理的新 benchmark，促进了对模型概率推理能力的研究。
- **可解释性**：因子分解结构使得隐私风险可追溯至具体属性组合，便于用户理解。
- **不确定性利用**：巧妙地将 LLM 不确定性作为预测质量指标，有利于实际部署中的风险管理。

## 8. 不足与局限
- **信息不全**：基于现有摘要和元数据，实验细节（数据集构成、样本量、评价指标细粒度）缺失，无法评估全面性。
- **比较方法有限**：仅与 o3-mini 对比，未涉及其他隐私度量方法（如基于差分隐私的评估）或传统统计推断，说服力有待加强。
- **领域适应性未知**：未提及文本领域、语言、文化差异对 k-值估计的影响；在合成数据上的成功可能不完全适用于真实多样文本。
- **依赖先验知识**：贝叶斯网络结构和 LLM 的概率估计依赖于高质量的常识和人口统计知识，在处理小众或反事实属性时可能产生偏差。
- **算力与可复现性**：未披露模型调用开销或计算资源，可复现性受到影响。

（完）
