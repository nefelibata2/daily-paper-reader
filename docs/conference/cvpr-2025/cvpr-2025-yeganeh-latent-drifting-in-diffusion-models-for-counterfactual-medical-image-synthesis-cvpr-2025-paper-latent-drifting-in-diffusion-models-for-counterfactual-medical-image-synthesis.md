---
title: Latent Drifting in Diffusion Models for Counterfactual Medical Image Synthesis
title_zh: 扩散模型中的潜在漂移用于反事实医学图像合成
authors: "Yeganeh, Yousef, Farshad, Azade, Charisiadis, Ioannis, Hasny, Marta, Hartenberger, Martin, Ommer, Björn, Navab, Nassir, Adeli, Ehsan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Yeganeh_Latent_Drifting_in_Diffusion_Models_for_Counterfactual_Medical_Image_Synthesis_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 8.0
evidence: 通过支持有限数据微调应对医学影像隐私障碍
tldr: 针对医学影像因隐私和成本问题导致大数据难以获取的挑战，提出潜在漂移（Latent Drift）方法，支持在数据受限时对扩散模型进行微调或作为推理条件，缓解分布偏移，促进隐私受限场景下的医学图像合成。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1751, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 866, \"height\": 407, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1782, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1723, \"height\": 818, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 642, \"height\": 276, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1743, \"height\": 265, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 851, \"height\": 1378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1563, \"height\": 515, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1525, \"height\": 596, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 861, \"height\": 599, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 610, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-yeganeh-latent-drifting-in-diffusion-models-for-counterfactual-medical-image-synthesis-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 610, \"height\": 204, \"label\": \"Table\"}]"
motivation: 医学影像领域因隐私问题难以获取大规模数据集，限制了扩散模型的合成能力。
method: 提出潜在漂移（LD）方法，可集成到任何微调方法中，缓解分布偏移。
result: 在有限数据条件下，LD能提升扩散模型医学图像合成的质量与真实性。
conclusion: LD为隐私敏感的医学AI应用提供了一种实用的生成技术路径。
---

## Abstract
Scaling by training on large datasets has been shown to enhance the quality and fidelity of image generation and manipulation with diffusion models; however, such large datasets are not always accessible in medical imaging due to cost and privacy issues, which contradicts one of the main applications of such models to produce synthetic samples where real data is scarce. Also, finetuning on pre-trained general models has been a challenge due to the distribution shift between the medical domain and the pre-trained models. Here, we propose Latent Drift (LD) for diffusion models that can be adopted for any fine-tuning method to mitigate the issues faced by the distribution shift or employed in inference time as a condition. Latent Drifting enables diffusion models to be conditioned for medical images fitted for the complex task of counterfactual image generation, which is crucial to investigate how parameters such as gender, age, and adding or removing diseases in a patient would alter the medical images. We evaluate our method on three public longitudinal benchmark datasets of brain MRI and chest X-rays for counterfactual image generation. Our results demonstrate significant performance gains in various scenarios when combined with different fine-tuning schemes. The source code of this work is available on GitHub.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过支持有限数据微调应对医学影像隐私障碍。

### 2. 核心内容
针对医学影像因隐私和成本问题导致大数据难以获取的挑战，提出潜在漂移（Latent Drift）方法，支持在数据受限时对扩散模型进行微调或作为推理条件，缓解分布偏移，促进隐私受限场景下的医学图像合成。

### 3. 对应检索需求
privacy preserving techniques for medical AI and generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Yeganeh_Latent_Drifting_in_Diffusion_Models_for_Counterfactual_Medical_Image_Synthesis_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Yeganeh_Latent_Drifting_in_Diffusion_Models_for_Counterfactual_Medical_Image_Synthesis_CVPR_2025_paper.html)
