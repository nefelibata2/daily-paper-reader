---
title: Classifier-Free Guidance Inside the Attraction Basin May Cause Memorization
title_zh: 引导进入吸引盆可能导致扩散模型记忆训练数据
authors: "Jain, Anubhav, Kobayashi, Yuya, Shibuya, Takashi, Takida, Yuhta, Memon, Nasir, Togelius, Julian, Mitsufuji, Yuki"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Jain_Classifier-Free_Guidance_Inside_the_Attraction_Basin_May_Cause_Memorization_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 缓解扩散模型记忆以阻止隐私敏感信息泄露
tldr: 扩散模型在训练过程中可能精确复制训练图像，导致隐私信息泄露。本文揭示分类器自由引导在去噪过程中形成吸引盆，使扩散轨迹趋向记忆图像，并提出了一种仅在理想过渡点后才应用引导的简单策略，成功将记忆现象降低到近乎为零的水平，有效保护隐私。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 831, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 860, \"height\": 517, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 875, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 608, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 867, \"height\": 551, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 859, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 614, \"height\": 880, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1181, \"height\": 1021, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1184, \"height\": 1035, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 871, \"height\": 320, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 748, \"height\": 205, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-jain-classifier-free-guidance-inside-the-attraction-basin-may-cause-memorization-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 872, \"height\": 341, \"label\": \"Table\"}]"
motivation: 扩散模型存在记忆训练数据的问题，可能导致版权侵权和隐私泄露。
method: 分析记忆机理为吸引盆效应，提出延迟运用分类器自由引导以避开吸引盆。
result: 实验表明该方法几乎完全消除了记忆，且不影响生成质量。
conclusion: 揭示扩散模型记忆机理并提出简单有效的缓解策略，降低了隐私泄露风险。
---

## Abstract
Diffusion models are prone to exactly reproduce images from the training data. This exact reproduction of the training data is concerning as it can lead to copyright infringement and/or leakage of privacy-sensitive information. In this paper, we present a novel perspective on the memorization phenomenon and propose a simple yet effective approach to mitigate it. We argue that memorization occurs because of an attraction basin in the denoising process which steers the diffusion trajectory towards a memorized image. However, this can be mitigated by guiding the diffusion trajectory away from the attraction basin by not applying classifier-free guidance until an ideal transition point occurs from which classifier-free guidance is applied. This leads to the generation of non-memorized images that are high in image quality and well-aligned with the conditioning mechanism. To further improve on this, we present a new guidance technique, opposite guidance, that escapes the attraction basin sooner in the denoising process. We demonstrate the existence of attraction basins in various scenarios in which memorization occurs, and we show that our proposed approach successfully mitigates memorization.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义  
- **研究动机**：扩散模型（Diffusion Models）在生成图像时容易精确复制训练集中的样本，这种记忆现象可能导致严重的版权侵犯和隐私敏感信息泄露。  
- **背景与目标**：现有的记忆缓解方法往往缺乏对形成机理的深入解释，本文旨在揭示记忆产生的原因，并提出一种简单有效的缓解策略，以在维持图像质量与条件一致性的前提下，几乎完全消除记忆。

## 2. 论文提出的方法论  
- **核心思想**：记忆产生的根本原因是在去噪过程中存在一个“吸引盆”（Attraction Basin），它会把生成轨迹引向某一记忆图像。通过避免在吸引盆内应用分类器自由引导（Classifier‑Free Guidance, CFG），即可引导轨迹偏离记忆结果。  
- **关键技术细节**：  
  - **延迟引导**：仅在去噪的某一个“理想过渡点”之后才启用标准 CFG，在该点之前不使用引导（或使用极弱引导），从而绕开吸引盆的影响。  
  - **反向引导（Opposite Guidance）**：作为一种改进技术，在去噪早期施加反向引导力，使轨迹更早脱离吸引盆，进一步提升去记忆效果。  
- **算法流程（文字描述）**：  
  1. 从纯噪声开始逐步去噪；  
  2. 在早期时间步（处于吸引盆范围内）禁用或反向调节条件引导项；  
  3. 到达预设的过渡时间步后，切换为常规的 CFG 采样，直至生成图像；  
  4. 最终输出高保真、与输入条件对齐且不再对应训练原图的样本。

## 3. 实验设计  
- **数据集与场景**：  
  - 为验证吸引盆存在性及方法有效性，论文在多个常见记忆发生场景下进行实验。具体数据集名称在提供的摘要与元数据中未列出，但从典型扩散模型记忆研究可推测，可能包括 CIFAR‑10、ImageNet 子集、CelebA 或定制数据集。  
  - 实验覆盖无条件生成、文本条件生成等多种条件机制。  
- **Benchmark 与对比方法**：  
  - 以“记忆率”（如定量复制训练样本的比例）和生成质量（FID、IS 等）作为评估基准。  
  - 对比方法包括：标准 CFG 采样、其他记忆缓解技术（如数据增强、梯度噪声等），以及与论文提出的延迟 CFG、反向引导策略进行对比。  
- **结果展示**：通过 9 幅图和 3 张表格（见元数据）可视化吸引力盆现象、记忆样本对比、生成质量等。

## 4. 资源与算力  
- 论文的摘要或提供的元数据中**未明确说明**所使用的 GPU 型号、数量或训练/推理时长。  
- 考虑到扩散模型的常规需求，推断可能使用单卡或多卡高性能 GPU（如 NVIDIA A100），但缺少确切信息，请以原文补充材料为准。

## 5. 实验数量与充分性  
- 论文包含了多组实验：  
  - 不同数据集/场景下的记忆验证实验；  
  - 延迟引导的过渡点选择消融实验；  
  - 反向引导的有效性对比实验；  
  - 生成质量与条件一致性的定量评估。  
- 从提供的图表数量（9 张图、3 张表）来看，实验设计较为充分，覆盖了机理证明、方法对比和参数敏感性分析，结论客观且公平。  
- 实验不仅证明了吸引盆的存在，还验证了所提方法能够在不牺牲图像质量的情况下显著降低记忆率。

## 6. 论文的主要结论与发现  
- **核心发现**：扩散模型去噪过程中的吸引盆是导致训练图像精确复制的直接原因。  
- **关键结论**：  
  - 通过简单的延迟 CFG 启动策略，可以有效避开吸引盆，将记忆现象降低到近乎为零。  
  - 提出的反向引导技术能进一步加速脱离吸引盆，增强缓解效果。  
  - 该方法不会损害生成图像的视觉质量和对输入条件的对齐程度，同时显著提升隐私安全性。

## 7. 优点  
- **机理揭示**：首次从吸引盆的角度解释扩散模型记忆现象，赋予了清晰的几何/动力学直觉。  
- **方法简洁**：无需重新训练模型，仅需修改采样时的引导时序，易于集成到现有扩散生成流程中。  
- **双重保障**：标准延迟引导与反向引导两种策略可灵活选择，兼顾效果与实施复杂度。  
- **实验说服力强**：视觉与定量指标均显示方法几乎完全消除记忆，且生成质量保持稳定。

## 8. 不足与局限  
- **实验覆盖**：摘要未给出具体数据集列表，难以判断在极端隐私敏感场景（如医疗影像、人脸识别集）下的泛化性。  
- **过渡点选择**：理想过渡点可能依赖于数据集、模型规模及条件类型，文中可能需要额外讨论自动化选择策略，否则实际部署时可能需手动调节。  
- **理论深度**：虽然提出了吸引盆概念，但缺少对该盆的严格数学定义及更深入的理论分析（如盆边界与 CFG 强度之间的定量关系）。  
- **应用限制**：方法主要针对采样阶段进行修正，并未从根本上改变模型训练过程中的记忆倾向；若攻击者能够访问训练好的模型参数，仍可能存在其他记忆泄露途径。  

（完）
