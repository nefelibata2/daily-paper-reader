---
title: Convex Approximation of Two-Layer ReLU Networks for Hidden State Differential Privacy
title_zh: 两层ReLU网络的凸近似以实现隐藏状态差分隐私
authors: "Rob Romijnders, Antti Koskela"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=T9OQ094qR8"
tags: ["query:priv-sec"]
score: 8.0
evidence: 通过凸近似将隐藏状态差分隐私扩展到多层网络
tldr: 现有隐藏状态差分隐私分析局限于凸优化问题，难以应用于多层神经网络。本文提出将两层ReLU网络通过凸松弛转化为凸问题，从而能在隐藏状态威胁模型下实现差分隐私训练。实验表明，该方法在标准数据集上的隐私-效用权衡与DP-SGD相当，但提供了更强的隐私保障（仅暴露最终模型）。这项工作将差分隐私的理论保证扩展到了重要的深度学习模型，为诸如医学AI等敏感领域提供了新的隐私保护手段。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 隐藏状态差分隐私分析限于凸模型，无法直接用于多层网络。
method: 提出凸松弛技术，将两层ReLU网络转换为凸优化问题进行隐私训练。
result: 在隐私-效用权衡上达到与DP-SGD相近的性能。
conclusion: 为神经网络训练提供了一种新的差分隐私机制，拓展了隐蔽状态隐私保护的应用范围。
---

## Abstract
The hidden state threat model of differential privacy (DP) assumes that the adversary has access only to the final trained machine learning (ML) model, without seeing intermediate states during training. However, the current privacy analyses under this model are restricted to convex optimization problems, reducing their applicability to multi-layer neural networks, which are essential in modern deep learning applications. Notably, the most successful applications of the hidden state privacy analyses in classification tasks have only been for logistic regression models. We demonstrate that it is possible to privately train convex problems with privacy-utility trade-offs comparable to those of 2-layer ReLU networks trained with DP stochastic gradient descent (DP-SGD). This is achieved through a stochastic approximation of a dual formulation of the ReLU minimization problem, resulting in a strongly convex problem. This enables the use of existing hidden state privacy analyses and provides accurate privacy bounds also for the noisy cyclic mini-batch gradient descent (NoisyCGD) method with fixed disjoint mini-batches. Empirical results on benchmark classification  tasks demonstrate that NoisyCGD can achieve privacy-utility trade-offs on par with DP-SGD applied to 2-layer ReLU networks.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **差分隐私（DP）的隐藏状态威胁模型**：在该模型下，对手只能访问最终训练好的机器学习模型，而无法观测训练中间状态。这种方式理论上能提供更强的隐私保障，因为它只暴露最终结果。
- **当前局限**：目前隐藏状态DP的隐私分析仅适用于**凸优化问题**，难以直接用于多层神经网络。已有的成功应用基本局限在逻辑回归等凸模型上，无法覆盖现代深度学习核心的 **ReLU 多层网络**。
- **本文动机**：研究如何在隐藏状态威胁模型下，对**两层 ReLU 网络**实现差分隐私训练，使其获得与 DP-SGD（差分隐私随机梯度下降）相当的隐私-效用权衡，同时提供仅暴露最终模型的更强隐私保护。
- **整体含义**：这项工作将隐藏状态DP的理论保证**拓展到重要的深度学习架构**，为医疗AI等敏感领域的隐私保护提供新手段。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：把原本非凸的两层 ReLU 网络训练问题，通过**凸松弛（convex relaxation）**技术转化为一个**凸优化问题**。
- **具体路径**：
  - 从 ReLU 最小化问题的对偶形式（dual formulation）出发，构造其**随机近似**，得到一个**强凸问题**（strongly convex problem）。
  - 由于问题是强凸的，就可以直接套用现有的**隐藏状态差分隐私分析方法**，从而得到严格的隐私保证。
- **适用的算法**：生成的凸问题可以使用 **NoisyCGD**（带固定不相交 mini-batch 的噪声循环 mini-batch 梯度下降）进行训练，并且该方法同样可获得准确的隐私界。
- **重要特性**：整个过程在训练完毕后只释放最终模型参数，隐藏所有中间状态，符合隐藏状态威胁模型。

## 3. 实验设计：数据集、基准与方法对比

- **使用场景**：在**标准分类基准任务**上进行实验（摘要未列出具体数据集名称，可能涉及常用图像或表格分类数据集）。
- **对比方法**：
  - 本文方法：基于凸松弛 + NoisyCGD 的两层 ReLU 网络隐藏状态DP训练。
  - **对比对象**：通过 **DP-SGD** 训练的两层 ReLU 网络（DP-SGD 是当前神经网络差分隐私训练的主流方法，通常暴露中间梯度）。
- **评估指标**：隐私-效用权衡（privacy-utility trade-off），即在不同隐私预算下模型准确率等性能。
- **结果**：NoisyCGD 方法在 benchmark 上的隐私-效用权衡与 DP-SGD 相当，同时提供了更强的隐私模型（仅最终模型暴露）。

## 4. 资源与算力

- 摘要及元数据中**未提及** GPU 型号、数量、训练时长等算力信息。
- 因此无法判断该方法在大规模场景下的计算开销。

## 5. 实验数量与充分性

- 从现有信息来看，论文至少在若干**标准分类任务**上进行了实验，并与 DP-SGD 进行比较。
- 由于无法获取全文，无法确知：
  - 具体使用了多少个数据集；
  - 是否包含消融实验（如凸松弛程度的影响、不同隐私参数的灵敏度分析）；
  - 实验是否在不同随机种子下重复、是否统计方差等。
- 根据摘要给出的“comparable to those of 2-layer ReLU networks trained with DP-SGD”可推测实验设计较为直接、聚焦于核心对比，但细节尚待查证。从会议接收（NeurIPS-2025）的角度看，实验通常被认为是充分且公平的。

## 6. 论文的主要结论与发现

- **可行性结论**：可以在隐藏状态差分隐私威胁模型下训练两层 ReLU 网络，且隐私-效用权衡**与 DP-SGD 相当**。
- **方法论贡献**：提出了一种凸松弛策略，将非凸 ReLU 网络转化为凸问题，从而解锁了原本仅适用于凸模型的隐藏状态DP隐私分析方法。
- **隐私模型优势**：相比 DP-SGD 暴露中间更新，本文方法**仅释放最终模型**，提供了更符合真实部署场景的隐私保障。
- **应用展望**：该方法拓展了隐藏状态差分隐私在深度学习中的应用范围，尤其对医学 AI 等需要强隐私且要求高性能的领域有潜在价值。

## 7. 优点：方法或实验设计上的亮点

- **理论突破**：成功弥合了隐藏状态DP与多层网络之间的鸿沟，通过凸松弛这一经典工具找到了新用法。
- **隐私模型更有吸引力**：仅保护最终模型，不泄露训练动态，在实际部署中更具安全性和说服力。
- **实用性**：在标准基准上表现与主流 DP-SGD 相匹敌，说明方法并未因更强的隐私模型而显著牺牲效用。
- **对偶与随机近似**：利用对偶形式构造强凸问题，巧妙的思路可能为其他非凸网络的隐私分析提供灵感。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **网络深度限制**：目前方法仅针对**两层 ReLU 网络**，能否扩展到更深的网络（如 ResNet、Transformer）仍未知，通用性受限。
- **凸松弛的代价**：凸近似可能引入额外的偏差，在更复杂任务上效用损失可能增大，但摘要未量化这种偏差。
- **实验细节未知**：未提供具体数据集、超参数选择、鲁棒性分析（如不同数据分布、标签噪声等），难以全面评估方法的稳定性。
- **计算开销未明确**：NoisyCGD 与凸松弛的实际训练成本未知，可能比直接 DP-SGD 更高，限制了在大规模数据上的应用。
- **仅比较 DP-SGD**：未与其他先进的隐藏状态DP方法（如果存在）对比，对比基线较为单一。
- **威胁模型假设**：隐藏状态模型假设对手只能看到最终模型，现实中可能仍需考虑其他侧面信息泄漏，该方法仅覆盖这一特定威胁。

（完）
