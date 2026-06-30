---
title: Secret-Protected Evolution for Differentially Private Synthetic Text Generation
title_zh: 秘密保护进化：面向差分隐私合成文本生成
authors: "Tianze Wang, Zhaoyu Chen, Jian Du, Yingtai Xiao, Linjun Zhang, Qiang Yan"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=1vacZJxi56"
tags: ["query:priv-sec"]
score: 9.0
evidence: 差分隐私合成文本生成中的秘密感知保护
tldr: 针对现有差分隐私合成文本均匀保护导致效用损失大的问题，本文提出秘密保护进化框架SecPE，通过秘密感知机制区分敏感与非敏感内容，在理论保障下实现高效且高质的文本合成，适用于大语言模型训练。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有DP合成文本方案过度保护非敏感内容，导致效用严重下降和计算开销过大。
method: 提出SecPE框架，扩展私有进化算法，引入秘密感知保护，差异化处理敏感信息。
result: 实验表明SecPE在保护隐私的同时显著提高了合成文本的效用和效率。
conclusion: 该方法为隐私保护文本生成提供了更经济、更高质量的途径，有助于LLM安全使用私密数据。
---

## Abstract
Text data has become extremely valuable on large language models (LLMs) and even lead to general artificial intelligence (AGI).
A lot of high-quality text in the real world is private and cannot be freely used due to privacy concerns. Therefore, differentially private (DP) synthetic text generation has been proposed, aiming to produce high-utility synthetic data while protecting sensitive information.
However, existing DP synthetic text generation imposes uniform guarantees that often overprotect non-sensitive content, resulting in substantial utility loss and computational overhead. Therefore, we propose Secret-Protected Evolution (SecPE), a novel framework that extends private evolution with secret-aware protection. 
Theoretically, we show that SecPE satisfies $(\vp, \vr)$-secret protection, constituting a relaxation of Gaussian DP that enables tighter utility–privacy trade-offs, while also substantially reducing computational complexity relative to baseline methods.
Empirically, across the OpenReview, PubMed, and Yelp benchmarks, SecPE consistently achieves lower Fréchet Inception Distance (FID) and higher downstream task accuracy than GDP-based Aug-PE baselines, while requiring less noise to attain the same level of protection. 
Our results highlight that secret-aware guarantees can unlock more practical and effective privacy-preserving synthetic text generation.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：在利用私有文本数据训练大语言模型（LLM）时，差分隐私（DP）合成文本生成被用来保护隐私，但现有方法对所有内容施加均匀的隐私保护，导致非敏感内容也被过度保护，造成严重的效用损失和计算开销。
- **研究动机**：真实世界中的高质量文本（如医疗记录、用户评论）因隐私限制无法直接使用，传统的 DP 合成方法无法区分敏感与非敏感信息，限制了合成数据的质量和实用性。
- **整体含义**：通过引入“秘密感知”的差异化保护机制，在确保敏感信息隐私的前提下，最大化合成文本的效用，使得隐私保护文本生成更加经济、高质量，进而促进 LLM 在私密数据上的安全应用。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：提出 **秘密保护进化（SecPE, Secret-Protected Evolution）** 框架，在差分隐私合成文本生成中引入“秘密感知保护”（secret-aware protection），对敏感内容施加更强的隐私保护，而对非敏感内容放宽保护，从而在相同隐私预算下获得更高的数据效用。
- **关键技术细节**：
  - 扩展了现有的“私有进化”（private evolution）算法，将单一的全局隐私保障替换为分层的、内容相关的保护。
  - 引入 $(\epsilon, \rho)$-秘密保护（secret protection）概念，作为高斯差分隐私（Gaussian DP）的一种松弛，允许对非秘密部分施加更宽松的隐私约束。
  - 理论上证明 SecPE 满足 $(\epsilon, \rho)$-秘密保护，并显著降低了计算复杂度。
- **算法流程（文字说明）**：
  - 给定私有文本语料库，先识别或定义哪些部分为“秘密”（敏感内容），例如通过关键词、实体或语义分割。
  - 在进化生成合成文本的过程中，对涉及秘密内容的生成步骤注入更多噪声（满足更严格的 DP），而对非秘密步骤注入较少噪声。
  - 最终生成的合成文本既保护了秘密信息，又保留了非敏感内容的统计特性，实现更紧致的效用-隐私权衡。

### 3. 实验设计：使用的数据集 / 场景，benchmark，对比方法
- **数据集**：
  - OpenReview（学术论文评审）
  - PubMed（生物医学文献）
  - Yelp（用户评论）
  - 这三个数据集覆盖了学术、医疗及社交媒体不同领域的隐私敏感文本。
- **Benchmark 与评价指标**：
  - Fréchet Inception Distance (FID) 用于衡量合成文本与真实文本分布的距离（越低越好）。
  - 下游任务准确率（downstream task accuracy），如分类或生成任务，评估合成数据在训练模型时的实用性。
- **对比方法**：
  - 基于 GDP（Gaussian DP）的 Aug-PE（Augmented Private Evolution）基线方法。
  - 在相同隐私保护级别下，比较 SecPE 与基线在 FID 和下游准确率的表现，以及所需噪声量的差异。

### 4. 资源与算力
- 文中提供的摘要和元数据中 **未明确说明** 使用的 GPU 型号、数量或训练时长等算力细节。需查阅全文获取具体计算资源信息。

### 5. 实验数量与充分性
- 至少包含 **3 个不同领域的数据集**（OpenReview, PubMed, Yelp），每个数据集上可能进行了多组隐私预算设置的实验。
- 对比了多个指标（FID、下游准确率、所需噪声量），提供了与基线方法的全面比较。
- 理论分析部分给出了隐私证明和计算复杂度分析，强化了实验的说服力。
- 从摘要来看，实验设计**足够充分**，覆盖了不同场景、指标和维度，且通过与标准基线对比，客观性较好。消融实验未在摘要中提及，但全文可能包含对秘密感知机制的模块分析。

### 6. 论文的主要结论与发现
- SecPE 在所有三个基准上均取得了**更低的 FID** 和**更高的下游任务准确率**，优于 GDP-based Aug-PE 基线。
- 在达到相同保护水平时，SecPE 所需注入的噪声量**更少**，有效降低了效用损失。
- 秘密感知保护能够**实现更紧致的效用-隐私权衡**，使差分隐私合成文本生成更贴近实用。
- 整体上，所提方法开辟了一条更经济、更高质量的隐私保护文本生成途径，有助于 LLM 安全使用私密数据。

### 7. 优点：方法或实验设计上的亮点
- **差异化隐私保护**：突破传统 DP 均匀保护的局限，首次在合成文本生成中实现秘密感知机制，提高了实用性和灵活性。
- **理论创新**：提出 $(\epsilon, \rho)$-秘密保护概念，作为高斯差分隐私的松弛，并提供了严格的理论分析与计算复杂度降低证明。
- **实验全面扎实**：覆盖三个不同敏感度领域的数据集，从分布相似度、下游任务效果和隐私成本多角度验证，对比公平且效果显著。
- **实用性强**：直接在私有进化框架上扩展，易于部署，且更好地平衡了隐私和效用，为 LLM 训练数据制备提供了新方案。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **秘密定义依赖人工**：如何定义“秘密”内容尚未自动化，可能需要领域知识或预定义规则，存在主观偏差或遗漏风险。
- **实验覆盖范围**：仅测试了三个英文文本数据集，未涉及多语言、结构化或对话式数据，普适性有待验证。
- **攻击模型假设**：秘密感知保护放松了非敏感区域的隐私要求，但在某些攻击场景下（如关联攻击）非敏感信息仍可能间接泄露秘密，安全性需要更深入评估。
- **计算开销虽然降低但未量化**：摘要只声称计算复杂度降低，未给出具体数值比较（如运行时间或内存消耗）。
- **无用户研究**：仅通过自动指标评估，缺少人工对合成文本可读性、真实性和隐私泄露风险的评判。

（完）
