---
title: "Preventing Privacy Leakage in Vision-Language Models: A Secure Framework for Large-Scale Image Classification"
title_zh: 防止视觉语言模型隐私泄漏：面向大规模图像分类的安全框架
authors: "Meng Wei, Zhongnian Li, Shi Xu, Peng Ying, Xinzheng Xu"
date: 2025-09-10
pdf: "https://openreview.net/pdf?id=UN31lBlltd"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出框架防止大视觉语言模型在生成标签时泄漏隐私，特别针对医疗状况等敏感数据
tldr: 大视觉语言模型在生成伪标签时可能意外访问医学状况等敏感信息，造成隐私泄漏。本文提出一个融合隐私标签集与随机标签集的安全标注框架，由人类标注者判断合并标签集是否包含真实标签，仅在不包含时才调用LVLM，从而避免模型接触敏感数据。该方法在图像分类任务上平衡了隐私保护与标注效率，为医疗AI等敏感领域的生成模型应用提供了实用隐私保护方案。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 视觉语言模型在伪标签生成过程中可能读取并泄漏数据中隐含的医疗状况等敏感信息，存在隐私风险。
method: 构建隐私标签集与随机标签集的混合集合，由人类标注者先行判断是否包含真实标签，仅在必要时使用LVLM。
result: 在保持分类精度的同时，有效阻断模型访问敏感属性，降低了在医学图像等应用中隐私泄漏的可能性。
conclusion: 该框架为大规模图像分类中的隐私保护提供了轻量级方案，有助于推动视觉语言模型在敏感领域的合规部署。
---

## Abstract
Recently, large vision-language models (LVLMs) have demonstrated strong performance in generating pseudo-labels for diverse downstream tasks. However, during annotation or label generation, these models may inadvertently access sensitive information contained in the data (e.g., medical conditions, smoking habits), thereby creating potential risks of individual privacy leakage. To mitigate this challenge, we propose a novel framework that prevents LVLMs from accessing data associated with sensitive information. Specifically, our framework integrates a privacy label set with a randomized label set. Human annotators first determine whether the merged label set contains the ground-truth label; only when it does not, the LVLMs are employed to generate a pseudo-label. This mechanism ensures that LVLMs never directly access samples associated with sensitive information during annotation, while the inclusion of the randomized label set provides partial supervision for non-privacy samples. Moreover, we introduce a risk-consistent estimator that enables effective learning from LVLM-generated pseudo-labels under the exclusion of sensitive data. Extensive experiments on benchmark datasets demonstrate the superiority of our approach over state-of-the-art methods, effectively safeguarding sensitive label information while maintaining competitive model performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大视觉语言模型（LVLMs）在生成伪标签时，可能无意中从图像数据中读取并暴露与隐私密切相关的敏感信息（如医学病症、吸烟习惯等），导致个人隐私泄露风险。
- **研究动机**：随着 LVLMs 在图像分类等任务中广泛用于自动标注，如何在利用其强大表征能力的同时，阻断模型对敏感属性的直接访问，成为安全部署的关键挑战。
- **整体含义**：提出一种“不接触敏感数据即可获得高质量伪标签”的安全标注框架，旨在推动 LVLMs 在医疗 AI 等敏感领域的合规应用，并为隐私保护下的弱监督学习提供新思路。

### 2. 论文提出的方法论
- **核心思想**：通过人类标注者先对混合标签集进行“是否包含真实标签”的判断，对包含真实标签的敏感样本直接使用人类判断结果，而仅在不包含真实标签时调用 LVLM 生成伪标签，从而在机制上杜绝 LVLM 接触任何与敏感属性关联的图像。
- **关键技术细节**：
  - **隐私标签集与随机标签集**：构建两类标签集合，一类是与敏感属性关联的隐私标签集，另一类是随机生成的通用标签集。两者合并后供人类标注者快速筛查。
  - **人机协作的判断流程**：
    1. 对于每张图像，向人类标注者展示由隐私标签和随机标签组成的合并标签集。
    2. 人类标注者只需要判断该合并标签集中是否包含该图像的真实标签。
    3. 若**包含真实标签**，说明该图像可能涉及敏感属性，此时**不调用 LVLM**，直接用人类判断结果作为监督信号（部分监督）。
    4. 若**不包含真实标签**，说明该图像不涉及被选中的隐私标签，此时安全地将图像送入 LVLM 生成伪标签。
  - **风险一致估计器（risk‑consistent estimator）**：在训练阶段，针对部分由 LVLM 生成的伪标签和部分由人类标注的真实标签（非敏感样本），设计了一种能够消除因排除敏感数据而引入的选择偏差的统计估计方法，确保模型仍能从混合监督信号中有效学习。
- **流程简化示意**（文字描述）：
  ```
  原始图像 → 合并标签集（隐私+随机）→ 人类判断是否包含真标签？
                  ├─ 是 → 使用人类标签（LVLM 不接触图像）
                  └─ 否 → 调用 LVLM 生成伪标签 → 加入训练集
  → 使用风险一致估计器进行模型训练
  ```

### 3. 实验设计
- **数据集/场景**：论文元数据与摘要中提到进行了“大量基准数据集实验”和“医学图像等应用”，但未列出具体数据集名称。推测可能涉及常见图像分类基准（如 ImageNet 子集）、医疗影像数据集（如皮肤镜、视网膜图像）等包含敏感属性的场景。
- **Benchmark 与对比方法**：与“最先进方法（state‑of‑the‑art methods）”进行对比，但未指明具体方法名称。可能包括常规 LVLM 生成伪标签的弱监督方法、基于差分隐私的保护方案、或仅使用人类标注的完全监督基线。
- **评估指标**：应涵盖分类精度（如准确率）、隐私泄露度量（如敏感属性推断成功率）以及标注效率（人工时间成本）。

### 4. 资源与算力
- **未明确说明**：提供的摘要及元数据中没有任何关于 GPU 型号、数量、训练时长或内存消耗的量化信息。论文实际全文可能包含相关细节，但在此提取文本中无法确认。

### 5. 实验数量与充分性
- **实验数量**：摘要提到“Extensive experiments”，暗示进行了多组实验，包括不同数据集、不同隐私保护强度、消融实验（如移除随机标签集或风险一致估计器）等，但具体数量未知。
- **充分性与客观性**：
  - 从方法论看，实验应至少涵盖**不同隐私标签规模、不同数据分布、不同人类判断准确率**的敏感性分析，才能说明框架的鲁棒性。
  - 现有信息只能说明论文试图通过“与最先进方法对比”证明其优越性，但无法判断实验是否覆盖了足够的场景、是否控制了人类标注者的主观偏差、是否采用了公平的评估协议。

### 6. 论文的主要结论与发现
- 所提框架能够在**保持图像分类精度**（与无隐私保护的 LVLM 标注效果相当）的同时，**有效阻断模型对敏感属性的访问**，显著降低隐私泄露风险。
- 通过风险一致估计器，模型可以在排除敏感样本的残缺数据下，仍充分利用 LVLM 生成的非敏感伪标签，实现轻量级且稳健的学习。
- 该方法为大规模图像分类中隐私保护提供了实用、可部署的蓝图，尤其适合医疗等需严格管控敏感信息的领域。

### 7. 优点
- **机制层面隔离**：通过人机协同的“预判‑屏蔽”设计，从数据源头阻止 LVLM 接触敏感图像，而非事后修补，隐私保障更为根本。
- **兼顾精度与隐私**：不牺牲模型性能，在标准分类任务上仍具竞争力，避免了隐私保护常伴随的效用急剧下降。
- **灵活的部分监督**：引入随机标签集，使得人类标注者的判断任务极其简单（只需回答“是否包含”），降低人工负担，而随机标签同时为普通样本提供弱监督，巧妙平衡了效率与效果。
- **理论支撑**：风险一致估计器的提出为缺失非随机子集的弱监督学习提供了统计一致性保证。

### 8. 不足与局限
- **缺乏实施细节的公开**：目前公开的摘要和元数据尚未披露具体数据集、对比方法名称、超参数设置等，难以独立复现或全面评估其有效性。
- **对人类标注的依赖性**：仍需要人工判断合并标签集中是否包含真实标签，当隐私标签集规模较大或图像内容模糊时，人类标注的成本和一致性可能成为瓶颈。
- **隐私标签集的定义先验**：框架需要预先定义哪些标签属于“隐私敏感”范畴，若定义不完整，敏感属性可能从非隐私标签中泄露（例如通过关联推断）。
- **对 LVLM 能力的受限利用**：对于被判定为“包含真实标签”的图像，完全放弃 LVLM 的标注，可能浪费其在非敏感维度上的信息，尽管风险一致估计器试图补偿，但仍可能丢失细粒度特征。
- **扩展性未知**：实验是否在大型（如百万级）图像集上进行尚不清晰；随机标签集的设计和人类判断在超大规模场景下的可行性有待验证。

（完）
