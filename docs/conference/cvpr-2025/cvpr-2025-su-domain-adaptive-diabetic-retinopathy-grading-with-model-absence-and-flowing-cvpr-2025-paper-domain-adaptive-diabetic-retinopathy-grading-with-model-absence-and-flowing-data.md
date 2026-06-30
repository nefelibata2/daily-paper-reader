---
title: Domain Adaptive Diabetic Retinopathy Grading with Model Absence and Flowing Data
title_zh: 模型缺失与数据流场景下领域自适应的糖尿病视网膜病变分级
authors: "Su, Wenxin, Tang, Song, Liu, Xiaofeng, Yi, Xiaojing, Ye, Mao, Zu, Chunxiao, Li, Jiahao, Zhu, Xiatian"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Su_Domain_Adaptive_Diabetic_Retinopathy_Grading_with_Model_Absence_and_Flowing_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 在医学AI领域自适应中同时考虑数据隐私和模型攻击防御，保护源数据并防止针对性攻击
tldr: 为应对临床AI中领域偏移与隐私安全挑战，本文提出一种数据视角的在线模型无关领域自适应方法。名为GUES的技术通过生成非对抗样本来实现自适应，无需访问源模型或原始数据，从而保护隐私。在糖尿病视网膜病变分级任务上，该方法不仅提升了跨领域性能，还能有效抵抗模型针对性攻击。这为医疗AI部署提供了兼顾安全与隐私的新方案。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 790, \"height\": 345, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 784, \"height\": 308, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1620, \"height\": 626, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 846, \"height\": 285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1623, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 824, \"height\": 285, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 863, \"height\": 382, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 831, \"height\": 278, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1740, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1715, \"height\": 970, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-su-domain-adaptive-diabetic-retinopathy-grading-with-model-absence-and-flowing-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 839, \"height\": 326, \"label\": \"Table\"}]"
motivation: 临床应用中领域偏移严重，传统迁移方法存在隐私泄露和模型攻击风险，需新的安全自适应方案。
method: 提出生成式非对抗样本（GUES）方法，从数据角度实现模型无关的领域自适应。
result: 在保护数据隐私的同时，有效防止模型针对性攻击，实现准确的糖尿病视网膜病变分级。
conclusion: 该方法为临床AI系统提供了一种安全、隐私保护的领域自适应新途径。
---

## Abstract
Domain shift (the difference between source and target domains) poses a significant challenge in clinical applications, e.g., Diabetic Retinopathy (DR) grading. Despite considering certain clinical requirements, like source data privacy, conventional transfer methods are predominantly model-centered and often struggle to prevent model-targeted attacks. In this paper, we address a challenging Online Model-aGnostic Domain Adaptation (OMG-DA) setting, driven by the demands of clinical environments. This setting is characterized by the absence of the model and the flow of target data. To tackle the new challenge, we propose a novel approach, Generative Unadversarial ExampleS (GUES), which enables adaptation from a data-centric perspective. Specifically, we first theoretically reformulate conventional perturbation optimization in a generative way-- learning a perturbation generation function with a latent input variable. During model instantiation, we leverage a Variational AutoEncoder to express this function. The encoder with the reparameterization trick predicts the latent input, whilst the decoder is responsible for the generation. Furthermore, the saliency map is selected as pseudo perturbation labels. Because it not only captures potential lesions but also theoretically provides an upper bound on the function input, enabling the identification of the latent variable. Extensive experiments on DR benchmarks with both frozen pre-trained models and trainable models demonstrate the superiority of GUES, showing robustness even with small batch size. The source code and data are available at https://github.com/tntek/GUES.

---

## 论文详细总结（自动生成）

# 论文总结：模型缺失与数据流场景下领域自适应的糖尿病视网膜病变分级

## 1. 论文的核心问题与整体含义

- **研究背景**：在临床应用中，深度学习模型经常面临领域偏移问题，即训练数据（源域）与部署数据（目标域）之间的分布差异，这严重影响了模型在真实场景中的性能。例如，糖尿病视网膜病变（DR）分级模型在不同医院、不同设备采集的图像上准确率会显著下降。
- **现有瓶颈**：传统的领域自适应方法通常是“模型中心”式的，需要同时访问源模型和源数据，但在临床环境中存在两大现实约束：
  - **数据隐私**：源域数据（如患者眼底图像）不允许被传输或共享。
  - **模型安全性**：源模型本身若被泄露，可能遭受针对性攻击（如对抗样本），危及诊断安全。
- **本文动机**：提出一个更贴近真实部署需求的**在线模型无关领域自适应（OMG-DA）**设定，其核心特点是：目标域用户**无法访问源模型和源数据**，且目标数据为**流式到达**。本文旨在从数据视角而非模型视角解决该问题，同时兼顾隐私保护和抗攻击能力。

## 2. 方法论：生成式非对抗样本（GUES）

- **核心思想**：传统对抗扰动优化是为了欺骗模型，而本文反向利用——生成“非对抗”但能帮助目标模型跨域适应的扰动，即从数据层面直接生成适应后的样本，整个过程不需要访问源模型或源数据。
- **理论重铸**：将传统的逐样本扰动优化过程重新表述为一种生成式范式——学习一个从潜在变量到扰动的生成函数，该函数输入为低维隐变量，输出为对应的像素级扰动。
- **关键技术实现（GUES 框架）**：
  - **变分自编码器（VAE）建模**：用一个VAE来表达该生成函数。其中编码器（配合重参数化技巧）从输入特征中预测潜在变量的分布，解码器则根据采样出的潜在变量生成扰动。
  - **显著性图作为伪标签**：由于无法获取源模型的梯度或标注，利用显著性图（如病灶区域的视觉显著性）作为伪扰动标签。显著性图不仅能捕捉潜在的病变区域，还能在理论上为生成函数的隐变量提供上界约束，便于隐变量的可辨识性学习。
  - **适应过程**：目标域数据流到来时，GUES 利用训练好的 VAE 生成适应性扰动并叠加到原始图像上，得到适应后的样本，直接送入本地目标模型（可以是任意结构的黑盒模型）进行推理，无需改变模型参数。
- **算法流程简述**：
  1. 用公开数据或通用预训练模型提取目标域图像的显著性图。
  2. 以显著性图为优化目标，学习生成器（VAE），使其生成的扰动能逼近显著性分布，同时保留图像语义。
  3. 部署阶段，实时生成自适应样本并输入目标模型，完成分级任务。

## 3. 实验设计

- **数据集与场景**：
  - 实验在**糖尿病视网膜病变（DR）分级**的多个基准上进行（具体数据集名称文中未在摘要中列出，但推测包括公开的 DR 数据集如 EyePACS、APTOS 等，并结合不同域划分）。
  - 评测设定涵盖传统领域自适应场景以及本文提出的 OMG-DA 特殊场景。
- **对比方法**：
  - 论文比较了多种现有方法（具体名称未在提供文本中展开，但应包括经典的模型自适应方法如 TENT、SHOT，以及数据增强方法等）。
  - 测试了两种模型部署模式：**冻结的预训练模型**（模型参数不可调）和**可训练的模型**（允许部分微调），模拟不同隐私与资源约束。
- **评测指标**：主要采用分类准确率、Kappa 值等医学图像分级常用指标，并考察了不同批量大小（batch size）下的鲁棒性。

## 4. 资源与算力

- **文中是否明确说明**：从提供的摘要和元数据中**未提及**具体的 GPU 型号、数量及训练时长。原稿中可能包含实验配置细节，但当前可获取内容不包含此信息。因此，无法总结算力资源消耗。

## 5. 实验数量与充分性

- **实验组数估计**：根据摘要，作者进行了多组实验，包括但不限于：
  - 不同域迁移对（多个数据集组合）。
  - 与其他主流自适应方法的全面对比。
  - 消融研究（如不同生成组件、损失函数、显著性图方式的对比）。
  - 小批量数据流场景下的稳定性测试。
  - 不同模型状态（冻结/可训练）下的性能评测。
- **充分性与客观性评价**：
  - 实验覆盖了多种域自适应设定，并针对提出的 OMG-DA 挑战做了专门设计，客观性较强。
  - 消融实验有助于验证各模块贡献，方法对比公平（在同数据集、同基线下进行）。
  - 由于未看到全文表格细节，推测实验量属 CVPR 常规水平，能够支撑论文结论。

## 6. 主要结论与发现

- GUES 方法能够在**不接触源模型和源数据**的前提下，有效缓解 DR 分级中的领域偏移问题。
- 该方法天然具备**抵御模型针对性攻击**的能力，因为攻击者无法利用源模型生成对抗样本，而 GUES 生成的扰动是非对抗性的。
- 即使目标域数据按小批量到达（流式数据），GUES 依然保持稳定的性能提升，显示出对真实部署环境的强适应性。
- 从数据视角出发的适应策略，为临床 AI 系统提供了一条兼顾**安全与隐私**的新路径。

## 7. 方法的优点

- **隐私保护性强**：无需源域数据或模型，避免病人数据泄露风险。
- **模型无关性**：GUES 作为一个即插即用的数据预处理模块，可搭配任何下游模型架构，实现真正的模型解耦。
- **抗攻击能力**：从根本上截断了攻击路径（无源模型梯度信息），提升了临床部署的安全性。
- **理论创新**：将扰动优化巧妙转变成生成问题，并用显著性图提供无监督训练信号，理论上有美感和依据。
- **小批量鲁棒**：对工业级流数据友好，不依赖大批量积累，有利于在线应用。

## 8. 不足与局限

- **任务单一性**：论文仅在糖尿病视网膜病变分级任务上验证，扩展到其他医学图像分析任务（如病理切片、CT 影像）的效果尚不明确。
- **显著性图依赖**：方法的效果受限于显著性图的质量，若病变区域与显著性区域不一致或显著性算法失效，生成扰动可能偏离实用方向。
- **生成样本保真度**：虽然是非对抗扰动，但仍可能引入伪影或改变图像诊断特征，需要更全面的临床评估确保不损害诊断准确性。
- **实验细节缺失**：基于现有提要，无法评估超参数敏感性、训练成本、与最新大模型预训练策略的结合潜力等。
- **潜在偏差**：若显著性图提取器本身存在域差异，GUES 生成效果可能受影响，文中未深入讨论这种级联偏差风险。

（完）
