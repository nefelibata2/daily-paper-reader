---
title: Nearly Zero-Cost Protection Against Mimicry by Personalized Diffusion Models
title_zh: 近乎零成本的个性化扩散模型防模仿保护
authors: "Ahn, Namhyuk, Yoo, KiYoon, Ahn, Wonhyuk, Kim, Daesik, Nam, Seung-Hun"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Ahn_Nearly_Zero-Cost_Protection_Against_Mimicry_by_Personalized_Diffusion_Models_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 7.0
evidence: 保护图像免遭个性化扩散模型模仿，应对隐私与滥用风险
tldr: 个性化扩散模型可能被用来模仿他人图像，导致隐私泄露和盗用。本文提出基于扰动预训练和混合扰动策略的高效图像保护方法，显著降低延迟并提升扰动不可见性，同时保持强保护能力。实验表明，该方法在计算开销近乎为零的情况下实现了同等的防模仿效果。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1788, \"height\": 439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1810, \"height\": 922, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 868, \"height\": 450, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 868, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1792, \"height\": 637, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1790, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1797, \"height\": 477, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 829, \"height\": 453, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1788, \"height\": 427, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 506, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1803, \"height\": 296, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ahn-nearly-zero-cost-protection-against-mimicry-by-personalized-diffusion-models-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1201, \"height\": 313, \"label\": \"Table\"}]"
motivation: 扩散模型易被用于模仿他人图像，现有保护方法无法兼顾效果、不可见性和延迟。
method: 通过扰动预训练减少延迟，提出混合扰动方法动态适应图像，并在多个VAE特征空间计算保护损失。
result: 实验显示保护性能相当，不可见性更好，延迟大幅降低。
conclusion: 提出一种高效且低延迟的图像保护方案，有效防止个性化扩散模型的模仿攻击。
---

## Abstract
Recent advancements in diffusion models revolutionize image generation but pose risks of misuse, such as replicating artworks or generating deepfakes. Existing image protection methods, though effective, struggle to balance protection efficacy, invisibility, and latency, thus limiting practical use. We introduce perturbation pre-training to reduce latency and propose a mixture-of-perturbations approach that dynamically adapts to input images to minimize performance degradation. Our novel training strategy computes protection loss across multiple VAE feature spaces, while adaptive targeted protection at inference enhances robustness and invisibility. Experiments show comparable protection performance with improved invisibility and drastically reduced inference time.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
保护图像免遭个性化扩散模型模仿，应对隐私与滥用风险。

### 2. 核心内容
个性化扩散模型可能被用来模仿他人图像，导致隐私泄露和盗用。本文提出基于扰动预训练和混合扰动策略的高效图像保护方法，显著降低延迟并提升扰动不可见性，同时保持强保护能力。实验表明，该方法在计算开销近乎为零的情况下实现了同等的防模仿效果。

### 3. 对应检索需求
privacy risks in generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Ahn_Nearly_Zero-Cost_Protection_Against_Mimicry_by_Personalized_Diffusion_Models_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Ahn_Nearly_Zero-Cost_Protection_Against_Mimicry_by_Personalized_Diffusion_Models_CVPR_2025_paper.html)
