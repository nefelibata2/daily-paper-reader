---
title: "T2ISafety: Benchmark for Assessing Fairness, Toxicity, and Privacy in Image Generation"
title_zh: T2ISafety：评估图像生成公平性、毒性和隐私的基准
authors: "Li, Lijun, Shi, Zhelun, Hu, Xuhao, Dong, Bowen, Qin, Yiran, Liu, Xihui, Sheng, Lu, Shao, Jing"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Li_T2ISafety_Benchmark_for_Assessing_Fairness_Toxicity_and_Privacy_in_Image_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 8.0
evidence: 评估文本到图像生成隐私风险的基准
tldr: 本文构建T2ISafety基准，全面评估文本到图像模型在毒性、公平性和隐私方面的安全性。该基准包含12个任务、44个类别和7万条提示，揭示了当前模型在生成有害、偏见或隐私内容方面的风险，为生成模型的安全评估提供了标准化工具，推动负责任AI发展。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-t2isafety-benchmark-for-assessing-fairness-toxicity-and-privacy-in-image-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1784, \"height\": 882, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-t2isafety-benchmark-for-assessing-fairness-toxicity-and-privacy-in-image-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1727, \"height\": 788, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-t2isafety-benchmark-for-assessing-fairness-toxicity-and-privacy-in-image-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1531, \"height\": 518, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-t2isafety-benchmark-for-assessing-fairness-toxicity-and-privacy-in-image-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1441, \"height\": 309, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-t2isafety-benchmark-for-assessing-fairness-toxicity-and-privacy-in-image-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 518, \"height\": 397, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-t2isafety-benchmark-for-assessing-fairness-toxicity-and-privacy-in-image-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1530, \"height\": 499, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-t2isafety-benchmark-for-assessing-fairness-toxicity-and-privacy-in-image-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 890, \"height\": 524, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-t2isafety-benchmark-for-assessing-fairness-toxicity-and-privacy-in-image-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1530, \"height\": 316, \"label\": \"Table\"}]"
motivation: 文本到图像模型存在安全风险，现有评估不全面。
method: 构建多层次安全基准，涵盖毒性、公平性、隐私，收集7万提示。
result: 揭示模型在多个安全维度上的不足。
conclusion: 为生成模型安全评估提供了全面基准。
---

## Abstract
Text-to-image (T2I) models have rapidly advanced, enabling the generation of high-quality images from text prompts across various domains. However, these models present notable safety concerns, including the risk of generating harmful, biased, or private content. Current research on assessing T2I safety remains in its early stages. While some efforts have been made to evaluate models on specific safety dimensions, many critical risks remain unexplored. To address this gap, we introduce T2ISafety, a safety benchmark that evaluates T2I models across three key domains: toxicity, fairness, and bias. We build a detailed hierarchy of 12 tasks and 44 categories based on these three domains, and meticulously collect 70K corresponding prompts. Based on this taxonomy and prompt set, we build a large-scale T2I dataset with 68K manually annotated images and train an evaluator capable of detecting critical risks that previous work has failed to identify, including risks that even ultra-large proprietary models like GPTs cannot correctly detect. We evaluate 15 prominent diffusion models on T2ISafety and reveal several concerns including persistent issues with racial fairness, a tendency to generate toxic content, and significant variation in privacy protection across the models, even with defense methods like concept erasing.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估文本到图像生成隐私风险的基准。

### 2. 核心内容
本文构建T2ISafety基准，全面评估文本到图像模型在毒性、公平性和隐私方面的安全性。该基准包含12个任务、44个类别和7万条提示，揭示了当前模型在生成有害、偏见或隐私内容方面的风险，为生成模型的安全评估提供了标准化工具，推动负责任AI发展。

### 3. 对应检索需求
privacy risks in generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Li_T2ISafety_Benchmark_for_Assessing_Fairness_Toxicity_and_Privacy_in_Image_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Li_T2ISafety_Benchmark_for_Assessing_Fairness_Toxicity_and_Privacy_in_Image_CVPR_2025_paper.html)
