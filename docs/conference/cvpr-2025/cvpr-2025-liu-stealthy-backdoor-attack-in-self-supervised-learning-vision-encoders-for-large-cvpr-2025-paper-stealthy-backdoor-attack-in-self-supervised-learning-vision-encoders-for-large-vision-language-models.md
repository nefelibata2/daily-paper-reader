---
title: Stealthy Backdoor Attack in Self-Supervised Learning Vision Encoders for Large Vision Language Models
title_zh: 针对大视觉语言模型中自监督学习视觉编码器的隐身后门攻击
authors: "Liu, Zhaoyi, Zhang, Huan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Liu_Stealthy_Backdoor_Attack_in_Self-Supervised_Learning_Vision_Encoders_for_Large_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 8.0
evidence: 针对大语言模型中视觉编码器的后门攻击，构成安全威胁
tldr: 自监督视觉编码器被广泛用于构建大视觉语言模型（LVLM），本文提出BadVision攻击，通过污染视觉编码器引入后门，使下游LVLMs在特定触发条件下产生显著视觉幻觉，且该后门会因编码器共享而广泛传播。实验验证了攻击的有效性和隐蔽性，凸显了LVLM供应链中的严重安全威胁。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-stealthy-backdoor-attack-in-self-supervised-learning-vision-encoders-for-large-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 858, \"height\": 478, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-stealthy-backdoor-attack-in-self-supervised-learning-vision-encoders-for-large-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 868, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-stealthy-backdoor-attack-in-self-supervised-learning-vision-encoders-for-large-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 864, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-stealthy-backdoor-attack-in-self-supervised-learning-vision-encoders-for-large-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1759, \"height\": 475, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-stealthy-backdoor-attack-in-self-supervised-learning-vision-encoders-for-large-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1812, \"height\": 841, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-stealthy-backdoor-attack-in-self-supervised-learning-vision-encoders-for-large-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1567, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liu-stealthy-backdoor-attack-in-self-supervised-learning-vision-encoders-for-large-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 742, \"height\": 486, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-stealthy-backdoor-attack-in-self-supervised-learning-vision-encoders-for-large-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 743, \"height\": 381, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-stealthy-backdoor-attack-in-self-supervised-learning-vision-encoders-for-large-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 753, \"height\": 249, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liu-stealthy-backdoor-attack-in-self-supervised-learning-vision-encoders-for-large-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 847, \"height\": 457, \"label\": \"Table\"}]"
motivation: 视觉编码器被多个LVLM复用，其安全性隐患可能导致后门广泛传播。
method: 提出BadVision，在SSL视觉编码器中植入隐蔽后门，触发LVLMs视觉幻觉。
result: 实验证明后门可跨模型传播，产生一致且隐蔽的幻觉攻击效果。
conclusion: 揭示了LVLM视觉编码器复用带来的严重安全威胁，需加强供应链安全。
---

## Abstract
Self-supervised learning (SSL) vision encoders learn high-quality image representations and thus have become a vital part of developing vision modality of large vision language models (LVLMs). Due to the high cost of training such encoders, pre-trained encoders are widely shared and deployed into many LVLMs, which are security-critical or bear societal significance. Under this practical scenario, we reveal a new backdoor threat that significant visual hallucinations can be induced into these LVLMs by merely compromising vision encoders. Because of the sharing and reuse of these encoders, many downstream LVLMs may inherit backdoor behaviors from encoders, leading to widespread backdoors. In this work, we propose BadVision, the first method to exploit this vulnerability in SSL vision encoders for LVLMs with novel trigger optimization and backdoor learning techniques. We evaluate BadVision on two types of SSL encoders and LVLMs across eight benchmarks. We show that BadVision effectively drives the LVLMs to attacker-chosen hallucination with over 99% attack success rate, causing a 77.6% relative visual understanding error while maintaining the stealthiness. SoTA backdoor detection methods cannot detect our attack effectively.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
针对大语言模型中视觉编码器的后门攻击，构成安全威胁。

### 2. 核心内容
自监督视觉编码器被广泛用于构建大视觉语言模型（LVLM），本文提出BadVision攻击，通过污染视觉编码器引入后门，使下游LVLMs在特定触发条件下产生显著视觉幻觉，且该后门会因编码器共享而广泛传播。实验验证了攻击的有效性和隐蔽性，凸显了LVLM供应链中的严重安全威胁。

### 3. 对应检索需求
security threats and defenses for large language models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Liu_Stealthy_Backdoor_Attack_in_Self-Supervised_Learning_Vision_Encoders_for_Large_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Liu_Stealthy_Backdoor_Attack_in_Self-Supervised_Learning_Vision_Encoders_for_Large_CVPR_2025_paper.html)
