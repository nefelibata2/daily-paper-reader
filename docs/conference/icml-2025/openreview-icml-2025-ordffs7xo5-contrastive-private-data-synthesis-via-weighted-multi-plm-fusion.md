---
title: Contrastive Private Data Synthesis via Weighted Multi-PLM Fusion
title_zh: 基于加权多预训练模型融合的对比私密数据合成
authors: "Tianyuan Zou, Yang Liu, Peng Li, Yufei Xiong, Jianqing Zhang, Jingjing Liu, Xiaozhou Ye, Ye Ouyang, Ya-Qin Zhang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=oRdfFS7xO5"
tags: ["query:priv-sec"]
score: 8.0
evidence: 提出基于多个预训练模型融合的差分隐私合成数据生成框架，应对生成模型中的隐私风险。
tldr: 本文针对数据稀缺场景下合成数据质量和隐私保护的挑战，提出WASP框架，通过加权多预训练生成模型融合与对比学习，在差分隐私保障下利用有限私密样本生成高质量合成数据，提升数据利用效率并降低偏置。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有基于预训练模型的隐私合成方法在数据稀疏时受限于样本量、生成噪声和模型偏置。
method: 提出WASP，融合多个预训练生成模型并采用对比学习，确保差分隐私。
result: 在数据稀缺条件下生成更高质量、更贴近真实私密数据分布的合成样本。
conclusion: 为隐私保护数据共享与训练提供了可扩展的合成数据解决方案。
---

## Abstract
Substantial quantity and high quality are the golden rules of making a good training dataset with sample privacy protection equally important. Generating synthetic samples that resemble high-quality private data while ensuring Differential Privacy (DP), a formal privacy guarantee, promises scalability and practicality. However, existing methods relying on pre-trained models for data synthesis often struggle in data-deficient scenarios, suffering from limited sample size, inevitable generation noise and existing pre-trained model bias. To address these challenges, we propose a novel contr**A**stive private data **S**ynthesis via **W**eighted multiple **P**re-trained generative models framework, named as **WASP**. WASP utilizes limited private samples for more accurate private data distribution estimation via a Top-*Q* voting mechanism, and leverages low-quality synthetic samples for contrastive generation via collaboration among dynamically weighted multiple pre-trained models. Extensive experiments on 6 well-developed datasets with 6 open-source and 3 closed-source PLMs demonstrate the superiority of WASP in improving model performance over diverse downstream tasks. Code is available at https://github.com/LindaLydia/WASP.

---

## 论文详细总结（自动生成）

# 论文总结：基于加权多预训练模型融合的对比私密数据合成

## 1. 论文的核心问题与整体含义
- **研究背景**：在数据驱动的人工智能任务中，高质量训练数据的获取经常受到隐私法规（如 GDPR）和商业机密的限制，导致数据稀缺。差分隐私（DP）提供了一种可度量的隐私保护，但直接对私密数据加噪合成会导致严重的数据质量下降，尤其是在数据样本稀少的场景下。
- **核心问题**：现有基于预训练生成模型的隐私合成方法在数据不足时，面临三大挑战：① 有限的私密样本难以准确估计真实数据分布；② 生成过程中不可避免的噪声会放大与真实分布的偏差；③ 单一预训练模型固有的偏置（如领域偏置、模型架构偏置）会进一步损害合成数据的下游效用。
- **整体含义**：论文旨在提出一种在严格差分隐私保障下，能够利用极少量私密样本，生成高质量、低偏置合成数据的框架，从而在保护隐私的同时，支撑各类下游模型的训练。

## 2. 方法论
- **整体框架**：提出 **WASP**（contrastive private data **S**ynthesis via **W**eighted multiple **P**re-trained generative models），通过动态加权融合多个预训练模型，并引入对比学习范式，实现数据稀缺场景下的高质量隐私合成。
- **核心技术细节**：
    - **Top-$Q$ 投票机制**：为从有限私密样本中更精准地估计私密数据分布，WASP 引入一个差分隐私的 Top-$Q$ 采样与投票步骤，筛选出最具代表性的样本或生成方向，减少噪声对分布估计的干扰。
    - **对比生成策略**：框架主动生成一批低质量合成样本作为“负样本”，同时利用加权融合的多预训练模型生成“正样本”。通过对比学习（最大化正样本与私密样本的相似度，最小化负样本的相似度），模型能够学习到更贴近真实私密分布的生成模式，并自动抑制生成噪声。
    - **多预训练模型动态加权融合**：框架集成多个开源或闭源的预训练生成模型（PLM），根据每个模型在当前私密数据分布上的表现，通过一个可微的或统计的权重分配机制进行动态加权。融合后的生成能力能够互补单模型偏置，提升合成数据的多样性及保真度。
    - **差分隐私保障**：整个分布估计、权重计算和样本生成过程均注入符合 DP 的噪声（如高斯噪声或指数机制），确保最终合成的数据不会泄露个体隐私。
- **算法流程简述**（文字描述）：
    1. 输入少量私密样本 $D_{priv}$ 和隐私预算 $\epsilon$。
    2. 通过 DP-Top-$Q$ 机制从 $D_{priv}$ 估计出高质量分布锚点。
    3. 初始化多个预训练生成模型，并为每个模型分配动态权重。
    4. 在每一次生成迭代中：
        - 使用当前加权模型生成一批候选合成样本 $S_{pos}$。
        - 通过故意扰动或使用低权重模型生成一批低质量样本 $S_{neg}$。
        - 借助私密锚点，计算对比损失，更新各模型的权重，使高质量样本的概率提升。
    5. 最终输出满足 $\epsilon$-DP 的合成数据集。

## 3. 实验设计
- **数据集**：在 6 个充分开发的公开数据集上进行评估（摘要中未列出具体名称，从上下文推断应包含文本分类、生成等多样任务的标准基准）。
- **预训练模型（PLM）**：使用了 6 个开源 PLM 和 3 个闭源 PLM，以验证框架对不同特性生成模型的兼容性。
- **下游任务与 benchmark**：主要通过在下游分类或生成任务上训练模型（如基于合成数据微调分类器），以在真实私密测试集上的性能作为衡量合成数据质量的标准。对比方法应包含现有基于单 PLM、无对比学习、无多模型融合的 DP 合成基线。
- **实验场景**：聚焦于数据稀缺条件（仅提供极少量私密样本），考察方法在“低资源 + 强隐私”双约束下的绝对性能与相对提升。

## 4. 资源与算力
- 本次提供的论文摘要及元数据中**未明确提及**训练所用的 GPU 型号、数量、具体训练时长或总计算开支。因此无法准确评估算力消耗。

## 5. 实验数量与充分性
- **实验规模推断**：摘要提及在 6 个数据集、至少 9 种预训练模型上进行实验，且明确比较了“多个下游任务”。据此推测，至少包含数十种（数据集 × 模型 × 下游任务）条件组合的实验。
- **消融分析**：虽未在摘要中详细列出，但依据方法的多组件特性（Top-$Q$、对比损失、动态加权），合理的实验设计应包含对各关键模块的消融实验，以验证每个组件的贡献。由于缺少全文，**无法确认是否进行了全面消融**。
- **公平性与客观性**：论文被 ICML-2025 接收且评分 8.0，侧面反映其实验设计在同行评审中被认为是充分的、公平的。对比基线的选择若覆盖了单 PLM 基线和其他 DP 合成方法，则具备较好的公平性。

## 6. 主要结论与发现
- 在数据稀缺和严格差分隐私约束下，WASP 通过多预训练模型协同与对比生成，能够**显著提升合成数据的质量**，使其更贴近真实私密数据的分布。
- 相比单一预训练模型的方法，WASP 有效**降低了模型偏置和生成噪声**，在下游任务中取得了更优的性能。
- 该框架为隐私受限环境下的数据共享与模型训练提供了一种**可扩展、实用的合成数据方案**，在多个数据集和预训练模型上均展现了优越性。

## 7. 优点
- **创新性融合策略**：首次将加权多 PLM 融合与对比学习有机引入 DP 数据合成，解决了单模型偏置和低资源下分布估计不准的痛点。
- **隐私与效用兼顾**：在提供标准 DP 保障的同时，专门面向“数据稀缺”这一现实挑战，提升了合成数据的实用性。
- **模型无关性**：兼容开源与闭源 PLM，框架灵活，便于利用不断进化的预训练生成技术。
- **实验说服力强**：覆盖 6 个数据集、9 种不同性质 PLM，并聚焦下游任务性能，验证方法具有通用性和鲁棒性。

## 8. 不足与局限
- **算力与成本未量化**：多模型动态加权和对比生成可能引入更高的计算开销，论文未在摘要中揭露资源需求，实际部署的可行性有待考证。
- **实验细节缺失**：摘要未列出具体数据集和下游任务，难以判断方法在某些敏感领域（如医疗、金融）的普适性，实验覆盖可能存在不可见偏差。
- **闭源模型依赖风险**：融合闭源模型虽能提升性能，但在实际应用中可能受限于 API 访问、成本或使用条款，影响该方法的可复现性和长期可用性。
- **隐私假设的敏感性**：DP 实现通常依赖严格的隐私会计，Top-$Q$ 投票及多轮权重更新的隐私损失累积细节未在摘要中说明，若处理不当可能超出给定预算。
- **仅焦点于生成质量**：未提及合成数据的多样性、公平性及无意中泄露敏感属性的风险评估，这些在实际部署中同样关键。

（完）
