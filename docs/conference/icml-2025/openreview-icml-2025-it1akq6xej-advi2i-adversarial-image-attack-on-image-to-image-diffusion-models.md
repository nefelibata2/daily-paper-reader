---
title: "AdvI2I: Adversarial Image Attack on Image-to-Image Diffusion Models"
title_zh: AdvI2I：针对图像到图像扩散模型的对抗性图像攻击
authors: "Yaopei Zeng, Yuanpu Cao, Bochuan Cao, Yurui Chang, Jinghui Chen, Lu Lin"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=It1AkQ6xEJ"
tags: ["query:priv-sec"]
score: 9.0
evidence: 图像到图像扩散模型中的对抗性图像攻击漏洞
tldr: 本文揭露了图像到图像扩散模型存在安全隐患：攻击者可通过精心构造的对抗图像诱导模型生成不良内容，绕过文本过滤。提出AdvI2I框架，优化生成器制作对抗样本，揭示了现有安全措施的不足。实验证明该攻击有效，对生成模型的内容安全构成严重威胁。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 扩散模型易受对抗性提示攻击生成不安全内容，但文本提示易被过滤，图像输入漏洞尚未被充分研究。
method: 提出AdvI2I框架，通过优化生成器生成对抗图像，操纵I2I扩散模型输出NSFW内容。
result: 实验表明AdvI2I能有效绕过文本过滤器，诱导模型生成不良内容，暴露严重安全漏洞。
conclusion: AdvI2I揭示了扩散模型在图像输入上的新攻击面，提醒安全防御需覆盖多模态输入。
---

## Abstract
Recent advances in diffusion models have significantly enhanced the quality of image synthesis, yet they have also introduced serious safety concerns, particularly the generation of Not Safe for Work (NSFW) content. Previous research has demonstrated that adversarial prompts can be used to generate NSFW content. However, such adversarial text prompts are often easily detectable by text-based filters, limiting their efficacy. In this paper, we expose a previously overlooked vulnerability: adversarial image attacks targeting Image-to-Image (I2I) diffusion models. We propose AdvI2I, a novel framework that manipulates input images to induce diffusion models to generate NSFW content. By optimizing a generator to craft adversarial images, AdvI2I circumvents existing defense mechanisms, such as Safe Latent Diffusion (SLD), without altering the text prompts. Furthermore, we introduce AdvI2I-Adaptive, an enhanced version that adapts to potential countermeasures and minimizes the resemblance between adversarial images and NSFW concept embeddings, making the attack more resilient against defenses. Through extensive experiments, we demonstrate that both AdvI2I and AdvI2I-Adaptive can effectively bypass current safeguards, highlighting the urgent need for stronger security measures to address the misuse of I2I diffusion models.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究动机**：扩散模型图像生成质量大幅提升，但也带来了生成不安全（NSFW）内容的严重隐患。现有研究主要通过对抗性文本提示引发越狱，但这类文本提示通常能被基于文本的过滤器轻易检测，攻击效果受限。
- **核心问题**：本文揭示了一个被忽视的攻击面——**图像到图像（I2I）扩散模型**中，对抗性**图像**输入可成为新的攻击载体。攻击者可在不修改文本提示（甚至使用安全提示）的情况下，通过操纵输入图像迫使模型生成有害内容，从而绕过文本过滤器。
- **整体含义**：I2I扩散模型对多模态输入（尤其是图像）的安全防护严重不足，仅依靠文本审核无法阻止恶意利用，亟需更强健的多模态防御机制。

## 2. 论文提出的方法论
- **核心思想**：训练一个生成器，该生成器能够将任意输入图像转换为精心构造的对抗图像，当该对抗图像与无害文本提示一同送入 I2I 扩散模型时，会诱导模型生成 NSFW 内容。
- **关键技术细节**：
  - **AdvI2I 框架**：通过优化生成器参数，最大化扩散模型输出与NSFW概念嵌入的相似度（或直接攻击安全过滤器，如 Safe Latent Diffusion, SLD）。框架不修改文本提示，仅通过对抗扰动控制图像引导方向。
  - **AdvI2I-Adaptive 增强版本**：为应对可能的防御措施，在优化目标中引入两个关键改进：① 自适应地适应潜在反制手段；② 最小化对抗图像与 NSFW 概念嵌入之间的视觉/语义相似度，使对抗样本更难被图像过滤器检测，攻击更具弹性和隐蔽性。
- **算法流程（文字描述）**：
  1. 固定 I2I 扩散模型和目标 NSFW 概念。
  2. 生成器接收原始图像，输出对抗扰动并与原图叠加得到对抗图像。
  3. 将对抗图像与中性文本提示送入模型进行去噪生成。
  4. 根据生成结果与 NSFW 内容的距离计算损失，反向传播更新生成器参数，循环优化。
  5. AdvI2I-Adaptive 额外加入正则项，抑制对抗图像在概念嵌入空间中与显式 NSFW 特征的接近度。

## 3. 实验设计
- **数据集与场景**：摘要及元数据中未明确列出具体数据集名称（如 COCO、LAION-5B 等），但可推测使用了通用自然图像数据集与自定义的 NSFW 概念库。场景聚焦于**绕过文本过滤器，仅通过图像攻击诱导生成有害内容**。
- **对比基准（Benchmark）**：文中提到的防御方法为 **Safe Latent Diffusion (SLD)**，实验应比较了 **无防御、仅有文本过滤、SLD防御** 以及 **AdvI2I vs. AdvI2I-Adaptive** 等条件下的攻击成功率。
- **对比方法**：自身框架的两种变体（AdvI2I 与 AdvI2I-Adaptive）之间的对比，以及与其它未明确指出的潜在攻击或防御基线的比较。

## 4. 资源与算力
- 提供的论文摘要及元数据中 **未提及** 使用的 GPU 型号、数量、训练时长等算力信息，无法评估资源开销。

## 5. 实验数量与充分性
- **实验组数**：摘要称进行了“大量实验（extensive experiments）”，但未给出具体实验组的数量（如不同数据集、不同防御机制、不同模型架构的消融实验数目）。
- **充分性与公平性**：
  - **充分性**：若能证明攻击在多种 I2I 模型和有/无防御下均有效，则充分性较高，但细节缺失。
  - **客观公平性**：对比 SLD 防御时，保持文本提示和模型权重不变，仅改变图像输入，实验设置应是公平的。AdvI2I-Adaptive 进一步考虑了防御自适应，提升了评估的完整性。
- **局限**：由于缺少具体实验规模数据，难以从提供文本中判断实验是否覆盖了足够的现实场景（如不同风格的 I2I 模型、真实聊天机器人接口等）。

## 6. 论文的主要结论与发现
- I2I 扩散模型存在 **严重的图像端对抗漏洞**，攻击者可通过 AdvI2I 生成对抗图像，诱导模型产生 NSFW 内容，**完全绕过** 仅依赖文本提示的过滤器。
- AdvI2I-Adaptive 甚至能进一步躲避基于图像语义的防御，并降低对抗样本与有害概念的显式关联，使攻击更为隐蔽且难以检测。
- 当前针对扩散模型的安全措施（如 SLD）在面对图像攻击时表现脆弱，提示社区必须 **将防御范围扩展到多模态输入层面**。

## 7. 优点
- **新攻击面发现**：首次系统性地揭露 I2I 扩散模型中图像输入对抗攻击的风险，填补了该方向的研究空白。
- **方法简洁有效**：AdvI2I 框架通过优化生成器实现攻击，无需修改文本提示，易于部署。
- **前瞻性防御考虑**：AdvI2I-Adaptive 展示了对未来防御机制的适应性对抗，增强了研究的现实意义和鲁棒性评估深度。
- **安全警示价值**：结果警示业界和学界，图像引导的越狱攻击可能成为真实世界的严重威胁。

## 8. 不足与局限
- **实验细节缺失**：摘要未提供数据集、具体模型版本、量化指标（如攻击成功率、图像质量评价）等信息，无法评估实验的完备性和可复现性。
- **对抗样本感知性未讨论**：未说明生成的对抗图像是否具有人眼可察觉的噪声或变形，若扰动过大，则在实际应用（如上传篡改图片）中易被人工审核发现。
- **攻击适用范围受限**：仅针对 I2I 扩散模型，未涉及其他生成范式（如视频、3D模型），且可能需要白盒访问模型梯度，在黑盒或商业 API 场景下的迁移性未验证。
- **防御对策仍待探索**：论文揭示了问题，但并未提出具体、可行的防御方案，仅呼吁加强多模态防护。

（完）
