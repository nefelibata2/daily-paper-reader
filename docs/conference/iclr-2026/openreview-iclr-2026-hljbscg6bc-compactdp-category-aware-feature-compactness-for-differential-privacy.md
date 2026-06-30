---
title: "CompactDP: Category-Aware Feature Compactness for Differential Privacy"
title_zh: CompactDP：基于类别感知特征紧凑性的差分隐私
authors: Shilin Zhang
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=hljBsCg6Bc"
tags: ["query:priv-sec"]
score: 7.0
evidence: 提出特征紧凑性方法以减少AI模型隐私泄露，可作为生成模型和医学AI的隐私保护技术。
tldr: 本文针对AI模型中的训练数据记忆和隐私泄露问题，提出一种无噪声的特征收缩方法C4P，通过使类别级特征流形紧凑化来降低个体样本影响，从而在保持模型效用的同时提升隐私保护水平。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 传统差分隐私方法如DP-SGD会降低模型效用，限制了在敏感领域的应用。
method: 提出类别级紧凑性隐私方法(C4P)，通过特征流形紧凑化减少隐私泄露，无需添加噪声。
result: 方法能有效降低成员推理攻击风险，同时保持模型性能。
conclusion: C4P为解决隐私泄露的根源提供了新思路，在敏感领域有广阔应用前景。
---

## Abstract
The rapid growth of AI models raises critical privacy concerns due to their tendency to memorize training data, making them vulnerable to extraction and membership inference attacks (MIAs). Traditional privacy-preserving methods like DP-SGD often degrade model utility, limiting their applicability in sensitive fields. We observe that compact class-wise feature manifold embeddings inherently reduce privacy risks by smoothing probability density functions (PDFs), which diminishes the influence of individual training samples and lowers memorization. Leveraging this insight, we propose  \textit{Class-wise Compactness for Privacy} (C4P) method, a noise-free feature contraction framework that directly addresses the root cause of privacy leakage, sparse, high-dimensional features, via feature contraction rather than relying on gradient noise. C4P can be trained independently and achieves a superior privacy-utility trade-off, with empirical privacy guarantee comparable to DP-SGD ($\epsilon=1$). C4P attains 95.82\% accuracy while limiting MIA risk comparable with DP-SGD ($\epsilon=1$) on CIFAR10. Notably, leveraging the optimized feature embedding, DP-SGD maintains robust model utility while preserving rigorous privacy guarantees across varying privacy budgets. Extensive experiments on FashionMNIST and MedicalMNIST further validate its favorable utility-privacy trade-off across diverse metrics.

---

## 论文详细总结（自动生成）

# 论文总结：CompactDP — 基于类别感知特征紧凑性的差分隐私

## 1. 核心问题与研究动机
- **背景**：AI 模型在训练过程中会记忆训练数据，从而易受提取攻击和成员推理攻击（MIA），泄露用户隐私。
- **痛点**：传统隐私保护方法（如 DP-SGD）通过注入噪声来提供差分隐私保证，但往往严重降低模型效用，限制了其在医疗等敏感领域的应用。
- **核心直觉**：作者观察到，紧凑的**类别级特征流形嵌入**可通过平滑概率密度函数（PDF）来减小个体训练样本的影响，从而从根源上降低记忆风险。由此，他们致力于设计一种无需噪声、直接压缩特征空间的方法来提升隐私性。

## 2. 方法论：C4P（Class-wise Compactness for Privacy）
- **核心思想**：不依赖梯度噪声，而是通过**特征收缩**强制同类样本的特征分布更紧凑，间接减少单个样本对决策边界的扰动，从而抑制隐私泄露。
- **技术路径**：
  - 提出 **C4P** 无噪声特征收缩框架，在训练过程中促使类别特征流形向紧凑形态演变。
  - 该方法不将噪声注入梯度，而是直接对特征嵌入施加紧凑性约束，从根源上解决稀疏高维特征带来的过度拟合与记忆问题。
- **训练与结合方式**：
  - C4P 可以**独立训练**，得到一个天然具有隐私保护能力的特征提取器。
  - 还可以将优化后的紧凑特征嵌入作为基础，进一步与 DP-SGD 结合，在变化的隐私预算下仍能保持高模型效用。

## 3. 实验设计
- **数据集**：CIFAR10、FashionMNIST、MedicalMNIST（医学影像数据集），覆盖自然图像、二分类服饰、医学多类等不同场景。
- **核心对比基准**：
  - 无隐私保护的原始模型。
  - DP-SGD（在不同隐私预算 ε 下的效果，尤其强调 ε = 1 的情况）。
- **评估指标**：
  - **效用**：分类准确率（如 CIFAR10 上达到 95.82%）。
  - **隐私**：成员推理攻击（MIA）风险，以及经验隐私保证是否与 DP-SGD（ε=1）相当。
  - 实验进一步展示了 C4P + DP-SGD 组合在不同隐私预算下的效用维持能力。

## 4. 资源与算力
- 摘要及元数据中**未提供**任何关于 GPU 型号、数量、训练时长或具体算力消耗的信息。这一点需要在阅读完整论文后补充。

## 5. 实验数量与充分性
- 根据摘要和元数据可推知的实验组：
  1. 多个数据集（至少 3 个：CIFAR10、FashionMNIST、MedicalMNIST）上的横向对比。
  2. 不同方法对比：无隐私、DP-SGD（可能多种 ε）、C4P 单独、C4P+DP-SGD 组合。
  3. 隐私评估维度：MIA 风险、经验隐私保证。
  4. 可能包含消融实验（例如是否验证紧凑度与隐私的相关性），但摘要未明确描述。
- 从已给信息看，实验覆盖了常见的隐私-效用权衡场景，且用多个数据集验证推广性，比较对象是领域主流方法 DP-SGD，**公平性方面无明显偏颇**。是否足够充分尚需论文正文中的详细消融、超参数敏感性和统计检验来确认。

## 6. 主要结论与发现
- **C4P 能在不引入噪声的情况下，实现与 DP-SGD（ε=1）相当的隐私保护水平**，同时维持较高分类准确率（CIFAR10 上 95.82%）。
- **特征紧凑性**是缓解训练数据记忆的有效手段，平滑概率密度函数可从根本上削弱个体样本对模型的影响。
- C4P 与 DP-SGD 相加后，即使在不同隐私预算下，模型也能保持稳健的效用，表明紧凑特征可作为差分隐私训练的优良“预正则化”底座。
- 该方法在多种数据集上（含医学数据）均取得有利的效用-隐私权衡，展现了在敏感领域的应用前景。

## 7. 方法亮点
- **无噪声隐私保护范式**：摆脱了对梯度噪声的依赖，避免效用损失，开辟了从特征几何角度解决隐私的新思路。
- **从根源解决问题**：直接操作特征流形的紧凑性，而非事后通过噪声掩盖，原理上更贴近防止过拟合与记忆的本质。
- **即插即用与兼容性**：可单独训练，也可作为前置步骤提升 DP-SGD 的性能，灵活性强。
- **在医学影像上验证**：关注真实敏感场景，增加了方法的实用说服力。

## 8. 不足与局限
- **信息不完整**：摘要未给出具体算法细节、损失函数形式、紧凑性约束的数学定义，难以判断其实施复杂度。
- **理论保证缺失**：文中提到“经验隐私保证与 DP-SGD 相当”，但未说明是否可提供像 DP 那样的严格理论保障（如 ε-δ 差分隐私证明）。若仅依靠经验攻击评估，可能存在攻击未覆盖全面时的安全性高估风险。
- **攻击覆盖有限**：摘要仅提及 MIA 风险，未涉及其他强攻击（如属性推理、模型逆向）或白盒攻击场景，安全性边界不明。
- **计算成本未知**：未描述训练代价，特征收缩是否会带来额外计算开销或收敛困难，难以评估落地可行性。
- **更复杂数据集的挑战**：仅在中小规模图像数据集上验证，对于大模型、大分辨率图像、文本等高维离散数据的适用性待探索。
- **与 DP-SGD 的深度比较局限**：虽声称性能与 DP-SGD（ε=1）相当，但未说明在该隐私水平下 DP-SGD 自身的精度下降程度，以及 C4P 是否在所有 ε 水平下都优于或不劣于 DP-SGD。

（完）
