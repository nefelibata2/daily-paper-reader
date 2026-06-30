---
title: Invisible Backdoor Attack against Self-supervised Learning
title_zh: 针对自监督学习的不可见后门攻击
authors: "Zhang, Hanrong, Wang, Zhenting, Li, Boheng, Lin, Fulin, Han, Tingxu, Jin, Mingyu, Zhan, Chenlu, Du, Mengnan, Wang, Hongwei, Ma, Shiqing"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Zhang_Invisible_Backdoor_Attack_against_Self-supervised_Learning_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 5.0
evidence: 针对SSL模型的不可见后门攻击，揭示安全漏洞
tldr: 自监督学习模型易受后门攻击，但现有隐形触发器常失效。本文发现其原因是后门分布与SSL数据增强分布重叠，进而设计了一种与增强变换解耦的优化触发器，实现不可见且有效的后门攻击，暴露了自监督模型的安全隐患。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 771, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1796, \"height\": 508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 442, \"height\": 445, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 869, \"height\": 396, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 831, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 854, \"height\": 350, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1811, \"height\": 428, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 625, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 649, \"height\": 229, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 800, \"height\": 271, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-invisible-backdoor-attack-against-self-supervised-learning-cvpr-2025-paper/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 807, \"height\": 151, \"label\": \"Table\"}]"
motivation: 现有SSL后门攻击显眼且易被检测，需要不可见攻击方法。
method: 分析SSL中后门失效原因，设计解耦增强变换的优化触发器。
result: 成功实现不可见后门攻击，攻击成功率较高。
conclusion: 发现自监督学习存在严重后门漏洞，需重视其安全性。
---

## Abstract
Self-supervised learning (SSL) models are vulnerable to backdoor attacks. Existing backdoor attacks that are effective in SSL often involve noticeable triggers, like colored patches or visible noise, which are vulnerable to human inspection. This paper proposes an imperceptible and effective backdoor attack against self-supervised models. We first find that existing imperceptible triggers designed for supervised learning are less effective in compromising self-supervised models. We then identify this ineffectiveness is attributed to the overlap in distributions between the backdoor and augmented samples used in SSL. Building on this insight, we design an attack using optimized triggers disentangled with the augmented transformation in the SSL, while remaining imperceptible to human vision. Experiments on five datasets and six SSL algorithms demonstrate our attack is highly effective and stealthy. It also has strong resistance to existing backdoor defenses. Our code can be found at https://github.com/Zhang-Henry/INACTIVE.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
针对SSL模型的不可见后门攻击，揭示安全漏洞。

### 2. 核心内容
自监督学习模型易受后门攻击，但现有隐形触发器常失效。本文发现其原因是后门分布与SSL数据增强分布重叠，进而设计了一种与增强变换解耦的优化触发器，实现不可见且有效的后门攻击，暴露了自监督模型的安全隐患。

### 3. 对应检索需求
security vulnerabilities of generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Zhang_Invisible_Backdoor_Attack_against_Self-supervised_Learning_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Zhang_Invisible_Backdoor_Attack_against_Self-supervised_Learning_CVPR_2025_paper.html)
