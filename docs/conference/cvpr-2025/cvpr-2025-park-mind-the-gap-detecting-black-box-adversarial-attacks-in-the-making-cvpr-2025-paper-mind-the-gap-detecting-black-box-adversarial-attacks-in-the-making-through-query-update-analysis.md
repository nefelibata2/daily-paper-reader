---
title: "Mind the Gap: Detecting Black-box Adversarial Attacks in the Making through Query Update Analysis"
title_zh: 留心差距：通过查询更新分析检测生成中的黑盒对抗攻击
authors: "Park, Jeonghwan, McLaughlin, Niall, Alouani, Ihsen"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Park_Mind_the_Gap_Detecting_Black-box_Adversarial_Attacks_in_the_Making_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 6.0
evidence: 检测进行中的黑盒对抗攻击，提供机器学习模型防御
tldr: 对抗攻击对机器学习模型构成严重威胁，现有防御常被自适应攻击突破。本文提出一种新框架，通过监测查询更新序列的相似性空间，学习攻击生成过程中的模式，从而在攻击完成前进行检测。该方法不依赖具体模型架构，在黑盒设置下有效防御多种先进攻击，为主动式攻击防御提供了新思路。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 864, \"height\": 309, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1794, \"height\": 638, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 384, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 867, \"height\": 298, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1783, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 833, \"height\": 327, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 873, \"height\": 393, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 847, \"height\": 246, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 867, \"height\": 298, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 889, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 893, \"height\": 341, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 855, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 820, \"height\": 299, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 900, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 748, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-park-mind-the-gap-detecting-black-box-adversarial-attacks-in-the-making-cvpr-2025-paper/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 864, \"height\": 292, \"label\": \"Table\"}]"
motivation: 黑盒对抗攻击因无需了解模型内部而难以防御，现有检测方法多在攻击完成后识别，缺乏在攻击生成阶段的主动拦截手段。
method: 利用攻击查询更新的相似性模式，训练模型识别攻击状态，在攻击噪声生成过程中即实现检测，无需依赖输入空间监测。
result: 实验表明，该方法能提前检测到多种黑盒攻击的生成，防御成功率显著优于传统状态检测方法，且对自适应攻击具有泛化能力。
conclusion: 该工作将防御时机前移，为对抗攻击防御开辟了新的主动检测范式，增强了ML模型在实际部署中的安全性。
---

## Abstract
Adversarial attacks remain a significant threat that can jeopardize the integrity of Machine Learning (ML) models. In particular, query-based black-box attacks can generate malicious noise without having access to the victim model's architecture, making them practical in real-world contexts. The community has proposed several defenses against adversarial attacks, only to be broken by more advanced and adaptive attack strategies. In this paper, we propose a framework that detects if an adversarial noise instance is being generated. Unlike existing stateful defenses that detect adversarial noise generation by monitoring the input space, our approach learns adversarial patterns in the input update similarity space. In fact, we propose to observe a new metric called Delta Similarity (DS), which we show it captures more efficiently the adversarial behavior.We evaluate our approach against 8 state-of-the-art attacks, including adaptive attacks, where the adversary is aware of the defense and tries to evade detection. We find that our approach is significantly more robust than existing defenses both in terms of specificity and sensitivity.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
检测进行中的黑盒对抗攻击，提供机器学习模型防御。

### 2. 核心内容
对抗攻击对机器学习模型构成严重威胁，现有防御常被自适应攻击突破。本文提出一种新框架，通过监测查询更新序列的相似性空间，学习攻击生成过程中的模式，从而在攻击完成前进行检测。该方法不依赖具体模型架构，在黑盒设置下有效防御多种先进攻击，为主动式攻击防御提供了新思路。

### 3. 对应检索需求
security threats and defenses for large language models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Park_Mind_the_Gap_Detecting_Black-box_Adversarial_Attacks_in_the_Making_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Park_Mind_the_Gap_Detecting_Black-box_Adversarial_Attacks_in_the_Making_CVPR_2025_paper.html)
