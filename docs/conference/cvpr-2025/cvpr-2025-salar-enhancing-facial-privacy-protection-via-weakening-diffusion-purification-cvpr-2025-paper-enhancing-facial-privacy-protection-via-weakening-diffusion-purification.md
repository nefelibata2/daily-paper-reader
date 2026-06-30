---
title: Enhancing Facial Privacy Protection via Weakening Diffusion Purification
title_zh: 通过削弱扩散纯化增强面部隐私保护
authors: "Salar, Ali, Liu, Qing, Tian, Yingli, Zhao, Guoying"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Salar_Enhancing_Facial_Privacy_Protection_via_Weakening_Diffusion_Purification_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 利用对抗扩散保护面部隐私以对抗未授权识别
tldr: 针对现有基于扩散模型的面部隐私保护因扩散纯化效应导致保护成功率低的问题，提出学习无条件嵌入以增强对抗修改能力，从而显著提升对自动人脸识别的防御效果，维护肖像隐私。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1615, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 149, \"height\": 150, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1620, \"height\": 697, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 808, \"height\": 647, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 855, \"height\": 381, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 730, \"height\": 351, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 866, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 845, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 683, \"height\": 387, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1810, \"height\": 507, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 875, \"height\": 351, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-salar-enhancing-facial-privacy-protection-via-weakening-diffusion-purification-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 705, \"height\": 127, \"label\": \"Table\"}]"
motivation: 现有扩散模型生成对抗面部图像保护隐私的方法受扩散纯化影响，保护成功率低。
method: 提出学习无条件嵌入，引导扩散模型生成更强对抗样本。
result: 削弱扩散纯化后，面部隐私保护成功率大幅提升。
conclusion: 为社交媒体中的面部隐私保护提供了一种更有效的技术方案。
---

## Abstract
The rapid growth of social media has led to the widespread sharing of individual portrait images, which pose serious privacy risks due to the capabilities of automatic face recognition (AFR) systems for mass surveillance. Hence, protecting facial privacy against unauthorized AFR systems is essential. Inspired by the generation capability of the emerging diffusion models, recent methods employ diffusion models to generate adversarial face images for privacy protection. However, they suffer from the diffusion purification effect, leading to a low protection success rate (PSR). In this paper, we first propose learning unconditional embeddings to increase the learning capacity for adversarial modifications and then use them to guide the modification of the adversarial latent code to weaken the diffusion purification effect. Moreover, we integrate an identity-preserving structure to maintain structural consistency between the original and generated images, allowing human observers to recognize the generated image as having the same identity as the original. Extensive experiments conducted on two public datasets, i.e., CelebA-HQ and LADN, demonstrate the superiority of our approach. The protected faces generated by our method outperform those produced by existing facial privacy protection approaches in terms of transferability and natural appearance. The code is available at https://github.com/parham1998/Facial-Privacy-Protection

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：社交媒体上大量个人肖像照片的分享使得人们面临严重的隐私泄露风险。未经授权的自动人脸识别（AFR）系统能够轻易地对这些图片进行大规模身份识别与监控。
- **核心问题**：现有的隐私保护方法利用扩散模型生成对抗性人脸图像以误导人脸识别系统，但这类方法存在“扩散纯化效应”（Diffusion Purification Effect），导致生成的对抗样本在扩散逆过程中被“净化”，保护成功率（PSR）低下。
- **整体含义**：本文旨在通过削弱扩散纯化效应，提升对抗性人脸图像的保护能力，同时保持图像的自然外观和身份一致性，为社交媒体环境下的人脸隐私提供更有效的技术方案。

## 2. 方法论

- **核心思想**：以削弱扩散纯化效应为目标，增强扩散模型生成强对抗性修改的能力，并维持生成图像与原始图像的身份关联。
- **关键技术细节**：
  - **学习无条件嵌入（Unconditional Embeddings）**：为提升模型对对抗性修改的学习容量，提出学习一组专门的无条件嵌入向量，用于指导扩散过程的潜码修改方向。
  - **对抗潜码引导修改**：利用学到的无条件嵌入，干预和调整扩散模型在潜空间中的采样过程，引导生成更具攻击性、不易被纯化的对抗特征。
  - **身份保持结构（Identity-Preserving Structure）**：在模型中集成身份保持模块，确保最终生成的“隐私保护人脸”与原始人脸在人类视觉感知上属于同一身份，避免外观严重失真。
- **算法流程简述**：给定原始人脸图像 → 通过身份保持结构提取身份特征 → 在扩散潜空间中加入学习到的无条件嵌入 → 进行对抗性潜码修改 → 经过削弱纯化的扩散过程生成保护图像。

## 3. 实验设计

- **使用数据集**：
  - CelebA‑HQ（高质量人脸数据集）
  - LADN（面部属性数据集，常用于低光照/自然场景）
- **对比方法（Benchmark）**：与现有主流的基于扩散模型的人脸隐私保护方法进行对比（摘要中未列出具体方法名，但明确包括“existing facial privacy protection approaches”）。
- **评估场景/指标**：
  - **保护成功率（PSR）**：衡量对抗样本成功欺骗人脸识别系统的比率。
  - **可迁移性**：对抗图像在不同人脸识别模型间的泛化攻击能力。
  - **自然外观**：生成图像的主观/客观质量，确保人眼可识别为同一人。

## 4. 资源与算力

- **算力信息**：论文提供的元数据及摘要中**未明确说明**所使用的GPU型号、数量、训练时长或总计算量。无法确认实验的具体资源消耗。

## 5. 实验数量与充分性

- **实验覆盖**：至少在两个公开数据集上进行了“广泛实验”，并给出了与现有方法的比较结果。同时，从消融研究需求看，方法涉及“无条件嵌入”、“身份保持结构”等模块，推断很可能包含消融实验以验证各组件的作用（文中未列出具体组数）。
- **充分性与公平性**：
  - 数据集使用两个不同场景的人脸数据集，增加了结果的可信度。
  - 对比对象明确为同一任务下的现有前沿方法，比较基础公平。
  - 但缺少关于实验重复次数、统计显著性检验以及更多元化评估指标（如结构相似度SSIM、FID等）的明确描述，使实验充分性难以从现有信息中完全评判。

## 6. 论文的主要结论与发现

- 提出的削弱扩散纯化方法能够显著**提升人脸隐私保护的成功率**，突破传统扩散模型因纯化效应导致的保护瓶颈。
- 生成的受保护人脸图像同时具备**良好的可迁移性**（可抵御不同识别模型）和**自然的视觉效果**（人类观察者仍可识别原身份）。
- 技术框架为社交媒体中的个人肖像隐私保护提供了一种更有效、更实用的对抗策略。

## 7. 优点

- **创新性强**：直击扩散模型用于对抗攻击时的固有问题“纯化效应”，提出针对性削弱策略。
- **效果显著**：在保护成功率和图像自然度上均优于现有方法，兼顾安全性与可用性。
- **设计精妙**：通过学习无条件嵌入增强对抗修改自由度，并加入身份保持结构，平衡了攻击强度与视觉保真度。
- **开源可用**：代码公开在GitHub，便于复现和后续研究。

## 8. 不足与局限

- **实验覆盖有限**：仅在两个公开数据集上验证，真实社交媒体环境中多样的人脸采集条件（极端光照、大角度、遮挡等）未被充分测试。
- **威胁模型单一**：专注防御自动人脸识别，未讨论对其他滥用形式（如人脸属性推断、深度伪造）的防护效果。
- **攻击对象局限**：对抗攻击主要针对特定的人脸识别模型，面对未知或更强的识别架构时，保护成功率可能下降（尽管文中强调了可迁移性）。
- **用户感知平衡**：虽保证人类可识别身份，但对抗扰动可能带来不易察觉的伪影，对高质量肖像需求场景的接受度未做用户研究。
- **资源需求未知**：缺少算力报告，无法评估方法的部署门槛和效率。

（完）
