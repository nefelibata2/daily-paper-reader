---
title: Differentially Private Conditional Text Generation with RL-Boosted Control
title_zh: 基于强化学习增强控制的差分隐私条件文本生成
authors: "Yuzheng Hu, Ryan McKenna, Da Yu, Shanshan Wu, Han Zhao, Zheng Xu, Peter Kairouz"
date: 2025-09-15
pdf: "https://openreview.net/pdf?id=TNIFLLzOTo"
tags: ["query:priv-sec"]
score: 9.0
evidence: 面向语言模型的分层差分隐私条件文本生成
tldr: 本文提出分层框架，将差分隐私合成文本生成分解为特征学习和条件生成，并结合强化学习优化控制能力，解决了现有DP生成数据集属性保留差、控制粗糙的问题，为语言模型隐私保护训练提供了高质量合成方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有DP合成文本数据集难以保留关键统计属性，缺乏细粒度控制，效用损失大。
method: 设计分层框架，分离特征学习与条件文本生成，利用强化学习提升生成控制。
result: 实验表明该方法能生成高质量、统计保真的DP文本，优于先前工作。
conclusion: 分层架构和RL控制有效提升了DP文本生成的实用性和可控性，赋能隐私安全语言模型。
---

## Abstract
Generating high-quality synthetic text under differential privacy (DP) is critical for training and evaluating language models without compromising user privacy. Prior work on synthesizing DP *datasets* often fail to preserve key statistical attributes, suffer utility loss from the noise required by DP, and lack fine-grained control over generation. To address these challenges, we make two contributions. First, we introduce a hierarchical framework that decomposes DP synthetic text generation into two subtasks: *feature learning* and *conditional text generation*. This design explicitly incorporates learned features into the generation process and simplifies the end-to-end synthesis task. Through systematic ablations, we identify the most effective configuration: a rich tabular schema as feature, a DP tabular synthesizer, and a DP fine-tuned conditional generator, which we term ACTG (**A**ttribute-**C**onditioned **T**ext **G**eneration). Second, we propose Anchored RL (ARL), a post-training method that improves the instruction-following ability of ACTG for conditional generation. ARL combines RL to boost control with an SFT anchor on best-of-$N$ data to prevent reward hacking. Together, these components form our end-to-end algorithm **ACTG-ARL**, which advances both the quality of DP synthetic text (+20\% MAUVE over prior work) and the control of the conditional generator under strong privacy guarantees.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 核心问题与整体含义
- **研究动机**：生成高质量的差分隐私合成文本对于在不泄露用户隐私的前提下训练与评估语言模型至关重要。然而，现有方法存在明显缺陷：
  - 合成的差分隐私数据集往往难以保留原文的关键统计属性（如词语分布、主题相关性）；
  - 满足差分隐私所需的噪声注入会导致严重的效用损失；
  - 缺乏对生成过程的细粒度控制，无法按需调整生成文本的属性（如情感、风格）。
- **整体含义**：本文旨在提出一种既能保证强隐私保护，又能生成高保真、高可控性的合成文本数据框架，从而赋能隐私安全场景下的语言模型研发。

### 2. 方法论
- **核心思想**：将差分隐私条件文本生成任务解构为“特征学习”与“条件生成”两个子任务，并通过强化学习增强生成器对条件的响应能力。
- **关键技术细节**：
  - **分层框架 ACTG（Attribute-Conditioned Text Generation）**：
    - **特征学习**：首先从原始文本中提取结构化的“属性”作为条件（采用丰富的表格模式），并利用差分隐私表格合成器生成符合隐私约束的合成属性。
    - **条件文本生成**：以合成属性为条件，对预训练语言模型进行差分隐私微调，使其能够根据属性生成对应文本。
    - 设计优势：明确将学习到的特征显式融入生成过程，简化了端到端的合成难度。
  - **后训练方法 Anchored RL (ARL)**：
    - **意图**：进一步提升 ACTG 生成器在条件控制下的指令遵循能力。
    - **机制**：引入强化学习来强化控制信号，同时为了防止奖励破解（即生成器产生高分但不符合真实条件的文本），使用基于Best-of-N采样得到的优质数据对生成器进行监督微调，作为策略更新的“锚点”。
  - **最终算法**：ACTG-ARL，融合分层生成与强化学习增强控制。

### 3. 实验设计
- **数据集/场景**：提供的摘要和元数据中未指明具体使用的数据集。文中提到通过系统性消融实验来寻找最佳配置，并对比了先前的工作。
- **基准与对比方法**：摘要提及与“prior work”进行比较，并以 MAUVE 分数作为生成质量的主要评估指标，结果显示较先前工作提升 +20% MAUVE。
- **评价方式**：主要关注生成文本的质量与保真度，以及条件生成的控制能力。

### 4. 资源与算力
- 提供的论文内容中**未明确说明**所使用的 GPU 型号、数量、训练时长等算力细节。

### 5. 实验数量与充分性
- **实验范围**：根据摘要的信息，论文至少完成了两类核心实验：
  - 通过系统性消融研究确定 ACTG 框架中最佳的特征配置（如特征选择、生成器组合）。
  - 与先前方法的对比实验，验证最终方案 ACTG-ARL 的有效性。
- **评估充分性**：在提供的信息中，实验设计表现出逻辑上的完整性（消融验证配置，对比证明提升），但无法从摘要推断出不同数据集覆盖、多维度指标（除 MAUVE 外）的全面性。从仅有的表述看，实验设计是客观且有对比价值的。

### 6. 主要结论与发现
- ACTG 的分层设计有效解决了差分隐私合成文本属性保留差、控制粗糙的问题。
- 引入 Anchored RL 可显著提高条件生成器对控制信号的响应精度，且通过 SFT 锚点机制防止了强化学习过程中常见的奖励破解。
- 融合方案 ACTG-ARL 在强差分隐私保证下，将合成文本质量指标 MAUVE 较先前工作提升了 20%，同时实现了更精细的生成控制。

### 7. 优点
- **架构创新**：将复杂任务解耦为特征合成与条件生成两个相对独立的模块，降低了训练难度，且每个模块均可独立进行差分隐私处理。
- **控制增强**：首次将基于锚点的强化学习引入差分隐私文本生成的后训练阶段，在提升可控性的同时保持了生成稳定性。
- **实用性**：方法生成的合成文本既可用于模型训练，也可作为下游评估的代理数据，且具有明确的隐私保障，落地价值较高。

### 8. 不足与局限
- **信息缺失无法评判的潜在局限**（基于提供的有限内容推测）：
  - 未提供具体的数据集和任务，难以判断方法的领域泛化性。
  - 差分隐私合成器的效用高度依赖表格特征的提取质量，若原始文本特征复杂或难以结构化，框架性能可能受限。
  - 强化学习后训练部分引入了额外的计算开销与超参数敏感性问题，摘要未讨论其训练稳定性。
  - 缺乏对极端隐私预算下（如 \(\epsilon\) 极小时）性能退化程度的讨论。

（完）
