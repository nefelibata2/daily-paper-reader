---
title: Harnessing Global-Local Collaborative Adversarial Perturbation for Anti-Customization
title_zh: 利用全局-局部协同对抗扰动进行抗定制
authors: "Xu, Long, Wang, Jiakai, Hao, Haojie, Qin, Haotong, Zhao, Jiejie, Liu, Xianglong"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Xu_Harnessing_Global-Local_Collaborative_Adversarial_Perturbation_for_Anti-Customization_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 8.0
evidence: 抗定制框架保护潜在扩散模型免受面部盗用等未授权滥用
tldr: 本文提出GoodAC框架，针对潜在扩散模型（LDM）的未授权定制滥用风险，利用全局-局部协同对抗扰动增强防御能力。该方法同时考虑全局特征相关性和局部面部属性，有效抵抗概念转移和语义盗用，相比现有方法显著提升了对个性化图像合成中隐私侵犯的防护效果。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-harnessing-global-local-collaborative-adversarial-perturbation-for-anti-customization-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 860, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-harnessing-global-local-collaborative-adversarial-perturbation-for-anti-customization-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1805, \"height\": 708, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-harnessing-global-local-collaborative-adversarial-perturbation-for-anti-customization-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1792, \"height\": 626, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-harnessing-global-local-collaborative-adversarial-perturbation-for-anti-customization-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 861, \"height\": 262, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xu-harnessing-global-local-collaborative-adversarial-perturbation-for-anti-customization-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 861, \"height\": 424, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-harnessing-global-local-collaborative-adversarial-perturbation-for-anti-customization-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1808, \"height\": 578, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-harnessing-global-local-collaborative-adversarial-perturbation-for-anti-customization-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1809, \"height\": 579, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-harnessing-global-local-collaborative-adversarial-perturbation-for-anti-customization-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 866, \"height\": 305, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xu-harnessing-global-local-collaborative-adversarial-perturbation-for-anti-customization-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 873, \"height\": 339, \"label\": \"Table\"}]"
motivation: 现有抗定制方法防御不足，忽视层次特征。
method: 提出GoodAC框架，生成全局-局部协同的对抗扰动。
result: 有效抵抗概念转移和语义盗用，防护能力增强。
conclusion: 为生成模型的定制滥用提供了更强防御。
---

## Abstract
Though achieving significant success in personalized image synthesis, Latent Diffusion Models (LDMs) pose substantial social risks caused by unauthorized misuse (e.g., face theft). To counter these threats, the Anti-Customization (AC) method that exploits adversarial perturbations was proposed. Unfortunately, existing AC methods show insufficient defense ability due to the ignorance of hierarchical characteristics, i.e., global feature correlations and local facial attributes, leading to weak resistance to concept transfer and semantic theft in customization methods. To address these limitations, we are motivated to propose a **G**lobal-L**o**cal c**o**llaborate**d** Anti-Customization (GoodAC) framework to generate powerful adversarial perturbations by disturbing both feature correlations and facial attributes. To enhance the ability to resist concept transfer, we disrupt the spatial correlation of perceptual features that form the basis of model generation at a global level, thereby creating highly concept-transfer-resistant adversarial camouflage. To improve the ability to resist semantic theft, leveraging the fact that facial attributes are personalized, we designed a personalized and precise facial attribute distortion strategy locally, focusing the attack on the individual's image structure to generate strong camouflage. Extensive experiments on various customization methods, including Dreambooth and LoRA, have strongly demonstrated that our GoodAC outperforms other state-of-the-art approaches by large margins, e.g., over 50% improvements on ISM.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
抗定制框架保护潜在扩散模型免受面部盗用等未授权滥用。

### 2. 核心内容
本文提出GoodAC框架，针对潜在扩散模型（LDM）的未授权定制滥用风险，利用全局-局部协同对抗扰动增强防御能力。该方法同时考虑全局特征相关性和局部面部属性，有效抵抗概念转移和语义盗用，相比现有方法显著提升了对个性化图像合成中隐私侵犯的防护效果。

### 3. 对应检索需求
security vulnerabilities of generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Xu_Harnessing_Global-Local_Collaborative_Adversarial_Perturbation_for_Anti-Customization_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Xu_Harnessing_Global-Local_Collaborative_Adversarial_Perturbation_for_Anti-Customization_CVPR_2025_paper.html)
