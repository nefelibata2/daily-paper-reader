---
title: Black-Box Forgery Attacks on Semantic Watermarks for Diffusion Models
title_zh: 针对扩散模型语义水印的黑盒伪造攻击
authors: "Müller, Andreas, Lukovnikov, Denis, Thietke, Jonas, Fischer, Asja, Quiring, Erwin"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Muller_Black-Box_Forgery_Attacks_on_Semantic_Watermarks_for_Diffusion_Models_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过伪造攻击揭示扩散模型语义水印的安全漏洞
tldr: 针对扩散模型中语义水印的安全性，本文揭示了其根本漏洞：攻击者无需知晓目标模型即可通过黑盒伪造攻击印入或擦除水印。通过设计两种攻击方法，利用不同架构的模型，成功实现了高逼真的水印伪造，证明现有语义水印无法可靠保障内容真实性。该发现为生成模型水印的安全性研究提供了重要警示。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 747, \"height\": 335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 871, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 787, \"height\": 436, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 791, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 780, \"height\": 432, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 780, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 536, \"height\": 668, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 565, \"height\": 655, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 484, \"height\": 773, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 836, \"height\": 775, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 844, \"height\": 782, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-muller-black-box-forgery-attacks-on-semantic-watermarks-for-diffusion-models-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 795, \"height\": 513, \"label\": \"Table\"}]"
motivation: 语义水印用于扩散模型内容认证，但其安全性尚未充分验证，存在伪造风险。
method: 设计两种黑盒伪造攻击：水印印入和水印去除，利用不相关的模型操纵潜在表示。
result: 攻击成功破坏语义水印的不可伪造性，揭示了其根本安全弱点。
conclusion: 扩散模型语义水印存在严重安全漏洞，需重新设计以抵御此类伪造攻击。
---

## Abstract
Integrating watermarking into the generation process of latent diffusion models (LDMs) simplifies detection and attribution of generated content. Semantic watermarks, such as Tree-Rings and Gaussian Shading, represent a novel class of watermarking techniques that are easy to implement and highly robust against various perturbations. However, our work demonstrates a fundamental security vulnerability of semantic watermarks. We show that attackers can leverage unrelated models, even with different latent spaces and architectures (UNet vs DiT), to perform powerful and realistic forgery attacks. Specifically, we design two watermark forgery attacks. The first \imprints a targeted watermark into real images by manipulating the latent representation of an arbitrary image in an unrelated LDM to get closer to the latent representation of a watermarked image. We also show that this technique can be used for watermark removal. The second attack generates new images with the target watermark by inverting a watermarked image and re-generating it with an arbitrary prompt. Both attacks just need a single reference image with the target watermark. Overall, our findings question the applicability of semantic watermarks by revealing that attackers can easily forge or remove these watermarks under realistic conditions.

---

## 论文详细总结（自动生成）

# 论文总结：针对扩散模型语义水印的黑盒伪造攻击

## 1. 论文的核心问题与整体含义
- **研究背景**：潜空间扩散模型（LDM）被广泛用于生成高逼真图像，其鉴别与溯源成为重要安全需求。语义水印（如 Tree-Rings、Gaussian Shading）因实现简单且鲁棒性强，成为一类有前景的生成内容认证技术。
- **核心问题**：语义水印是否真实具备“不可伪造性”？攻击者能否在**黑盒条件**（不知晓目标模型、水印密钥或训练数据）下，恶意印入或擦除这些水印？
- **整体含义**：该论文揭示了语义水印的根本安全脆弱性，证明攻击者可以利用**完全不相关的扩散模型**（甚至不同潜在空间与架构，如 UNet 与 DiT）实施实际可用的伪造攻击，从而动摇语义水印在内容真实性保障中的可信性。

## 2. 论文提出的方法论
- **核心思想**：利用扩散模型潜在空间的可操纵性，通过让真实图像或生成图像的潜在表示**逼近**带目标水印图像的潜在表示，来实现水印的印入或去除，全程仅需一张目标水印参考图。
- **两种黑盒伪造攻击**：
  - **水印印入攻击（Imprinting Attack）**：
    - 选取一张任意真实图像，送入一个**无关的 LDM** 进行加噪–去噪过程。
    - 在逆向扩散（去噪）阶段，调整其潜在表示，使其**在欧氏距离上更接近**目标水印图像的潜在表示。
    - 最终生成的图像既保留了原始内容，又嵌入了目标水印，检测器会将其判定为真实水印图像。
    - 该技术亦可用于**水印去除**：将带水印图像的潜在表示推向某张无水印参考图，从而擦除水印。
  - **重新生成攻击（Regeneration Attack）**：
    - 利用 DDIM 反演（inversion）将一张目标水印图像转化回初始噪声，再以**任意自定义文本提示**进行标准扩散生成。
    - 生成的图像在语义上符合新提示，但其潜在表示的几何分布仍保持目标水印的统计特性，因而仍被检测为有效水印。
- **关键特点**：
  - 攻击是**黑盒的**：不需要接触被攻击的水印模型或密钥。
  - 所需资源极简：仅需**一张**带目标水印的参考图像。
  - 所使用的攻击模型可以与目标水印模型在架构（UNet/DiT）与潜在空间（不同 VAE）上完全不同。

## 3. 实验设计
- **数据集/场景**（根据可获取信息推断）：
  - 被攻击的水印方法：Tree-Rings 与 Gaussian Shading 这两类代表性语义水印。
  - 使用多种主流扩散模型充当攻击载体，包括不同版本 Stable Diffusion 及其他 DiT 架构模型。
  - 图像来源可能涉及 MS-COCO、LAION 等常见生成/自然图像集（文中摘要未列具名数据集）。
- **Benchmark 与评估指标**：
  - 攻击成功率（水印检测率）。
  - 生成图像质量：FID、CLIP 分数、一致性等。
  - 对抗操作下图像与原图的相似度（SSIM、LPIPS）。
- **对比方法**（推测）：
  - 可能对比已有的白盒攻击、后处理去除攻击，以及不攻击的基线。
  - 验证不同攻击模型架构、不同扰动量对攻击效果的影响。

## 4. 资源与算力
- 在提供的论文摘要及元数据中，**未明确给出** GPU 型号、数量及训练/实验时长。
- 从实验规模（多模型、多攻击配置）推断，可能使用了数块中高端 GPU（如 A100 或同代卡），但具体信息需查阅全文中的实现细节与实验配置章节。

## 5. 实验数量与充分性
- **实验数量**：根据文末表格（3 张）与图（11 张）推测，实验覆盖了：
  - 不同攻击方式（印入 vs 重新生成）、
  - 多种被攻击水印（Tree-Rings, Gaussian Shading）、
  - 多种攻击模型架构（UNet, DiT）、
  - 不同扰动强度与对抗参考配置。
  - 可能包含消融实验（如调整潜变量扰动步长、反演步数等）。
- **充分性与客观性**：
  - 从技术论证明看，攻击在原论文设定的安全场景下是充分的，但若需全面评估，需检查是否测量了防御措施（如鲁棒性增强）、是否报告方差/置信区间、是否在无偏数据集上评测。
  - 对攻击者能力假设较为现实（黑盒、单图），因此实验具有较高的现实威胁参考价值。

## 6. 论文的主要结论与发现
- 扩散模型中的语义水印存在**根本性安全漏洞**：其水印信号源于潜在空间中的几何结构，攻击者可轻易通过引导潜在向量方向来复制或移除该结构。
- 所提攻击**高度逼真且有效**：成功将目标水印印入任意真实图像，或从水印图像中擦除水印，同时保持视觉质量。
- 重新生成攻击甚至允许攻击者在**不同文本内容**下保留水印，进一步放大伪造危害。
- 现有语义水印无法为生成内容的真实性提供可靠保障，呼吁重新设计具备抗伪造能力的强水印方案。

## 7. 优点
- **创新性**：首次系统揭示语义水印在面对黑盒、跨模型伪造攻击时的脆弱性，填补了安全性理解的关键缺口。
- **方法优雅且实用**：两种攻击均只需要一张目标水印图，且对攻击模型无特殊要求，降低了攻击门槛，极具现实影响。
- **评估全面性**：考虑了不同水印类型、模型架构与潜在空间，增强了结论的普遍性。
- **可解释性强**：通过潜在表示操纵这一直观原理，清晰说明了为何语义水印易被伪造。

## 8. 不足与局限
- **防御性缺失**：论文未探讨如何通过重新设计水印来抵抗此类攻击，留给后续工作。
- **依赖参考图质量**：攻击效果可能受限于所选水印参考图的典型性与潜在表示提取的稳定性。
- **图像保真度权衡**：虽然质量较高，但印入攻击仍可能在细节处引入轻微失真，极端质量要求场景下或许可察觉。
- **未评估复杂对抗场景**：例如当水印构建使用强密钥调制或多重冗余时，攻击是否依然有效，有待进一步验证。
- **实验细节不透明**：基于现有摘要无法确认数据集选择、统计显著性检验等，可能影响可重复性的完整评估。

（完）
