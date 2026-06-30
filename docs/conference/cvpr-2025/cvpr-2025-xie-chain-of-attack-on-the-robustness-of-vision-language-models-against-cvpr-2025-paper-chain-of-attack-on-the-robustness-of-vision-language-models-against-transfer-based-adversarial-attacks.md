---
title: "Chain of Attack: On the Robustness of Vision-Language Models Against Transfer-Based Adversarial Attacks"
title_zh: 攻击链：视觉语言模型对迁移对抗攻击的鲁棒性研究
authors: "Xie, Peng, Bie, Yequan, Mao, Jianda, Song, Yangqiu, Wang, Yang, Chen, Hao, Chen, Kani"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Xie_Chain_of_Attack_On_the_Robustness_of_Vision-Language_Models_Against_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 8.0
evidence: 评估基于迁移的对抗攻击对视觉语言模型的安全鲁棒性
tldr: 本文针对视觉语言模型（VLM）的安全鲁棒性，提出链式攻击方法，利用视觉与文本间的语义相关性增强迁移攻击。实验表明该方法能更有效地使VLM生成有害内容，暴露了现有模型在对抗攻击下的脆弱性，为提升多模态大模型的安全性提供了评估手段和防御方向。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xie-chain-of-attack-on-the-robustness-of-vision-language-models-against-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 845, \"height\": 635, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xie-chain-of-attack-on-the-robustness-of-vision-language-models-against-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1776, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xie-chain-of-attack-on-the-robustness-of-vision-language-models-against-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1779, \"height\": 956, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xie-chain-of-attack-on-the-robustness-of-vision-language-models-against-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1786, \"height\": 1039, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xie-chain-of-attack-on-the-robustness-of-vision-language-models-against-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1796, \"height\": 684, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-chain-of-attack-on-the-robustness-of-vision-language-models-against-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1804, \"height\": 1441, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-chain-of-attack-on-the-robustness-of-vision-language-models-against-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1696, \"height\": 412, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xie-chain-of-attack-on-the-robustness-of-vision-language-models-against-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 787, \"height\": 364, \"label\": \"Table\"}]"
motivation: VLM应用广泛，但其对抗攻击鲁棒性值得担忧。
method: 提出链式攻击，利用语义相关性增强迁移攻击。
result: 成功使VLM生成有毒内容，揭示安全漏洞。
conclusion: 为多模态大模型安全评估提供了新方法。
---

## Abstract
Pre-trained vision-language models (VLMs) have showcased remarkable performance in image and natural language understanding, such as image captioning and response generation. As the practical applications of VLMs become increasingly widespread, their potential safety and robustness issues raise concerns that adversaries may evade the system and cause these models to generate toxic content through malicious attacks. Therefore, evaluating the robustness of open-source VLMs against adversarial attacks has garnered growing attention, with transfer-based attacks as a representative black-box attacking strategy. However, most existing transfer-based attacks neglect the importance of the semantic correlations between vision and text modalities, leading to sub-optimal adversarial example generation and attack performance. To address this issue, we present Chain of Attack (CoA), which iteratively enhances the generation of adversarial examples based on the multi-modal semantic update using a series of intermediate attacking steps, achieving superior adversarial transferability and efficiency. A unified attack success rate computing method is further proposed for automatic evasion evaluation. Extensive experiments conducted under the most realistic and high-stakes scenario, demonstrate that our attacking strategy is able to effectively mislead models to generate targeted responses using only black-box attacks without any knowledge of the victim models. The comprehensive robustness evaluation in our paper provides insight into the vulnerabilities of VLMs and offers a reference for the safety considerations of future model developments.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
评估基于迁移的对抗攻击对视觉语言模型的安全鲁棒性。

### 2. 核心内容
本文针对视觉语言模型（VLM）的安全鲁棒性，提出链式攻击方法，利用视觉与文本间的语义相关性增强迁移攻击。实验表明该方法能更有效地使VLM生成有害内容，暴露了现有模型在对抗攻击下的脆弱性，为提升多模态大模型的安全性提供了评估手段和防御方向。

### 3. 对应检索需求
security threats and defenses for large language models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Xie_Chain_of_Attack_On_the_Robustness_of_Vision-Language_Models_Against_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Xie_Chain_of_Attack_On_the_Robustness_of_Vision-Language_Models_Against_CVPR_2025_paper.html)
