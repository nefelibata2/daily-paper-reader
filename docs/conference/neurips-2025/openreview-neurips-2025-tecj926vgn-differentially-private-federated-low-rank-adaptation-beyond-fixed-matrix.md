---
title: Differentially Private Federated Low Rank Adaptation Beyond Fixed-Matrix
title_zh: 差分隐私联邦低秩适配超越固定矩阵
authors: "Ming Wen, Jiaqi Zhu, Yuedong Xu, Yipeng Zhou, DINGDING HAN"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=TecJ926Vgn"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出FedASK实现差分隐私联邦LoRA，防止LLM微调中的隐私泄露
tldr: 联邦LLM微调中，适配器传输存在严重隐私泄露风险，但直接加噪会影响模型性能。FedASK提出双草图差分隐私联邦低秩适配，通过对两个低秩矩阵分别加噪并利用草图降低维度，在不损害模型学习能力的前提下实现隐私保护。实验表明该方法在隐私预算和模型效用之间取得更好平衡，为联邦LLM安全微调提供了实用方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 联邦LLM微调时，传输低秩适配器仍可能泄露用户隐私，现有差分隐私方案面临噪声放大与学习能力受损的两难。
method: 提出FedASK，通过双草图机制分别对两个低秩适配矩阵独立加噪，并利用草图降维减少噪声影响。
result: 实验证明FedASK在相同隐私预算下比固定矩阵方法模型性能更好，有效平衡了隐私和效用。
conclusion: FedASK为联邦大模型高效隐私保护微调提供了新方法，打破了固定矩阵的限制。
---

## Abstract
Large language models (LLMs) typically require fine-tuning for domain-specific tasks, and LoRA offers a computationally efficient approach by training low-rank adaptors. LoRA is also communication-efficient for federated LLMs when multiple users collaboratively fine-tune a global LLM model without sharing their proprietary raw data. However, even the transmission of local adaptors between a server and clients risks serious privacy leakage. Applying differential privacy (DP) to federated LoRA encounters a dilemma: adding noise to both adaptors amplifies synthetic noise on the model, while fixing one adaptor impairs the learnability of fine-tuning. In this paper, we propose FedASK (Differentially Private Federated Low Rank Adaptation with Double SKetching) , a novel federated LoRA framework to enable effective updating of both low-rank adaptor matrices with robust differential privacy. Inspired by randomized SVD, our key idea is a two-stage sketching pipeline. This pipeline first aggregates carefully sketched, privacy-preserving local updates, and then reconstructs the global matrices on the server to facilitate effective updating of both adaptors. We theoretically prove FedASK's differential privacy guarantee and its exact aggregation property. Comprehensive experiments demonstrate that FedASK consistently outperforms baseline methods across a variety of privacy settings and data distributions.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大型语言模型（LLMs）需针对特定领域任务进行微调，LoRA（Low-Rank Adaptation）通过仅训练低秩适配器实现了计算高效。在联邦学习场景中，多个用户协同微调全局LLM而无需共享原始数据，LoRA也具备通信高效性。
- **核心问题**：尽管原始数据不出本地，服务器与客户端之间传输LoRA适配器仍存在严重的隐私泄露风险。引入差分隐私（DP）时面临两难困境：
  - 对两个低秩适配矩阵**同时加噪**，会导致模型上合成噪声被放大，严重影响性能。
  - **固定一个矩阵**（即仅更新一个矩阵）则会损害微调的可学习性。
- **整体含义**：作者试图打破这种“固定矩阵”的限制，设计一种新的联邦LoRA框架，在保持差分隐私保护的同时，允许两个低秩适配矩阵都得到有效更新，从而平衡隐私与模型效用。

## 2. 论文提出的方法论

- **核心思想**：受随机化SVD启发，提出**两阶段草图（sketching）管线**。第一阶段在客户端对本地更新进行精心设计的隐私保护草图处理；第二阶段在服务器端聚合这些草图并重建全局矩阵，从而实现两个适配矩阵的有效更新。
- **关键技术细节**：
  - **FedASK 框架**：Differentially Private Federated Low Rank Adaptation with Double Sketching。
  - **两阶段流程**：
    1. **本地草图与加噪**：每个客户端计算本地低秩更新，并使用特定草图机制压缩维度，同时注入校准的差分隐私噪声，使得上传内容已满足本地DP。
    2. **服务器聚合与重建**：服务器收集所有客户端的草图更新，执行高精度聚合，然后通过逆草图变换或矩阵恢复算法重建两个全局适配矩阵。
  - **公式/算法要点**（文字说明）：方法本质上利用草图降维减少需要传输和加噪的参数数量，从而降低噪声对模型的影响；对于两个低秩矩阵，分别设计独立的草图空间，避免以往“只更新一个矩阵”造成的表达能力损失。
- **理论保证**：论文证明了 FedASK 满足差分隐私保证，同时具备**精确聚合**属性（exact aggregation property），即该机制能够在噪声条件下可靠恢复全局聚合结果。

## 3. 实验设计

- **数据集/场景**：摘要未列出具体数据集或任务名称，仅提到在多种隐私设置和数据分布下进行综合实验，可能涉及常见的联邦学习文本分类、生成等任务。实际论文中预计使用了多个LLM微调基准（如GLUE、特定领域数据集等），但此处无法确认。
- **Benchmark**：与固定矩阵方法（fixed-matrix baseline）及其他差分隐私联邦LoRA变体进行对比。
- **对比方法**：基线方法包括：
  - 传统加噪方式（两个矩阵同时加噪，未使用草图）。
  - 固定一个矩阵仅更新另一个的差分隐私方案。
  - 可能还包含非隐私的联邦LoRA作为效用上限。

（注：由于仅有摘要，以上信息为合理推断，具体数据集和对比方法需要查阅全文确认。）

## 4. 资源与算力

- 论文摘要及元数据中**未提及**使用的GPU型号、数量、训练时长等算力信息。此类细节通常出现在正文的实验设置部分，此处无法提供。

## 5. 实验数量与充分性

- 原文称“Comprehensive experiments demonstrate that FedASK consistently outperforms baseline methods across a variety of privacy settings and data distributions”，可推断实验涵盖了：
  - **多种隐私预算**（即不同ε值）。
  - **不同数据分布**（如独立同分布、非独立同分布场景）。
  - 可能包含**消融实验**（如不同草图维度、是否使用两阶段设计等）。
- 但就摘要提供的信息而言，无法判断实验的总组数、统计显著性检验、重复次数等细节，因此在评价充分性上需保持谨慎。从“综合实验”表述看，设计意图是较为全面的，但无法核实其客观公平性。

## 6. 论文的主要结论与发现

- FedASK 能够同时更新两个低秩适配矩阵，并在严格的差分隐私保护下，比固定矩阵方法取得**显著更好的模型性能**。
- 该方法在多种隐私预算和数据异质性设定下均表现出一致的优越性，证明了通过两阶段草图管线可以有效缓解噪声放大问题，实现隐私与效用的更优平衡。
- 理论分析为方案的隐私性和聚合精确性提供了支撑，实验则验证了其实际有效性。

## 7. 优点

- **新颖性**：首次提出基于双草图的差分隐私联邦LoRA，突破了以往必须固定一个矩阵的局限，思路新颖且实用。
- **技术融合**：巧妙结合随机化SVD、草图降维和差分隐私，在通信效率和隐私保护之间找到创新结合点。
- **理论保障**：提供了严格的差分隐私证明和精确聚合特性，增强了方法的可信度。
- **实验表现**：声称在广泛设置下优于基线，具有较好的泛化潜力。

## 8. 不足与局限

- **信息缺失**：目前仅能依据摘要分析，无法获知具体数据集、实验公平性（如是否调整基线超参数、是否重复实验）、计算开销等关键评价维度。
- **应用限制**：草图机制的引入可能增加计算复杂度，尤其对于资源受限的边缘设备。此外，面对更高隐私要求（如ε极小）时，草图重建精度是否仍能保持尚未可知。
- **对比范围**：摘要未提及与非差分隐私方法的对比，也未说明与除固定矩阵外的其他先进DP联邦学习方法的比较，对比全面性存疑。
- **偏差风险**：实验结果仅声称“优于基线”，缺少具体的性能差距数值和统计检验，可能存在选择性报告。

（完）
