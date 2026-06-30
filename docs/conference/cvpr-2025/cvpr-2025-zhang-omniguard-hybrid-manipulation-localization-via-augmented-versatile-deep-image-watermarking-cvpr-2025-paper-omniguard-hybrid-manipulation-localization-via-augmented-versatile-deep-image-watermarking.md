---
title: "OmniGuard: Hybrid Manipulation Localization via Augmented Versatile Deep Image Watermarking"
title_zh: "OmniGuard: 通过增强通用深度水印实现混合篡改定位"
authors: "Zhang, Xuanyu, Tang, Zecheng, Xu, Zhipei, Li, Runyi, Xu, Youmin, Chen, Bin, Gao, Feng, Zhang, Jian"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Zhang_OmniGuard_Hybrid_Manipulation_Localization_via_Augmented_Versatile_Deep_Image_Watermarking_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 6.0
evidence: 针对AI生成图像编辑的版权保护与篡改定位水印方法
tldr: 随着生成式AI图像编辑的普及，数字内容的真实性和完整性面临挑战。本文提出OmniGuard水印方案，融合主动嵌入与被动盲提取，实现稳健版权保护和篡改定位，克服了传统水印在定位精度和视觉质量上的权衡，在AIGC编辑场景下展现出优越性能。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 881, \"height\": 252, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1796, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1796, \"height\": 884, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1812, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1718, \"height\": 738, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 867, \"height\": 229, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 823, \"height\": 189, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1627, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1809, \"height\": 499, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 783, \"height\": 189, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-omniguard-hybrid-manipulation-localization-via-augmented-versatile-deep-image-watermarking-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 786, \"height\": 182, \"label\": \"Table\"}]"
motivation: 生成式AI图像编辑带来内容真实性和完整性的安全风险。
method: 设计增强型通用水印方法，结合主动嵌入与盲提取实现篡改定位。
result: 实验表明OmniGuard在版权提取准确率和篡改定位精度上优于现有方法。
conclusion: 提供了一种有效的AIGC内容保护水印方案，兼顾鲁棒性与不可见性。
---

## Abstract
With the rapid growth of generative AI and its widespread application in image editing, new risks have emerged regarding the authenticity and integrity of digital content. Existing versatile watermarking approaches suffer from trade-offs between tamper localization precision and visual quality. Constrained by the limited flexibility of previous framework, their localized watermark must remain fixed across all images. Under AIGC-editing, their copyright extraction accuracy is also unsatisfactory. To address these challenges, we propose OmniGuard, a novel augmented versatile watermarking approach that integrates proactive embedding with passive, blind extraction for robust copyright protection and tamper localization. OmniGuard employs a hybrid forensic framework that enables flexible localization watermark selection and introduces a degradation-aware tamper extraction network for precise localization under challenging conditions. Additionally, a lightweight AIGC-editing simulation layer is designed to enhance robustness across global and local editing. Extensive experiments show that OmniGuard achieves superior fidelity, robustness, and flexibility. Compared to the recent state-of-the-art approach EditGuard, our method outperforms it by 4.25dB in PSNR of the container image, 20.7% in F1-Score under noisy conditions, and 14.8% in average bit accuracy.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
针对AI生成图像编辑的版权保护与篡改定位水印方法。

### 2. 核心内容
随着生成式AI图像编辑的普及，数字内容的真实性和完整性面临挑战。本文提出OmniGuard水印方案，融合主动嵌入与被动盲提取，实现稳健版权保护和篡改定位，克服了传统水印在定位精度和视觉质量上的权衡，在AIGC编辑场景下展现出优越性能。

### 3. 对应检索需求
security vulnerabilities of generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Zhang_OmniGuard_Hybrid_Manipulation_Localization_via_Augmented_Versatile_Deep_Image_Watermarking_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Zhang_OmniGuard_Hybrid_Manipulation_Localization_via_Augmented_Versatile_Deep_Image_Watermarking_CVPR_2025_paper.html)
