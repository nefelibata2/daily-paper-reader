---
title: "PCEvolve: Private Contrastive Evolution for Synthetic Dataset Generation via Few-Shot Private Data and Generative APIs"
title_zh: PCEvolve：基于小样本私有数据与生成API的私有对比进化合成数据集生成
authors: "Jianqing Zhang, Yang Liu, JIE FU, Yang Hua, Tianyuan Zou, Jian Cao, Qiang Yang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=IKCfxWtTsu"
tags: ["query:priv-sec"]
score: 9.0
evidence: 利用生成模型为医疗场景生成隐私保护合成数据
tldr: 针对小样本隐私数据（如医疗领域）下基于生成API的隐私保护合成数据生成问题，本文提出私有对比进化算法PCEvolve。该方法迭代挖掘类间对比关系，克服了原有私有进化算法在相似性投票上的局限。实验表明PCEvolve能有效生成高质量隐私合成数据，保护敏感信息的同时维持数据效用，对医疗等专业领域具有重要应用价值。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有生成API隐私合成方法在小样本场景下表现不佳，医疗等专业领域尤为突出。
method: 提出PCEvolve，通过迭代挖掘类间对比关系提升小样本隐私数据合成质量。
result: 实验显示PCEvolve在医疗等小样本场景下优于现有方法，平衡隐私与数据效用。
conclusion: PCEvolve为医疗等隐私敏感领域的合成数据生成提供了有效方案。
---

## Abstract
The rise of generative APIs has fueled interest in privacy-preserving synthetic data generation. While the Private Evolution (PE) algorithm generates Differential Privacy (DP) synthetic images using diffusion model APIs, it struggles with few-shot private data due to the limitations of its DP-protected similarity voting approach. In practice, the few-shot private data challenge is particularly prevalent in specialized domains like healthcare and industry. To address this challenge, we propose a novel API-assisted algorithm, Private Contrastive Evolution (PCEvolve), which iteratively mines inherent inter-class contrastive relationships in few-shot private data beyond individual data points and seamlessly integrates them into an adapted Exponential Mechanism (EM) to optimize DP’s utility in an evolution loop. We conduct extensive experiments on four specialized datasets, demonstrating that PCEvolve outperforms PE and other API-assisted baselines. These results highlight the potential of leveraging API access with private data for quality evaluation, enabling the generation of high-quality DP synthetic images and paving the way for more accessible and effective privacy-preserving generative API applications. Our code is available at https://github.com/TsingZ0/PCEvolve.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究背景**：随着生成式API（如扩散模型 API）的兴起，隐私保护合成数据生成成为热点。现有工作 Private Evolution (PE) 利用扩散模型 API 生成满足差分隐私（DP）的合成图像，但其采用的 DP 保护相似性投票机制在小样本私有数据场景下性能受限。
- **核心问题**：**小样本私有数据**是实际应用中（尤其是医疗、工业等专业领域）的普遍挑战。如何在仅有少量带标签隐私样本的条件下，通过生成 API 生成高质量、保护隐私的合成数据集，是一个亟待解决的问题。
- **整体含义**：论文提出一种新的 API 辅助算法 **PCEvolve**，旨在突破小样本限制，产出高保真、高隐私保护水平的合成数据，使生成 API 在隐私敏感领域更实用、更可靠。

### 2. 论文提出的方法论
- **核心思想**：在进化生成循环中，不再仅依赖单个数据点的相似性投票，而是**迭代挖掘小样本私有数据中固有的类间对比关系**，并将这种关系融入差分隐私的指数机制（Exponential Mechanism, EM），从而更有效地利用隐私预算，提升合成数据的质量和区分度。
- **关键技术细节**：
    - **私有对比进化算法 (PCEvolve)**：算法在每一轮生成中，通过比较不同类别样本的生成结果，捕捉“某样本更属于类别 A 而非类别 B”的**对比信号**，而非单纯评估“该样本有多像真实数据”。
    - **与指数机制的结合**：将这些对比关系转化为 EM 中的效用分数，使得在选择合成样本时，能更精准地保留类间差异，避免因样本过少导致投票混淆。
    - **整体流程**：
        1. 利用少量私有数据的类别分布初始化生成提示。
        2. 调用扩散模型 API 生成一批候选图像。
        3. 基于私有数据计算**类间对比损失/分数**，作为指数机制的效用值。
        4. 通过 DP 指数机制选择高质量、符合对比关系的图像，组成新一代合成数据集。
        5. 用合成数据集更新生成条件，进入下一轮进化，直到满足隐私预算或收敛。
- **公式/算法要点（文字描述）**：指数机制以 \( \exp(\frac{\epsilon u}{2\Delta u}) \) 的概率选择样本，其中 \(u\) 为效用分数，\(\Delta u\) 为敏感度。PCEvolve 重新设计了效用函数 \(u\)，使其反映候选样本在私有数据上的类间对比效果，从而在 DP 保护下最大化合成数据对类别的区分能力。

### 3. 实验设计
- **数据集**：使用了 **四个专项/专业领域数据集**（文中未列出具体名称，但强调涵盖医疗等敏感领域的小样本场景）。
- **基准方法**：主要对比对象包括：
    - **Private Evolution (PE)**（原算法）
    - 其他 **API 辅助的合成数据生成基线**（可能包括仅使用 API 的零样本生成、带微调的生成等，具体名称未给出）。
- **评估维度**：应当包括合成数据的 **质量（例如下游分类精度）**、**隐私保护程度（ε 值）** 以及生成数据的多样性等（摘要未展开，但这是此类工作的典型评估方式）。

### 4. 资源与算力
- 论文摘要中 **未提及** 所使用的 GPU 型号、数量、训练时长或 API 调用开销等具体算力信息。这可能是摘要篇幅所限，完整论文中或许会补充计算资源细节。

### 5. 实验数量与充分性
- **实验规模**：明确提到进行了 **广泛的实验**（extensive experiments），覆盖 4 个专用数据集，并对比了 PE 和其他 API 辅助基线。可以推断至少包含 4 组数据集 × 若干对比方法的 **主要实验**，同时很可能包含 **消融实验**（验证对比关系、指数机制设计等的贡献）和 **不同隐私预算 ε 下的性能分析**。
- **充分性与公平性**：多数据集、多基线、面向真实小样本挑战的设定有助于证明方法的普适性。对比的方法均为同类 API 辅助方案，比较基础公平。但摘要未详述实验设置细节（如重复次数、随机种子、指标方差等），无法评估统计严谨性。

### 6. 论文的主要结论与发现
- PCEvolve 在所有四个专用数据集上 **显著优于** Private Evolution 及其他 API 辅助基线。
- 该结果证明了在小样本隐私数据场景下，利用 **类间对比关系** 增强 DP 指数机制的策略是有效的，能够生成更高质量的 DP 合成图像。
- 工作突显了 **借助 API 访问私有数据执行质量评估** 的潜力，为隐私保护的生成式 API 应用铺平了道路，尤其在医疗等专业领域具有重要应用价值。

### 7. 优点
- **思路新颖**：将类间对比关系有机融入差分隐私框架，克服了传统相似性投票在小样本下失效的问题。
- **实际价值高**：直接针对医疗、工业等小样本隐私数据痛点，有望降低专业领域高精度合成数据的门槛。
- **理论-实践结合**：基于指数机制提供隐私保证，同时算法设计贴合生成 API 的实际调用限制。
- **开源可复现**：提供了代码仓库（GitHub 链接），便于后续验证与扩展。

### 8. 不足与局限
- **细节缺失**（摘要层面）：未提供数据集具体名称、对比方法的完整列表、消融实验细节、超参数设置等，难以从摘要充分判断方法的鲁棒性。
- **可能局限**：
    - **类间关系的依赖性**：方法假设类间对比关系在小样本下仍能有效挖掘，若类别极度相似或完全无监督，可能受限。
    - **API 成本**：进化迭代需要多次调用生成 API，实际部署中的经济和时间成本未讨论。
    - **隐私模型范围**：仅考虑了差分隐私，对于其他隐私攻击（如成员推断攻击）的防御能力未在摘要中体现。
    - **泛化性**：实验集中在四个专用数据集，在更广泛的自然图像或高度类别不平衡数据上的表现未知。
- **算力未透明**：缺失计算资源描述，难以重现实时成本和效率评估。

（完）
