---
title: Fingerprinting Denoising Diffusion Probabilistic Models
title_zh: 去噪扩散概率模型指纹
authors: "Teng, Huan, Quan, Yuhui, Wang, Chengyu, Huang, Jun, Ji, Hui"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Teng_Fingerprinting_Denoising_Diffusion_Probabilistic_Models_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 7.0
evidence: 面向DDPM的非侵入式指纹用于知识产权保护
tldr: 本文针对去噪扩散概率模型（DDPM）的知识产权保护问题，提出首个非侵入式指纹方案。该方法无需修改模型参数或微调，通过设计基于“交叉路径”的判别性和鲁棒性指纹潜在空间，在保持生成质量的同时有效标识模型身份，为生成式AI的版权保护提供了一种无损且高效的新途径。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 852, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 750, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 830, \"height\": 330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 861, \"height\": 336, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 846, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 827, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1728, \"height\": 883, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 857, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 867, \"height\": 496, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 848, \"height\": 708, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 941, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 867, \"height\": 1419, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-teng-fingerprinting-denoising-diffusion-probabilistic-models-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 839, \"height\": 1028, \"label\": \"Table\"}]"
motivation: 扩散模型知识产权保护需求迫切，现有方法侵入性强。
method: 设计基于交叉路径的指纹潜在空间，实现非侵入式DDPM指纹。
result: 无需参数修改，保持生成质量，有效识别模型。
conclusion: 为生成模型提供了一种无损的IP保护方法。
---

## Abstract
Diffusion models, especially denoising diffusion probabilistic models (DDPMs), are prevalent tools in generative AI, making their intellectual property (IP) protection increasingly important. Most existing IP protection methods for DDPMs are invasive, e.g., model watermarking, which alter model parameters and raise concerns about performance degradation, also with requirement for extra computational resources for retraining or fine-tuning. In this paper, we propose the first non-invasive fingerprinting scheme for DDPMs, requiring no parameter changes or fine-tuning, and keeping generation quality intact. We introduce a discriminative and robust fingerprint latent space based on the well-designed "crossing route" of noisy samples that span the performance border-zone of DDPMs, with only black-box access required for the diffusion denoiser in ownership verification. Extensive experiments demonstrate that our fingerprinting approach enjoys both robustness against the often-seen attacks and distinctiveness on various DDPMs, providing an alternative for protecting DDPMs' IP rights without compromising their performance or integrity.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向DDPM的非侵入式指纹用于知识产权保护。

### 2. 核心内容
本文针对去噪扩散概率模型（DDPM）的知识产权保护问题，提出首个非侵入式指纹方案。该方法无需修改模型参数或微调，通过设计基于“交叉路径”的判别性和鲁棒性指纹潜在空间，在保持生成质量的同时有效标识模型身份，为生成式AI的版权保护提供了一种无损且高效的新途径。

### 3. 对应检索需求
security vulnerabilities of generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Teng_Fingerprinting_Denoising_Diffusion_Probabilistic_Models_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Teng_Fingerprinting_Denoising_Diffusion_Probabilistic_Models_CVPR_2025_paper.html)
