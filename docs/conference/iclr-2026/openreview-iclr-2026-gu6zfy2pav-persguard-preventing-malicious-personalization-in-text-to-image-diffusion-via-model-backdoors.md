---
title: "PersGuard: Preventing Malicious Personalization in Text-to-Image Diffusion via Model Backdoors"
title_zh: PersGuard：通过模型后门防止文本到图像扩散中的恶意个性化
authors: "Xinwei Liu, Xiaojun Jia, Yuan Xun, Hua Zhang, Xiaochun Cao"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=gU6ZfY2pav"
tags: ["query:priv-sec"]
score: 9.0
evidence: 防止扩散模型的未授权个性化，以缓解隐私和版权风险。
tldr: 文本到图像扩散模型的个性化能力带来隐私和版权风险。本文提出PersGuard框架，通过嵌入模型后门，在用户对受保护图像进行微调时触发保护行为，从而阻止未经授权的个性化。实验表明该方法比对抗扰动更鲁棒，有效防止隐私泄露。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 个性化扩散模型可能泄露隐私和侵犯版权，现有对抗扰动防护易被绕过。
method: 在预训练模型中嵌入保护性后门，基于触发条件限制微调行为。
result: 后门方法比扰动法更鲁棒，有效阻止了恶意个性化。
conclusion: PersGuard为扩散模型发布方提供了实用的隐私保护机制。
---

## Abstract
Diffusion models (DMs) have achieved remarkable success in text-to-image (T2I) generation, yet their personalization capabilities pose serious privacy and copyright risks. Existing protection methods primarily rely on adversarial perturbations, which are impractical in realistic settings and can be easily bypassed when inputs are mixed with clean or transformed data. In this work, we propose PersGuard, a novel model backdoor-based framework to prevent unauthorized personalization of pre-trained T2I diffusion models. Unlike perturbation-based approaches, PersGuard embeds protective backdoors directly into released models, ensuring that fine-tuning on protected images triggers predefined protective behaviors, while unprotected images yield normal outputs. To this end, we formulate backdoor injection as a unified optimization problem with three objectives, and introduce a backdoor retention loss to withstand downstream personalized fine-tuning. Extensive experiments across comparative and gray-box settings, as well as multi-identity scenarios, demonstrate that PersGuard delivers stronger and more reliable protection than existing methods.

---

## 论文详细总结（自动生成）

# PersGuard：通过模型后门防止文本到图像扩散中的恶意个性化

## 1. 研究动机与核心问题
- **背景**：文本到图像扩散模型（DMs）在个性化生成上表现优异，用户可通过微调向模型注入特定人物、物体或风格。
- **核心风险**：恶意用户可未经授权地对他人肖像、版权内容进行个性化微调，造成隐私泄露和版权侵犯。
- **现有防御局限**：主流防护依赖对抗扰动（adversarial perturbations），在真实场景中实用性差，且当输入混合干净或变换数据时极易被绕过。
- **本文目标**：从模型发布方视角，提出一种内置后门的防御机制，使模型一旦被用于未经授权的个性化微调，便触发保护行为，从根本上阻止隐私或版权信息的泄露。

## 2. 方法论
### 2.1 核心思想
- 将防护功能以**模型后门**的形式直接嵌入预训练扩散模型，而非对图像添加扰动。
- 后门在模型发布前注入，当用户使用受保护图像微调时，触发预定义的保护输出（如模糊、遮挡、变形），而正常图像微调时模型表现正常。

### 2.2 关键技术细节
- **统一优化问题**：后门注入被形式化为包含三个目标的优化问题：
  1. 保护目标：微调后模型在触发条件下生成保护性输出。
  2. 保真度目标：未触发时模型保持对正常图像的生成质量。
  3. 抗遗忘目标：后门在下游个性化微调过程中不被覆盖或遗忘。
- **后门保留损失（backdoor retention loss）**：专门设计的损失项，确保即使经过个性化微调，后门效应仍然存在。
- **实现框架**：通过对模型权重引入可控的后门模式，结合触发条件（例如特定图像特征或标识），使微调后模型行为可预测地偏离正常。

### 2.3 算法流程（文字描述）
1. **预训练阶段**：模型发布方在扩散模型参数中注入保护性后门，使用目标函数联合优化生成质量与后门鲁棒性。
2. **分发阶段**：将含后门的模型公开发布。
3. **用户微调阶段**：
   - 若用户使用普通图像微调，模型保持标准个性化能力。
   - 若用户使用受保护图像（如特定人脸）微调，后门被激活，输出被强制扭曲或遮挡，无法生成可辨认的肖像，从而阻止隐私泄露。

## 3. 实验设计
### 3.1 数据集与场景
- **受保护内容**：可能包括人脸数据集（如 CelebA）、版权作品等（摘要未详列，需参见原文）。
- **评估场景**：
  - **对比设置（Comparative settings）**：与现有对抗扰动防护方法直接对比。
  - **灰盒设置（Gray-box settings）**：攻击者部分知晓后门存在但仍无法规避。
  - **多身份场景（Multi-identity scenarios）**：同时对多个身份施加保护。

### 3.2 对比方法
- 对比基于对抗扰动的保护方案（如 AdvDM 等典型方法，具体名称原文可能列于正文）。

### 3.3 评估指标
- 保护效果：微调后生成图像中受保护内容的可辨识度、相似度。
- 图像质量：正常微调时生成图像的 FID、CLIP 分数等。
- 鲁棒性：在数据混合、变换下的防护持久性。

## 4. 资源与算力
- **摘要未提供**具体 GPU 型号、数量或训练时长。需参阅完整论文了解算力消耗细节。
- **推断**：扩散模型后门注入与微调实验通常需要多张高性能 GPU（如 A100），但本文未在元数据中说明。

## 5. 实验数量与充分性
- **实验种类**：
  - 对比实验（vs. 对抗扰动方法）
  - 灰盒鲁棒性测试
  - 多身份保护实验
  - 消融实验（可能涉及损失项、后门强度等）
- **充分性判断**：摘要称“大量实验”（Extensive experiments），覆盖不同设置，可初步判断较为充分。但具体实验组数需查阅正文。
- **公平性**：与同类防护方法直接比较，在统一设置下评估，具备可比性；灰盒设定考察了实际攻击场景，增强了客观性。

## 6. 主要结论与发现
- PersGuard 的后门防护比对抗扰动方法更强且更可靠（stronger and more reliable）。
- 后门方法能有效抵御混合干净数据、数据变换等绕过手段，对抗扰动方法在这些情况下失效。
- 该框架为扩散模型发布方提供了实用的隐私与版权保护机制。

## 7. 优点
- **范式创新**：首次将模型后门用于扩散模型的个性化滥用防护，由被动扰动转为主动模型控制。
- **高鲁棒性**：后门内建于模型权重，不易被数据清洗、变换破坏。
- **实用性强**：模型发布方仅需一次后门注入，无需用户配合，便于部署。
- **多场景验证**：考虑了对比、灰盒、多身份等实际威胁模型，评估全面。

## 8. 不足与局限
- **依赖模型发布方**：防护建立在发布方可信且愿意嵌入后门的前提下，若模型由不受控第三方发布则无效。
- **后门可能被检测或移除**：攻击者可能尝试通过微调消除后门，虽然后门保留损失提高了难度，但未完全免疫。
- **通用性限制**：摘要未提及时对其他生成任务（如非人脸物体、风格）的泛化能力。
- **计算成本未知**：后门注入和保护损失的训练开销未披露。
- **伦理考量**：后门技术本身敏感，可能引发双重用途担忧，需严格限定应用范围。

（完）
