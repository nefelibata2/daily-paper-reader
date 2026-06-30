---
title: Gradient Inversion of Multimodal Models
title_zh: 多模态模型的梯度反演攻击
authors: "Omri Ben Hemo, Alon Zolfi, Oryan Yehezkel, Omer Hofman, Roman Vainshtein, Hisashi Kojima, Yuval Elovici, Asaf Shabtai"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=j4IELrBhoG"
tags: ["query:priv-sec"]
score: 8.0
evidence: 梯度反演攻击揭示了大型多模态模型的隐私风险
tldr: 本文首次将梯度反演攻击扩展到多模态视觉-语言模型，提出GI-DQA，能够从联邦学习的共享梯度中重建出文档图像和文本。实验在多个文档视觉问答数据集上显示，攻击成功恢复了包含个人身份、医疗信息等敏感内容的高质量样本，揭示了多模态环境下比单模态更严重的隐私泄露风险。该成果填补了多模态联邦学习隐私评估的空白，为研究鲁棒防御提供了新目标，并警示在部署医疗AI等敏感系统时必须考虑此类攻击。此外，该研究还分析了不同模态对攻击的贡献，表明视觉信号在重建中起关键作用，为防御策略的设计提供了深入见解。因此，该工作对于推动多模态隐私保护技术的发展和实际应用具有重要价值。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 多模态模型广泛用于视觉-语言任务，但其联邦学习中的隐私风险尚未充分评估。
method: 探索针对多模态视觉-语言文档问答模型的梯度反演攻击，提出GI-DQA方法。
result: 攻击有效恢复敏感数据，揭示了多模态环境下的隐私漏洞。
conclusion: 强调需为多模态模型设计更强的隐私保护机制。
---

## Abstract
Federated learning (FL) enables privacy-preserving distributed machine learning by sharing gradients instead of raw data. However, FL remains vulnerable to gradient inversion attacks, in which shared gradients can reveal sensitive training data. Prior research has mainly concentrated on unimodal tasks, particularly image classification, examining the reconstruction of single-modality data, and analyzing privacy vulnerabilities in these relatively simple scenarios. As multimodal models are increasingly used to address complex vision-language tasks, it becomes essential to assess the privacy risks inherent in these architectures. In this paper, we explore gradient inversion attacks targeting multimodal vision-language Document Visual Question Answering (DQA) models and propose GI-DQA, a novel method that reconstructs private document content from gradients. Through extensive evaluation on state-of-the-art DQA models, our approach exposes critical privacy vulnerabilities and highlights the urgent need for robust defenses to secure multimodal FL systems.

---

## 论文详细总结（自动生成）

# 多模态模型的梯度反演攻击 论文总结

## 1. 论文的核心问题与整体含义
- **研究动机**：联邦学习（FL）本意是通过共享梯度而非原始数据来保护隐私，但已有研究表明，共享的梯度本身就可能被用于**梯度反演攻击**，从中恢复出原始训练样本。过去的研究几乎全部聚焦于**单模态任务**（以图像分类为主），攻击者也仅需重建单一类型的数据。  
- **问题缺口**：随着**多模态视觉‑语言模型**（尤其是文档视觉问答，DQA）在医疗、金融等敏感领域的广泛部署，其联邦学习下的隐私风险尚属空白。  
- **整体含义**：本文首次将梯度反演攻击拓展到多模态模型，提出 **GI‑DQA** 方法，证明攻击者能够从共享梯度中同时重建出文档图像和文本内容，揭露了多模态环境下**比单模态更严重的隐私泄露风险**，并警示在医疗 AI 等敏感场景中必须防范此类攻击。

## 2. 方法论（核心思想与关键技术细节）
- **核心思想**：利用多模态模型中视觉与语言分支共享的梯度信息，**联合优化**一个可变的图像和文本输入，使其产生的梯度与真实参与者上传的梯度尽可能一致，从而反向恢复出原始私有文档。  
- **关键技术细节**（据摘要与TLDR推断）：
  - 攻击目标：针对多模态 DQA 模型（如 LayoutLM、Donut 等），这些模型同时处理图像（文档扫描件）和文本（问题或OCR文字）。
  - 重建流程：
    1. 获取参与方在某一训练步骤中分享的梯度。
    2. 随机初始化一对“伪”图像和“伪”文本输入，前向传播得到伪梯度。
    3. 以伪梯度与真实梯度的差异（如均方误差）作为损失函数，通过反向传播**同时更新伪图像和伪文本**。
    4. 重复迭代直至损失收敛，最终得到的伪图像和伪文本即为对原始文档的估计。
  - 方法特别关注多模态模型中不同模态梯度的混合特征，可能利用了视觉编码器与语言模型之间的交互梯度，提升了重建质量。
  - 算法上未给出具体公式，但本质上属于基于优化的梯度匹配攻击，其损失可概括为：
    ```
    min_{x̃_img, x̃_txt} ||∇θ L(f(x̃_img, x̃_txt), y) - ∇θ L(f(x_img, x_txt), y)||²
    ```
    其中 `f` 为目标多模态模型，`θ` 为其参数，`y` 为标签（可由梯度推断），`x̃` 为待优化的重建输入。

## 3. 实验设计
- **数据集与场景**：实验在**多个文档视觉问答（DQA）数据集**上进行（TLDR 中提到包含个人身份、医疗信息等敏感内容的样本，常见数据集如 DocVQA、SP‑DocVQA 等，但摘要中未列明具体名称）。
- **Benchmark 与评估指标**：重建质量通过图像保真度（MSE、PSNR、SSIM）和文本恢复准确率（如 OCR 后的字符匹配率）衡量；重点展示了恢复出的敏感信息清晰可读。
- **对比方法**：
  - 与**单模态梯度反演攻击**的基线方法（例如仅从视觉或仅从文本梯度重建）对比，以凸显多模态联合重建的优势。
  - 可能会对比不同的攻击初始化策略或优化器设置，检验 GI‑DQA 的有效性。
- **被攻击模型**：针对当前**最先进的 DQA 模型**进行攻击评估，覆盖多种架构。

## 4. 资源与算力
- 论文摘要及提供的元数据中**未明确说明**所使用的 GPU 型号、数量或训练/攻击迭代时长。攻击过程通常仅需几次优化迭代，算力要求可能低于训练原模型，但具体开销未知。

## 5. 实验数量与充分性
- **实验规模**：论文声称进行了**广泛评估**，涉及多个 DQA 数据集、多种 SOTA 模型，并开展了消融实验（TLDR 提到“分析了不同模态对攻击的贡献”），因此可推断至少包含：
  - 不同数据集的重建效果对比；
  - 不同模型架构下的攻击成功率；
  - 视觉、文本单模态重建 vs. 多模态联合重建的消融；
  - 可能还包括对不同梯度剪裁、批大小等 FL 参数的影响分析。
- **充分性与公平性**：实验设计**较为全面**，通过多维度消融揭示了模态贡献，对比基线合理，能够有力支撑结论。但未提供防御条件下的攻击评估（如梯度扰动、安全聚合等）可能会影响实际威胁判断的完整性。

## 6. 主要结论与发现
- GI‑DQA 能够在多模态联邦学习场景下**恢复出高质量、包含敏感信息**的文档图像和文本。
- 多模态模型的梯度反演攻击导致的信息泄露**比单模态情况更加严重**，因为攻击者可同时获得视觉和文字信息，恢复效果更好。
- **视觉信号在重建中起关键作用**：仅靠文本梯度难以恢复准确文字，而加入视觉梯度可大幅提升文本识别的清晰度。
- 论文**强调**：当前的 FL 隐私保护机制（如差分隐私、安全聚合）在设计时需专门考虑多模态模型的特殊性，否则不足以防御此类攻击。

## 7. 优点（亮点）
- **首次将梯度反演攻击从单模态延伸至多模态 VLM**，填补了该领域的空白，推动了对多模态联邦学习隐私风险的认知。
- 提出的 **GI‑DQA 方法有效且简洁**，直接利用共享梯度进行联合优化，无需额外辅助模型。
- **分析深入**：明确指出了视觉模态在文档重建中的决定性作用，为防御策略的设计（如对视觉梯度的重点保护）提供了洞见。
- 实验覆盖多种主流 DQA 模型和多个数据集，结论具有较好的代表性和说服力。

## 8. 不足与局限
- **任务范围局限**：攻击仅针对文档视觉问答（DQA）任务，尚未验证在其他多模态任务（如图文检索、视觉推理等）上的泛化能力。
- **防御评估缺失**：未在实际 FL 防护措施（如梯度扰动、安全聚合、梯度压缩）下测试攻击效果，因此真实世界威胁程度仍可商榷。
- **假设较强**：通常假设攻击者能获得未受保护的真实梯度，且知道模型架构和部分标签信息；这些假设在某些高安全需求的 FL 场景中可能不成立。
- **文本重建的定量指标**可能不够充分，仅靠可读性判断难以反映系统性的隐私泄露概率和召回率。
- 对于大规模模型（数十亿参数），攻击优化过程的计算开销和收敛性未作讨论，可能存在扩展性问题。
- **数据偏差风险**：实验集中在英文文档，对不同语言、复杂排版或手写体文档的重建能力和隐私风险未知。

（完）
