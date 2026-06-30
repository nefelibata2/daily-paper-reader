---
title: "The Hidden Cost of Modeling $\\text{P}(X)$: Membership Inference Attacks in Generative Text Classifiers"
title_zh: 建模P(X)的隐藏代价：生成式文本分类器中的成员推理攻击
authors: "Owais Makroo, Karan Gupta, Siva Rajesh Kasa, Sumegh Roychowdhury, Pattisapu Nikhil Priyatam, Santhosh Kumar Kasa, Sumit Negi"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=YHz6PybFqK"
tags: ["query:priv-sec"]
score: 9.0
evidence: 生成式文本分类器上的成员推理攻击
tldr: 本研究从理论和实验两方面证明，与判别式分类器相比，生成式分类器更容易遭受成员推理攻击，揭示了概率建模的隐藏隐私代价。基于五个数据集和多种攻击策略的评估确认了这一结论，提醒在部署生成式模型时需额外关注隐私风险。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 系统性比较生成式与判别式分类器在成员推理攻击下的差异，前人工作欠缺。
method: 提供理论动机和全面的实证评估，覆盖多种分类器和攻击策略。
result: 实验表明生成式分类器的隐私脆弱性显著更高。
conclusion: 生成式文本模型存在更高的隐私泄露风险，需重视隐私防护。
---

## Abstract
Membership Inference Attacks (MIAs) pose a critical privacy threat by enabling adversaries to determine whether a specific sample was included in a model's training dataset. Despite extensive research on MIAs, systematic comparisons between generative and discriminative classifiers remain limited. This work addresses this gap by first providing theoretical motivation for why generative classifiers exhibit heightened susceptibility to MIAs, then validating these insights through comprehensive empirical evaluation.
Our study encompasses discriminative, generative, and pseudo-generative text classifiers across varying training data volumes, evaluated on five benchmark datasets. Employing a diverse array of MIA strategies, we consistently demonstrate that fully generative classifiers which explicitly model the joint likelihood $P(X,Y)$ are most vulnerable to membership leakage. Furthermore, we observe that the canonical inference approach commonly used in generative classifiers significantly amplifies this privacy risk.
These findings reveal a fundamental utility-privacy trade-off inherent in classifier design, underscoring the critical need for caution when deploying generative classifiers in privacy-sensitive applications. Our results motivate future research directions in developing privacy-preserving generative classifiers that can maintain utility while mitigating membership inference vulnerabilities.

---

## 论文详细总结（自动生成）

# 论文详细总结

## 1. 论文的核心问题与整体含义
- **研究动机**：成员推理攻击（Membership Inference Attack, MIA）是机器学习模型面临的关键隐私威胁，攻击者可借此判断某样本是否存在于训练集中。已有大量研究探讨 MIA，但针对生成式（generative）与判别式（discriminative）分类器的系统性对比十分有限。
- **整体含义**：本文旨在阐明为何生成式文本分类器对 MIA 更具敏感性，并从理论上论证、从实验上验证这一现象，揭示出**显式建模联合概率分布 \(P(X,Y)\) 的“隐藏隐私代价”**。研究结果提醒：在隐私敏感场景部署生成式模型需额外谨慎，存在“效用-隐私”基本权衡。

## 2. 论文提出的方法论
- **核心思想**：比较判别式、生成式以及“伪生成式”文本分类器对成员推理攻击的脆弱性，分析生成式分类器中使用的典型推理方法如何放大隐私风险。
- **技术路线**（基于摘要信息的推理）：
  - 首先给出**理论动机**，说明为何生成式分类器（显式建模 \(P(X,Y)\)）会更易受 MIA 影响。
  - 通过**全面的实证评估**验证理论发现：在不同数据量、多个数据集、多种攻击策略下，衡量各类分类器的成员隐私泄露程度。
- 未提供具体公式或算法流程（原文缺失细节），但可归纳为：对比分类器的设计范式 → MIA 攻击实施 → 泄露程度量化。

## 3. 实验设计
- **数据集**：使用五个基准数据集（名称未列出）。
- **评估场景**：涵盖不同训练数据量，考察数据规模对 MIA 脆弱性的影响。
- **对比方法**：
  - 分类器类型：判别式、生成式、伪生成式（pseudo‑generative）文本分类器。
  - 攻击策略：多种 MIA 攻击策略（具体名称未提供）。
- **Benchmark**：比较各分类器在相同 MIA 攻击下的成员信息泄露程度，评估生成式分类器是否始终表现最差（即隐私最脆弱）。

## 4. 资源与算力
- 提供的文本中**未明确提及**计算资源（GPU 型号、数量、训练时长等）。由于只有元数据和摘要，无法推断其算力需求，需查看全文才可确认。

## 5. 实验数量与充分性
- 从摘要看，实验覆盖**五个数据集、变化训练数据量、多种分类器类型和多种 MIA 策略**，属于较丰富的实验设计。
- **消融实验**：文本未直接提及消融实验，但“变化数据量”和“多种攻击策略”可视为某种程度的变量控制。
- **客观性与公平性**：统一基准、多样化的攻击方法有助于保证对比的客观性；但缺少具体实现细节、超参数设置、随机种子等说明，无法完全判断公平性。
- **充分性**：在摘要层面，实验组合数量似乎合理，但具体实验组数、统计显著性等需全文验证。

## 6. 论文的主要结论与发现
- 完全生成式分类器（显式建模 \(P(X,Y)\)）**最易遭受成员泄露**。
- 生成式分类器中广泛使用的典型推断手段会**显著加剧隐私风险**。
- 分类器设计中存在“效用-隐私”权衡：生成式模型虽有优势（如可生成新样本），但付出更高的隐私代价。
- 建议在隐私敏感应用中谨慎部署生成式分类器，并激励未来开发**兼顾效用与隐私保护的生成式模型**。

## 7. 优点（亮点）
- **首次系统对比**生成式与判别式分类器在 MIA 下的差异，填补研究空白。
- **理论+实证双重视角**：不仅有理论动机说明，更辅以多数据集、多攻击策略的全面评估，增强结论可信度。
- **实践指导意义强**：明确警告生成式模型的隐私隐患，对产业界部署有直接参考价值。
- 实验覆盖面广：多种分类器、不同数据量、多样攻击，使结论具有普适性。

## 8. 不足与局限
- **细节缺失**：由于仅有摘要和元信息，论文的具体方法、攻击实施细节、模型架构、数据集名称均未呈现，无法评估其可复现性。
- **实验覆盖可能仍有限**：仅文本分类，是否适用于其他模态（图像、表格等）未知；攻击策略虽“多样”但未列出，可能遗漏最新攻击方法。
- **偏差风险**：未说明分类器训练的超参数是否统一调优，性能差异可能源于训练配置而非模型性质；未提供置信区间或显著性检验。
- **应用局限**：结论针对生成式文本分类器，通用性待验证；隐私保护方法未实验，留为未来工作。
- **算力与成本信息缺失**：无法判断方案在大规模场景下的可行性。

（完）
