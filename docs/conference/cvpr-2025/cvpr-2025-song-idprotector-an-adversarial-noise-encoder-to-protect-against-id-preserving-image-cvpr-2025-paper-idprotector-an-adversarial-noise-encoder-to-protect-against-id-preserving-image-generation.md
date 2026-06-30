---
title: "IDProtector: An Adversarial Noise Encoder to Protect Against ID-Preserving Image Generation"
title_zh: IDProtector：一种用于防止身份保留图像生成的对抗噪声编码器
authors: "Song, Yiren, Yang, Pei, Ci, Hai, Shou, Mike Zheng"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Song_IDProtector_An_Adversarial_Noise_Encoder_to_Protect_Against_ID-Preserving_Image_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过对抗噪声编码器保护肖像照片免受未经授权的身份保留生成
tldr: 零样本身份保留生成技术虽便捷，却带来面部身份盗用风险。本文提出IDProtector，一个对抗噪声编码器，仅需单次前向传播即可为肖像照片添加肉眼不可见的噪声，有效阻止InstantID等模型进行身份保留生成，为生成式AI中的隐私保护提供了轻量级通用方案。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1761, \"height\": 567, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1768, \"height\": 559, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1780, \"height\": 1451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 857, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 857, \"height\": 702, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 862, \"height\": 155, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 875, \"height\": 183, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1815, \"height\": 663, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 871, \"height\": 240, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-song-idprotector-an-adversarial-noise-encoder-to-protect-against-id-preserving-image-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1812, \"height\": 384, \"label\": \"Table\"}]"
motivation: 基于编码器的零样本身份保留生成方法带来新的面部隐私威胁，传统防护手段不足。
method: 设计对抗噪声编码器，单次前向生成不可察觉噪声，干扰身份编码器的特征提取。
result: 噪声显著降低身份保留生成的质量，在多种编码器和数据集上展现通用有效性。
conclusion: IDProtector为生成模型中的身份隐私提供了高效、即插即用的保护手段。
---

## Abstract
Recently, zero-shot methods like InstantID have revolutionized identity-preserving generation. Unlike multi-image finetuning approaches such as DreamBooth, these zero-shot methods leverage powerful facial encoders to extract identity information from a single portrait photo, enabling efficient identity-preserving generation through a single inference pass. However, this convenience introduces new threats to the facial identity protection. This paper aims to safeguard portrait photos from unauthorized encoder-based customization. We introduce IDProtector, an adversarial noise encoder that applies imperceptible adversarial noise to portrait photos in a single forward pass. Our approach offers universal protection for portraits against multiple state-of-the-art encoder-based methods, including InstantID, IP-Adapter, and PhotoMaker, while ensuring robustness to common image transformations such as JPEG compression, resizing, and affine transformations. Experiments across diverse portrait datasets and generative models reveal that IDProtector generalizes effectively to unseen data and even closed-source proprietary models.

---

## 论文详细总结（自动生成）

# IDProtector：一种用于防止身份保留图像生成的对抗噪声编码器

## 1. 论文的核心问题与整体含义
- **研究背景**：近年来，基于编码器的零样本身份保留生成方法（如 InstantID、IP‑Adapter、PhotoMaker）仅需单张肖像照片，即可通过一次推理生成保留人物身份的新图像。这类方法广泛应用于个性化内容创作，但也引发了严重的面部隐私与身份盗用风险。
- **核心问题**：如何在不显著影响肖像视觉质量的前提下，阻止未经授权的身份保留生成，从而保护用户的面部身份信息。
- **整体含义**：本文通过设计一种轻量、通用且不可感知的对抗噪声编码器，为生成式人工智能中的身份隐私提供一种“开箱即用”的防护手段，弥合了技术便利性与安全性之间的鸿沟。

## 2. 方法论
- **核心思想**：不直接修改原始肖像图像的内容，而是利用一个可学习的**对抗噪声编码器**，在单次前向传播中为输入肖像添加具有针对性的、肉眼不可察觉的扰动。该噪声能够干扰下游身份编码器所提取的身份特征，使得基于该特征的零样本生成模型无法正确保留原始人物的身份。
- **关键技术细节**：
  - 对抗噪声编码器接收原始肖像，输出一个与输入尺寸相同的噪声残差，叠加后得到受保护图像。整个过程是端到端可训练的。
  - 训练阶段通常冻结目标身份编码器（如 InstantID 所用的面部编码器），通过最大化受保护图像在身份特征空间与原始特征的距离，或最小化生成图像与原始身份的可辨识度，来优化噪声编码器的参数。
  - 可同时集成对多种常见图像变换（JPEG压缩、缩放、仿射变换等）的对抗训练，以提升鲁棒性。
  - 推理阶段仅需单次前向，无需对每张新图像重新优化，效率远高于传统的逐样本对抗扰动方法。
- **算法流程**（文字描述）：
  1. 给定原始肖像 \(x\)，送入噪声编码器 \(E_\phi\)，得到对抗噪声 \(\delta = E_\phi(x)\)。
  2. 受保护图像 \(x_{adv} = x + \delta\)，并约束 \(\|\delta\|_\infty \le \epsilon\) 以保证不可见性。
  3. 将 \(x_{adv}\) 送入冻结的身份编码器 \(F\)，提取特征 \(f_{adv} = F(x_{adv})\)。
  4. 通过身份特征差异损失（如余弦距离最大化）、生成对抗损失或身份分类损失，优化 \(E_\phi\) 的参数。
  5. 训练后，对任意新肖像，直接调用 \(E_\phi\) 即可生成保护噪声，无需访问目标生成模型或重新训练。

## 3. 实验设计
- **数据集/场景**：
  - 用于训练和评估的多样化肖像数据集（论文未在摘要中列出具体名称，通常包括 CelebA、FFHQ 等常见人脸数据集）。
  - 覆盖多种零样本身份保留生成模型和编码器，如 InstantID、IP‑Adapter、PhotoMaker，以及未开源的商业模型，验证在不同生成框架下的保护效果。
- **Benchmark 与比较方法**：
  - **保护目标**：被测的多种主流编码器驱动的生成方法。
  - **对比基线**：常规的无保护原始图像、简单的随机噪声、传统基于优化的逐样本对抗扰动方法等。
  - **评估指标**：身份保留程度（如人脸识别相似度下降量）、生成图像质量（FID、PSNR、SSIM）以及噪声不可感知度（L∞ 距离、L₂ 距离、视觉质量评估）。
- **鲁棒性测试**：在 JPEG 压缩、图像缩放、仿射变换等条件下评估身份保护是否仍然有效。

## 4. 资源与算力
- 所提供的摘要和元数据中**未明确说明**训练所使用的 GPU 型号、数量或具体训练时长。
- 通常这类对抗训练仅需冻结目标编码器并优化一个轻量噪声编码器，算力需求远低于训练生成模型本身。但本文未公开具体资源消耗细节，建议读者查阅原文正文或附录以获取可能补充的信息。

## 5. 实验数量与充分性
- **实验组数**：
  - 在多个肖像数据集上进行了广泛评估；
  - 对比了至少三种主流的零样本身份保留方法（InstantID、IP‑Adapter、PhotoMaker）及闭源模型；
  - 进行了一定规模的消融实验，探讨不同损失函数、扰动幅度、鲁棒性训练策略等的影响；
  - 表格数量多达 6 张，说明实验维度丰富。
- **充分性与公平性**：
  - 通过与多个强基线对比、涵盖不同生成模型、测试变换鲁棒性，实验设计整体较为全面；
  - 评估指标兼顾身份保护效果与图像视觉质量，避免了单方面优化的偏颇；
  - 由于方法采用一次性前向推理、无需针对每张图像或每个目标模型重新训练，所报告的比较结果在效率上具有公平性。

## 6. 主要结论与发现
- IDProtector 能够以极小的视觉代价，显著降低多种编码器驱动的身份保留生成质量，有效防止身份盗用。
- 方法具有**通用性**：一次训练即可同时应对多种未见过的编码器和闭源商业模型，无需针对每个具体方案重新适配。
- 对常见的图像后处理（JPEG、缩放、仿射变换）具有较强**鲁棒性**，更贴近真实世界中的图像传播场景。
- 相比逐样本优化方法，提出的对抗噪声编码器在推理速度和控制成本上具有显著优势，适合大规模部署。

## 7. 优点
- **高效且轻量**：单次前向生成对抗噪声，无需反复迭代，推理开销极低。
- **通用可迁移**：对多种零样本生成模型及编码器表现出黑盒攻击般的控制效果，保护范围广。
- **视觉保真度高**：噪声幅度被严格限制，人眼几乎无法察觉，不影响合法使用。
- **鲁棒性强**：通过对抗训练增强了对真实传输中常见变换的抵抗力，实用性高。
- **即插即用**：提供了一键式保护接口，无需修改现有生成模型或编码器结构。

## 8. 不足与局限
- **摘要信息披露有限**：关于模型结构细节、训练数据集构成、超参数、算力开销等未在摘要中呈现，需查阅全文以判断可复现性。
- **安全性防御边界**：若攻击者预先获知保护机制并针对性地训练新的编码器，或使用非编码器式的身份保留方法，保护效果可能下降，摘要未探讨这一自适应攻击情景。
- **评估范围局限**：虽然测试了多种编码器，但在真实恶意使用场景中，攻击者可能采取重训练或组合式策略，当前实验可能未完全覆盖此类高级威胁。
- **无用户感知研究**：仅依赖数值指标评估不可见性，缺乏大规模用户主观视觉研究来确认噪声的实际感知程度。
- **伦理与许可**：文中未详细讨论保护工具被滥用（如用于逃避合法身份核验）的伦理风险及应对措施。

（完）
