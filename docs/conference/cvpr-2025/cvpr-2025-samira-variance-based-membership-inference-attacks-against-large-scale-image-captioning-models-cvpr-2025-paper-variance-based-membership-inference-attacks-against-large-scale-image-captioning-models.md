---
title: Variance-Based Membership Inference Attacks Against Large-Scale Image Captioning Models
title_zh: 针对大规模图像描述模型的方差基成员推理攻击
authors: "Samira, Daniel, Habler, Edan, Elovici, Yuval, Shabtai, Asaf"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Samira_Variance-Based_Membership_Inference_Attacks_Against_Large-Scale_Image_Captioning_Models_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 图像描述模型的成员推理攻击揭示隐私风险
tldr: 本文研究多模态图像描述模型的成员推理攻击，利用方差策略仅凭图像数据推断训练样本成员身份。实验证实此类模型存在记忆和敏感信息泄露风险，揭示了生成模型在隐私保护方面的脆弱性，为后续防御机制设计提供了重要参考。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 826, \"height\": 447, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 759, \"height\": 289, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 812, \"height\": 428, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 598, \"height\": 462, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 570, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 864, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 829, \"height\": 662, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 836, \"height\": 477, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1802, \"height\": 301, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1772, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-samira-variance-based-membership-inference-attacks-against-large-scale-image-captioning-models-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1779, \"height\": 467, \"label\": \"Table\"}]"
motivation: 多模态生成模型可能泄露训练数据中的敏感信息。
method: 提出基于方差的成员推理攻击，仅用图像数据推断。
result: 成功揭露图像描述模型的隐私泄露风险。
conclusion: 对生成模型的隐私安全性提出了警示。
---

## Abstract
The proliferation of multi-modal generative models has introduced new privacy and security challenges, especially due to the risks of memorization and unintentional disclosure of sensitive information. This paper focuses on the vulnerability of multi-modal image captioning models to membership inference attacks (MIAs). These models, which synthesize textual descriptions from visual content, could inadvertently reveal personal or proprietary data embedded in their training datasets. We explore the feasibility of MIAs in the context of such models. Specifically, our approach leverages a variance-based strategy tailored for image captioning models, utilizing only image data without knowing the corresponding caption. We introduce the means-of-variance threshold attack (MVTA) and confidence-based weakly supervised attack (C-WSA) based on the metric, means-of-variance (MV), to assess variability among vector embeddings. Our experiments demonstrate that these models are susceptible to MIAs, indicating substantial privacy risks. The effectiveness of our methods is validated through rigorous evaluations on these real-world models, confirming the practical implications of our findings.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
图像描述模型的成员推理攻击揭示隐私风险。

### 2. 核心内容
本文研究多模态图像描述模型的成员推理攻击，利用方差策略仅凭图像数据推断训练样本成员身份。实验证实此类模型存在记忆和敏感信息泄露风险，揭示了生成模型在隐私保护方面的脆弱性，为后续防御机制设计提供了重要参考。

### 3. 对应检索需求
privacy risks in generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Samira_Variance-Based_Membership_Inference_Attacks_Against_Large-Scale_Image_Captioning_Models_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Samira_Variance-Based_Membership_Inference_Attacks_Against_Large-Scale_Image_Captioning_Models_CVPR_2025_paper.html)
