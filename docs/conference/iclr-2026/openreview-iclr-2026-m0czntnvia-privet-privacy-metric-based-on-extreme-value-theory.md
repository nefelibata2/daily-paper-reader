---
title: "PRIVET: PRIVacy metric based on Extreme value Theory"
title_zh: "PRIVET: 基于极值理论的隐私度量"
authors: "Antoine Szatkownik, Aurélien Decelle, Beatriz Seoane, Nicolas BEREUX, Léo Planche, Guillaume Charpiat, Burak Yelmen, Flora Jay, Cyril Furtlehner"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=M0czNtnviA"
tags: ["query:priv-sec"]
score: 9.0
evidence: 生成模型的样本级隐私度量
tldr: 针对深度生成模型训练敏感数据时的隐私泄露问题，本文提出PRIVET指标，利用极值统计理论分析最近邻距离，提供样本级、模态无关的隐私度量，突破了现有全局评估的局限，支持合成数据的精细隐私管控。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有生成模型隐私评估仅提供全局非解释性指标，缺乏样本级精细度量，阻碍合成数据安全部署。
method: 利用极值统计对最近邻距离建模，提出通用样本级隐私度量PRIVET。
result: 实验证明PRIVET能有效识别单个样本的隐私风险，跨多种数据模态适用。
conclusion: 该指标为生成模型隐私保护提供了可操作的评估工具，尤其适用于医疗等敏感数据。
---

## Abstract
Deep generative models are often trained on sensitive data, such as genetic sequences, health data, or more broadly, any copyrighted, licensed or protected content. This raises critical concerns around privacy-preserving synthetic data, and more specifically around privacy leakage, an issue closely tied to overfitting. Existing methods almost exclusively rely on global criteria to estimate the risk of privacy failure associated to a model, offering only quantitative non interpretable insights. The absence of rigorous evaluation methods for data privacy at the sample-level may hinder the practical deployment of synthetic data in real-world applications. Using extreme value statistics on nearest-neighbor distances, we propose PRIVET, a generic sample-based, modality-agnostic algorithm that assigns an individual privacy leak score to each synthetic sample. We empirically demonstrate that PRIVET reliably detects instances of memorization and privacy leakage across diverse data modalities, including settings with very high dimensionality, limited sample sizes such as genetic data and even under underfitting regimes. We compare our method to existing approaches under controlled settings and show its advantage in providing both dataset level and sample level assessments through qualitative and quantitative outputs. Additionally, our analysis reveals limitations in existing computer vision embeddings to yield perceptually meaningful distances when identifying near-duplicate samples.

---

## 论文详细总结（自动生成）

根据提供的论文元数据与摘要，以下是对该论文的结构化中文总结。

### 1. 论文的核心问题与整体含义
- **研究背景**：深度生成模型（如生成对抗网络、扩散模型）常使用医疗、基因组等敏感数据训练，可能记忆并泄露训练样本，带来隐私风险。
- **核心问题**：现有隐私评估方法（如差分隐私指标、最近邻距离）几乎都提供**数据集级别**的全局度量，缺乏**样本级**、可解释的细粒度泄漏评分。
- **研究动机**：缺少样本级隐私评估工具，阻碍合成数据在真实场景（尤其是高敏感领域）的安全部署。文中称“生成模型的隐私失败与过拟合紧密相关”，需要能识别单个合成样本是否泄露训练数据的方法。
- **整体含义**：提出一种基于极值理论（Extreme Value Theory）的通用、跨模态样本级隐私度量，使每个合成样本都有一个个体泄漏风险得分，支持更精细的隐私管控。

### 2. 方法论：核心思想与关键技术细节
- **核心思想**：利用**最近邻距离**来刻画合成样本与训练集之间的关系，并通过**极值统计**为每个合成样本建模其最近邻距离的分布尾部，进而得到泄漏概率/得分。
- **关键技术细节**（基于摘要描述）：
  - 假设对于一个合成样本，在训练集中寻找其最近邻（或近邻），计算距离。
  - 运用极值理论（如广义帕累托分布、峰值阈值法等）对这些最近邻距离的尾部行为建模，将距离转化为一个概率分数，表示该合成样本“异常接近”某个训练样本的程度。
  - 该分数即为 **PRIVET（PRIVacy metric based on Extreme value Theory）** 指标，可跨数据模态（图像、基因序列等）直接应用，不依赖于特定嵌入模型，但文中也提及现有计算机视觉嵌入在感知重复样本时有局限性。
- **算法流程**（推测）：
  1. 给定训练集 \(X\) 和合成样本 \(s\)，计算 \(s\) 到 \(X\) 中所有样本的距离（或近似最近邻），取最小距离 \(d_{min}\)。
  2. 利用极值分布拟合全体合成样本最近邻距离的尾部，根据 \(d_{min}\) 在拟合分布中的位置（如生存函数），输出一个泄漏得分（例如 \(p\) 值或对数概率）。
  3. 得分越高，表示 \(s\) 越可能是记忆样本，隐私泄漏风险越大。
- **特点**：样本级、与模态无关、通用、不需要训练额外模型（仅依赖距离度量）。

### 3. 实验设计：数据集、场景与对比方法
- **数据集/场景**：
  - 高维度数据、小样本的基因数据（genetic data）。
  - 其他未具体指明的多种数据模态（abstract 提到“diverse data modalities”）。
  - 计算机视觉嵌入实验，揭示现有嵌入在识别重复样本上的距离感知缺陷。
- **对比方法**：
  - 现有全局隐私评估准则（具体名称未列出，摘要称“existing approaches under controlled settings”）。
  - 可能包括基于最近邻距离的简单阈值方法、差分隐私审计、成员推断攻击等（需要查看全文，但摘要未详述）。
- **评价维度**：是否能可靠检测**记忆（memorization）与隐私泄漏**，提供定性与定量输出，覆盖样本级和数据集级评估。

### 4. 资源与算力
- **论文明确给出信息**：未在摘要和元数据中说明使用的GPU型号、数量、训练时长等计算资源细节。
- **推断**：PRIVET 算法本身基于距离计算与极值分布拟合，可能不需要大量 GPU 算力，但生成模型的训练过程可能需要。由于摘要未提及，此处缺少具体数据。

### 5. 实验数量与充分性
- **实验数量**：摘要提及“across diverse data modalities, including settings with very high dimensionality, limited sample sizes such as genetic data and even under underfitting regimes”，并进行了“controlled settings”下的比较。可以判断至少包含3类以上数据场景（基因数据、图像嵌入、过拟合/欠拟合条件）。具体数目未知。
- **充分性与客观性**：
  - 优点：覆盖不同维度、样本量、训练状态（欠拟合等），体现评估的广泛性。
  - 不足：摘要未提供定量结果、统计显著性或消融实验细节，无法判断实验是否严格充分。需全文核实。
  - 比较方法仅提及“现有方法”，缺乏具体名称和公正对比的细节描述。

### 6. 主要结论与发现
- PRIVET 能够**可靠地检测记忆和隐私泄漏**，提供**样本级泄漏得分**，同时支持数据集级别的聚合评估。
- 该方法在不同数据模态和挑战性条件下均有效，包括**高维小样本场景（如基因数据）**和**欠拟合模型**。
- 相比现有全局指标，PRIVET 的优势在于给出**可操作的、可解释的个体级隐私评估**，有助于合成数据的安全部署。
- 另外发现现有计算机视觉嵌入在为识别近似重复样本提供感知上有意义的距离方面存在局限。

### 7. 优点
- **样本级隐私度量**：突破传统全局评估限制，能定位具体泄漏样本，便于下游决策（如过滤高风险合成记录）。
- **模态无关性**：仅依赖距离定义，可应用于图像、文本、基因组等多种数据类型。
- **理论基础强**：基于极值理论，给出概率解释，提高可信度。
- **计算经济性**：无需重新训练模型，可后验分析，易于集成到现有生成流程中。
- **实际应用价值高**：特别适用于医疗、基因等敏感数据场景，可推动合成数据安全标准。

### 8. 不足与局限
- **摘要信息有限**：缺乏定量对比结果、具体距离度量选择的影响分析、超参数设置等。
- **依赖距离质量**：若原始空间或嵌入空间的距离不能反映感知相似性（如摘要提到的CV嵌入问题），则PRIVET可能失效。
- **极值假设**：对最近邻距离的极值分布假设需要验证，低样本量下尾部估计可能不稳定。
- **对比实验不详**：未列出具体对比方法、基准数据集名称、评估指标（如AUC、F1），难以判断相对优越性。
- **部署门槛**：需要为每个生成模型计算全套训练样本的距离，大规模数据集下计算成本可能较高；摘要未讨论近似检索方法。
- **未见攻击鲁棒性**：未提及是否对主动攻击（如属性推断、重构攻击）提供样本级防御指示。

（完）
