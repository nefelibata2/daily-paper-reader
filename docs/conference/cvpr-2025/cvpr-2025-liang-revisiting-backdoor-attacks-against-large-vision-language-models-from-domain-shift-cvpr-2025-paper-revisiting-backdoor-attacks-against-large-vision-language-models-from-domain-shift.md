---
title: Revisiting Backdoor Attacks against Large Vision-Language Models from Domain Shift
title_zh: 从域偏移角度重新审视大型视觉语言模型的后门攻击
authors: "Liang, Siyuan, Liang, Jiawei, Pang, Tianyu, Du, Chao, Liu, Aishan, Zhu, Mingli, Cao, Xiaochun, Tao, Dacheng"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Liang_Revisiting_Backdoor_Attacks_against_Large_Vision-Language_Models_from_Domain_Shift_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 8.0
evidence: 研究跨域迁移下大型视觉语言模型的后门攻击漏洞及泛化因素
tldr: 本文研究指令微调下大型视觉语言模型的后门攻击在训练与测试域不匹配时的泛化能力，提出后门域泛化评估维度，发现域无关触发模式有利于攻击泛化，为生成式视觉语言模型的安全漏洞分析提供了新见解。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 864, \"height\": 516, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1777, \"height\": 838, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1812, \"height\": 477, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 869, \"height\": 955, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 835, \"height\": 279, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 860, \"height\": 385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 818, \"height\": 361, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1621, \"height\": 220, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 364, \"height\": 334, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1799, \"height\": 378, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liang-revisiting-backdoor-attacks-against-large-vision-language-models-from-domain-shift-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 864, \"height\": 337, \"label\": \"Table\"}]"
motivation: 指令微调增加LVLM漏洞，但现有后门攻击研究局限于静态设定，未考虑域偏移下的泛化性。
method: 引入后门域泛化评估维度，分析视觉和文本域偏移下触发模式与干净语义区的竞争关系。
result: 揭示域无关触发模式和模型无关特征能提升攻击泛化性，触发模式与语义区存在竞争。
conclusion: 为评估和设计鲁棒后门攻击提供了新视角，强调了域独立性在攻击泛化中的关键作用。
---

## Abstract
Instruction tuning enhances large vision-language models (LVLMs) but increases their vulnerability to backdoor attacks due to their open design. Unlike prior studies in static settings, this paper explores backdoor attacks in LVLM instruction tuning across mismatched training and testing domains. We introduce a new evaluation dimension, backdoor domain generalization, to assess attack robustness under visual and text domain shifts. Our findings reveal two insights: (1) backdoor generalizability improves when distinctive trigger patterns are independent of specific data domains or model architectures, and (2) the competitive interaction between trigger patterns and clean semantic regions, where guiding the model to predict triggers enhances attack generalizability. Based on these insights, we propose a multimodal attribution backdoor attack (MABA) that injects domain-agnostic triggers into critical areas using attributional interpretation. Experiments with OpenFlamingo, Blip-2, and Otter show that MABA significantly boosts the attack success rate of generalization by 36.4% over the unimodal attack, achieving a 97% success rate at a 0.2% poisoning rate. This study reveals limitations in current evaluations and highlights how enhanced backdoor generalizability poses a security threat to LVLMs, even without test data access.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
研究跨域迁移下大型视觉语言模型的后门攻击漏洞及泛化因素。

### 2. 核心内容
本文研究指令微调下大型视觉语言模型的后门攻击在训练与测试域不匹配时的泛化能力，提出后门域泛化评估维度，发现域无关触发模式有利于攻击泛化，为生成式视觉语言模型的安全漏洞分析提供了新见解。

### 3. 对应检索需求
security vulnerabilities of generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Liang_Revisiting_Backdoor_Attacks_against_Large_Vision-Language_Models_from_Domain_Shift_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Liang_Revisiting_Backdoor_Attacks_against_Large_Vision-Language_Models_from_Domain_Shift_CVPR_2025_paper.html)
