---
title: "STEREO: A Two-Stage Framework for Adversarially Robust Concept Erasing from Text-to-Image Diffusion Models"
title_zh: STEREO：面向文本到图像扩散模型的对抗鲁棒概念擦除两阶段框架
authors: "Srivatsan, Koushik, Shamshad, Fahad, Naseer, Muzammal, Patel, Vishal M., Nandakumar, Karthik"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Srivatsan_STEREO_A_Two-Stage_Framework_for_Adversarially_Robust_Concept_Erasing_from_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 为文本到图像扩散模型开发鲁棒概念擦除方法，防御对抗性再生攻击，增强模型安全性
tldr: 针对文本到图像扩散模型中概念擦除后易被对抗攻击再生的问题，本文提出STERO框架。该框架通过两阶段训练，首先进行基础概念擦除，然后引入对抗训练和嵌入空间防御来增强鲁棒性。实验结果表明，STERO在有效阻止擦除概念被重新生成的同时，保持了良性概念的高质量生成，为安全内容过滤提供了更可靠的方案。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1811, \"height\": 701, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 865, \"height\": 375, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1787, \"height\": 863, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 863, \"height\": 446, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 867, \"height\": 300, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 860, \"height\": 294, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 835, \"height\": 380, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 864, \"height\": 334, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 167, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 862, \"height\": 165, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 865, \"height\": 308, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-srivatsan-stereo-a-two-stage-framework-for-adversarially-robust-concept-erasing-from-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 863, \"height\": 322, \"label\": \"Table\"}]"
motivation: 现有概念擦除方法易受对抗攻击导致擦除概念被再生，需鲁棒的防御方案。
method: 提出两阶段框架，结合对抗训练与嵌入空间防御，实现对抗鲁棒的概念擦除。
result: 框架在保持良性生成质量的同时，显著提高了对各类对抗攻击的抵抗力。
conclusion: STEREO为扩散模型安全内容过滤提供了实用且鲁棒的解决方案。
---

## Abstract
The rapid proliferation of large-scale text-to-image diffusion (T2ID) models has raised serious concerns about their potential misuse in generating harmful content. Although numerous methods have been proposed for erasing undesired concepts from T2ID models, they often provide a false sense of security; concept-erased models (CEMs) can still be manipulated via adversarial attacks to regenerate the erased concept. While a few robust concept erasure methods based on adversarial training have emerged recently, they compromise on utility (generation quality for benign concepts) to achieve robustness and/or remain vulnerable to advanced embedding space attacks. These limitations stem from the failure of robust CEMs to thoroughly search for blind spots in the embedding space. To bridge this gap, we propose STEREO, a novel two-stage framework that employs adversarial training as a first step rather than the only step for robust concept erasure. In the first stage, STEREO employs adversarial training as a vulnerability identification mechanism to search thoroughly enough. In the second robustly erase once stage, STEREO introduces an anchor-concept-based compositional objective to robustly erase the target concept in a single fine-tuning stage, while minimizing the degradation of model utility. We benchmark STEREO against seven state-of-the-art concept erasure methods, demonstrating its superior robustness to both white-box and black-box attacks, while largely preserving utility.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义  
- **研究背景**：文本到图像扩散模型（T2ID）在生成内容时存在传播有害视觉概念的风险（如暴力、裸体等），因此“概念擦除”技术被广泛研究，旨在从已训练好的模型中移除特定概念。  
- **核心问题**：当前的概念擦除方法大多只能提供表面的安全感——经过擦除的模型（CEM）仍可通过对抗性攻击（包括白盒与黑盒攻击、嵌入空间攻击）被诱导重新生成已被擦除的概念，存在严重的鲁棒性漏洞。  
- **整体含义**：为弥补这一安全盲区，论文提出 STEREO 框架，以两阶段策略系统性地提升概念擦除的对抗鲁棒性，同时力求保持良性概念的生成质量，为扩散模型的安全内容过滤提供真正可靠的方案。

## 2. 论文提出的方法论  
- **核心思想**：不再将对抗训练视为最终的唯一防御手段，而是将其作为两阶段流程中的“漏洞搜寻”步骤，之后再辅以一次性的鲁棒擦除，从而在对抗强健性与生成效用之间取得更好平衡。  
- **关键技术细节**：  
  - **第一阶段——对抗漏洞搜寻（Adversarial Training as Vulnerability Discovery）**：利用对抗训练在嵌入空间中广泛搜寻模型可能被利用的“盲区”，生成多种对抗性提示，使擦除目标概念的失效点充分暴露。  
  - **第二阶段——一次性鲁棒擦除（Robustly Erase Once）**：引入基于“锚概念”（anchor-concept）的组合目标函数，在不重复对抗训练的情况下，仅通过单轮微调就实现针对目标概念的鲁棒擦除，并最小化对模型原始生成能力的损害。  
  - **嵌入空间防御**：在擦除过程中不单单关注文本提示的直接映射，还从嵌入层面对抗潜在的分布外攻击，提升整体鲁棒性。  
- **算法流程**（文字说明）：  
  1. 对预训练 T2ID 模型进行对抗训练，收集使擦除失败的高危样本/嵌入表示。  
  2. 固定已识别的对抗薄弱点，构建包含目标概念、锚概念及良性保持项的复合损失函数。  
  3. 执行单阶段微调，约束模型既能抵御已发现的对抗攻击，又不过度偏离原始生成分布。

## 3. 实验设计  
- **数据集/场景**：论文未在摘要与元数据中明确列出使用的具体数据集，但概念擦除研究通常采用包含敏感概念（如“nudity”“violence”“gore”）的图文配对数据，并配合通用测试集（如 COCO、ImageNet 相关性评估）衡量模型生成效用。  
- **评估基准（Benchmark）**：  
  - **鲁棒性指标**：白盒攻击下的擦除成功率（对抗后再生率）、黑盒攻击及嵌入空间攻击下的防御能力。  
  - **效用指标**：良性概念生成质量（通常用 FID、CLIP score 等衡量）。  
- **对比方法**：共与 **七种当前最先进的概念擦除方法** 进行比较（具体名称未在提供内容中列出）。

## 4. 资源与算力  
- 现有提取内容（摘要与元数据）中 **未提及任何 GPU 型号、卡数、训练时长** 等算力相关信息。  
- 因此，无法给出具体的资源消耗估计。

## 5. 实验数量与充分性  
- **实验数量**：从文本可推断至少包含：  
  - 与 7 种基线方法的全面对比（覆盖多个攻击类型与防御场景）  
  - 两阶段设计的消融验证（否则无法证明第二阶段单独擦除的必要性）  
  - 定性与定量的生成质量评估  
- **充分性与公平性**：  
  - 对比方法数量较多（7 种 SOTA），涵盖不同技术路线，具备一定说服力。  
  - 同时评估白盒、黑盒及嵌入空间攻击，鲁棒性测试全面。  
  - 但提供的摘要中未给出具体的样本量、重复实验次数或统计检验，无法进一步判断统计稳健性。

## 6. 论文的主要结论与发现  
- STEREO 在保持良性概念生成质量（效用）的前提下，显著提升了对各类对抗攻击（白盒、黑盒、嵌入空间攻击）的防御能力。  
- 两阶段设计比单纯依靠对抗训练的方法更能兼顾鲁棒性与实用性，有效填补了现有擦除技术的盲区。  
- 所提框架可作为扩散模型安全部署的实用解决方案，防止有害内容被恶意恢复。

## 7. 优点  
- **两阶段解耦设计**：将对抗训练从“防御工具”重新定位为“探测工具”，减轻了对模型性能的副作用。  
- **锚概念嵌入防御**：利用组合目标一次性完成鲁棒擦除，避免多轮对抗微调的算力开销和灾难性遗忘。  
- **多维度攻击防御**：不仅对抗文本空间攻击，还针对嵌入空间盲区进行强化，鲁棒性更全面。  
- **效用保持显式优化**：在损失函数中显式加入良性概念保持项，使得防御增强不以牺牲正常生成为代价。

## 8. 不足与局限  
- **缺少细粒度实验细节**：从所提供内容看，数据集、具体评价指标数值、置信区间等均未披露，外部复现和严格对比存在困难。  
- **算力成本未知**：未说明对抗训练和擦除微调的实际计算消耗，难以评估其在大规模模型上的可扩展性。  
- **泛化边界未触及**：未讨论该方法在新型攻击（如更强的自适应攻击）或更大尺寸模型上的表现，安全性上限仍待考察。  
- **应用限制**：框架仍依赖对目标概念的明确定义和锚概念的选择，对模糊或复合敏感概念的擦除可能面临挑战。  
- **可能的偏差风险**：若锚概念选取不当，可能引入新的偏见或影响无关概念，效用损害下限未经充分分析。

（完）
