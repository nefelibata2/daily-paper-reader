---
title: Towards All-in-One Medical Image Re-Identification
title_zh: 迈向全能型医学图像再识别
authors: "Tian, Yuan, Ji, Kaiyuan, Zhang, Rongzhao, Jiang, Yankai, Li, Chunyi, Wang, Xiaosong, Zhai, Guangtao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Tian_Towards_All-in-One_Medical_Image_Re-Identification_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 7.0
evidence: 为医学图像再识别提供统一模型，支持医疗隐私保护
tldr: 医学图像再识别在个性化医疗和隐私保护中至关重要但研究不足。本文建立统一基准，并提出基于连续模态参数适配器（ComPA）的统一模型，能动态处理多种医学模态数据，结合医学先验知识，实现了高效准确的再识别，为医学AI中的隐私保护技术提供了新工具。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 712, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1802, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 832, \"height\": 321, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 816, \"height\": 329, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 879, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1802, \"height\": 1184, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 868, \"height\": 79, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 867, \"height\": 125, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 866, \"height\": 192, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 866, \"height\": 172, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 854, \"height\": 98, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-tian-towards-all-in-one-medical-image-re-identification-cvpr-2025-paper/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 864, \"height\": 244, \"label\": \"Table\"}]"
motivation: 医学图像再识别对隐私保护和个性化医疗至关重要，但缺乏统一基准和模型。
method: 提出基于连续模态参数适配器的统一模型，动态学习模态特定参数，并融合医学基础模型先验。
result: 在多种医学模态数据集上取得了领先的再识别性能，展现了统一的跨模态能力。
conclusion: 为医学隐私保护提供了一种高效统一的再识别方案，推动了个性化医疗发展。
---

## Abstract
Medical image re-identification (MedReID) is under-explored so far, despite its critical applications in personalized healthcare and privacy protection.In this paper, we introduce a thorough benchmark and a unified model for this problem.First, to handle various medical modalities, we propose a novel Continuous Modality-based Parameter Adapter (ComPA). ComPA condenses medical content into a continuous modality representation and dynamically adjusts the modality-agnostic model with modality-specific parameters at runtime. This allows a single model to adaptively learn and process diverse modality data.Furthermore, we integrate medical priors into our model by aligning it with a bag of pre-trained medical foundation models, in terms of the differential features.Compared to single-image feature, modeling the inter-image difference better fits the re-identification problem, which involves discriminating multiple images.We evaluate the proposed model against 25 foundation models and 8 large multi-modal language models across 11 image datasets, demonstrating consistently superior performance.Additionally, we deploy the proposed MedReID technique to two real-world applications, i.e., history-augmented personalized diagnosis and medical privacy protection.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
为医学图像再识别提供统一模型，支持医疗隐私保护。

### 2. 核心内容
医学图像再识别在个性化医疗和隐私保护中至关重要但研究不足。本文建立统一基准，并提出基于连续模态参数适配器（ComPA）的统一模型，能动态处理多种医学模态数据，结合医学先验知识，实现了高效准确的再识别，为医学AI中的隐私保护技术提供了新工具。

### 3. 对应检索需求
privacy preserving techniques for medical AI and generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Tian_Towards_All-in-One_Medical_Image_Re-Identification_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Tian_Towards_All-in-One_Medical_Image_Re-Identification_CVPR_2025_paper.html)
