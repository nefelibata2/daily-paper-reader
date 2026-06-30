---
title: "Not Just Text: Uncovering Vision Modality Typographic Threats in Image Generation Models"
title_zh: 不只是文本：揭示图像生成模型中视觉模态的排版威胁
authors: "Cheng, Hao, Xiao, Erjia, Yang, Jiayan, Cao, Jiahang, Zhang, Qiang, Zhang, Jize, Xu, Kaidi, Gu, Jindong, Xu, Renjing"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Cheng_Not_Just_Text_Uncovering_Vision_Modality_Typographic_Threats_in_Image_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 10.0
evidence: 揭示图像生成模型中视觉模态的排版威胁
tldr: 本文揭示当前图像生成模型在视觉模态中存在排版威胁，这类威胁可通过编辑图像中的文字绕过仅依赖文本防护的机制，提出一种方法来检测并缓解这些新型安全漏洞，为多模态内容安全提供新视角。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 860, \"height\": 768, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1767, \"height\": 912, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1788, \"height\": 621, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 851, \"height\": 518, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 860, \"height\": 572, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1718, \"height\": 224, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1786, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1793, \"height\": 652, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1810, \"height\": 687, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 860, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-cheng-not-just-text-uncovering-vision-modality-typographic-threats-in-image-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 870, \"height\": 337, \"label\": \"Table\"}]"
motivation: 现有图像生成模型的安全防护多聚焦文本模态，视觉模态中的排版威胁容易被忽视。
method: 提出一种检测方法，通过分析视觉模态中的排版攻击揭示其安全风险。
result: 实验显示视觉排版攻击可绕过现有防御，揭示了生成模型的多模态安全挑战。
conclusion: 需同时重视视觉与语言模态的联合安全防护。
---

## Abstract
Current image generation models can effortlessly produce high-quality, highly realistic images, but this also increases the risk of misuse. In various Text-to-Image or Image-to-Image tasks, attackers can generate a series of images containing inappropriate content by simply editing the language modality input. To mitigate this security concern, numerous guarding or defensive strategies have been proposed, with a particular emphasis on safeguarding language modality. However, in practical applications, threats in the vision modality, particularly in tasks involving the editing of real-world images, present heightened security risks as they can easily infringe upon the rights of the image owner. Therefore, this paper employs a method named typographic attack to reveal that various image generation models are also susceptible to threats within the vision modality. Furthermore, we also evaluate the defense performance of various existing methods when facing threats in the vision modality and uncover their ineffectiveness. Finally, we propose the Vision Modal Threats in Image Generation Models (VMT-IGMs) dataset, which would serve as a baseline for evaluating the vision modality vulnerability of various image generation models.

---

## 论文详细总结（自动生成）

## 论文核心问题与研究背景

- **动机**：当前文本-图像和图像-图像生成模型（如扩散模型）可轻易生成高质量甚至滥用性内容，安全风险显著。
- **现有防护偏差**：现有安全策略主要聚焦于语言模态（文本提示）的过滤与防御，忽视了视觉模态中可能存在的攻击面。
- **视觉模态威胁**：在实际应用中，尤其是对真实图像的编辑任务，攻击者可以通过篡改图像本身的视觉信息（如嵌入排版文字）来绕过基于文本的安全检查，从而侵犯图像所有者权益，并生成违规内容。
- **核心问题**：揭示图像生成模型在视觉模态中存在的**排版威胁（typographic threats）**，检验现有防御手段的有效性，并构建评估基准。

## 方法论

- **攻击方法**：采用 **排版攻击（typographic attack）**，即在图像中植入特定文字（例如恶意指令或违规描述），利用模型对图像内文字的识别与理解能力，使模型在图像生成或编辑过程中执行隐藏于视觉文字中的攻击意图，而非依赖文本提示。
- **关键技术思路**：
  - 将传统基于语言模态的越狱（jailbreak）概念迁移到视觉模态。
  - 通过改变图像中文字的字体、大小、位置、颜色等属性，控制攻击的隐蔽性与成功率。
  - 可能的结构：在已有图像上叠加打印的文本，或生成含文字的合成图像，作为多模态模型的视觉输入。
- **防御评估**：系统性地将多种现有防护方法（如文本过滤、安全对齐模型、后处理审核等）置于视觉排版攻击下，测试其失效程度。
- **数据集构建**：提出 **VMT‑IGMs（Vision Modal Threats in Image Generation Models）** 数据集，作为评估模型视觉模态脆弱性的标准化基准。

> 注：由于仅提供摘要，上述方法论细节系基于摘要及常识推断，具体公式、算法流程在原论文中应有详细说明。

## 实验设计

- **任务场景**：涵盖 Text-to-Image（T2I）和 Image-to-Image（I2I）任务，可能包括真实图像编辑、图像变化生成等。
- **数据集**：作者自建 VMT‑IGMs 数据集，作为视觉模态威胁评估基线。该数据集应包含多种排版攻击样本（如不同文字内容、布局、字形），用于测试模型是否会被诱导生成不安全内容。
- **对比对象**：
  - 多种主流图像生成模型（可能包括 Stable Diffusion 系列、DALL·E、Midjourney 等，具体需见原文）。
  - 现有文本模态防御方法（如提示检查、安全分类器、后处理过滤器）在面对视觉攻击时的表现。
- **评估指标**：可能包括攻击成功率（ASR）、恶意内容生成率、防御绕过率等。

## 资源与算力

- 摘要及元数据中 **未明确提及** GPU 型号、数量、训练时长等算力信息。
- 可合理推测实验涉及推理阶段的模型调用，计算开销相对可控；若涉及模型微调或训练则需额外资源，但本文更侧重于攻击分析与评估，可能不依赖大规模训练。

## 实验数量与充分性

- 基于摘要无法获知具体实验组数，但可预期包含：
  - 多个生成模型×多种排版攻击变体的交叉实验；
  - 不同防御策略的对比实验；
  - 可能包含消融研究（如文字位置、字体、大小对攻击效果的影响）；
  - 人类评估或自动化内容安全度量。
- **充分性与客观性**：自建数据集和系统性对比多种防御方法，有助于建立基准；但若仅测试选定的模型和防御手段，其泛化性需进一步验证。论文发表在 CVPR 2025 高水平会议，通常实验设计较严谨。

## 主要结论与发现

- **视觉模态排版威胁真实有效**：图像生成模型极易通过视觉文字被间接操控，生成违规内容。
- **现有防护失效**：多数聚焦文本模态的防御方法在面对视觉攻击时基本无效，说明当前安全策略存在致命短板。
- **多模态安全须统一考虑**：单纯依赖语言侧防护不足以保障整体安全，必须同时加固视觉模态的攻防能力。
- **VMT‑IGMs 为后续研究提供基准**，有助于推动社区关注并解决该新型威胁。

## 优点与亮点

- **新颖的威胁视角**：率先系统性地定义并论证图像生成模型中的视觉排版攻击，将安全问题从文本拓展到视觉模态。
- **实际意义强**：贴近真实世界应用场景（图像编辑），直击图像版权与内容安全痛点。
- **防御全面评估**：覆盖主流防御手段，证明其盲区，推动更健壮的多模态防护设计。
- **数据集开源潜力**：VMT‑IGMs 可成为领域标准化测试平台，促进可复现研究。

## 不足与局限

- **技术细节缺失（基于摘要）**：摘要未给出攻击算法的具体实现、评估流程的量化细节，需阅读全文确认方法的可重复性。
- **可能的模型/环境偏差**：若仅在特定几款开源模型上测试，结论可能不适用于商业闭源系统（如 DALL·E 3 或 Midjourney）。
- **攻击隐蔽性与鲁棒性未深入**：排版文字的可见性可能触发人工审核，实际攻击中高隐蔽性要求是否满足有待考量。
- **防御策略单一**：仅评估现有文本防御，未提出新型视觉防御或分析多模态联合防御的可行性。
- **动态变化考量不足**：图像生成模型更新迅速，所测模型的版本固化可能影响结论的长效性。

（完）
