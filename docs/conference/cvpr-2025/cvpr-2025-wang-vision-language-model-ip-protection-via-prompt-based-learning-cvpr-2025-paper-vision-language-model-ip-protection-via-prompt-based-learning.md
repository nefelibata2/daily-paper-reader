---
title: Vision-Language Model IP Protection via Prompt-based Learning
title_zh: 基于提示学习的视觉语言模型知识产权保护
authors: "Wang, Lianyu, Wang, Meng, Fu, Huazhu, Zhang, Daoqiang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_Vision-Language_Model_IP_Protection_via_Prompt-based_Learning_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 4.0
evidence: 通过提示学习实现视觉语言模型的知识产权保护
tldr: 针对视觉语言模型（VLM）的知识产权保护需求，本文提出IP-CLIP方法，利用提示学习为CLIP嵌入IP信息，限定模型仅对授权数据域生效。该方法不修改视觉编码器，轻量高效，实验证明能有效防止未授权微调和部署，为VLM商业应用提供安全保障。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-vision-language-model-ip-protection-via-prompt-based-learning-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 849, \"height\": 332, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-vision-language-model-ip-protection-via-prompt-based-learning-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1594, \"height\": 845, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-vision-language-model-ip-protection-via-prompt-based-learning-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 621, \"height\": 302, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-vision-language-model-ip-protection-via-prompt-based-learning-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 873, \"height\": 169, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-vision-language-model-ip-protection-via-prompt-based-learning-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 874, \"height\": 183, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-vision-language-model-ip-protection-via-prompt-based-learning-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1810, \"height\": 510, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-vision-language-model-ip-protection-via-prompt-based-learning-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1808, \"height\": 563, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-vision-language-model-ip-protection-via-prompt-based-learning-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 875, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-vision-language-model-ip-protection-via-prompt-based-learning-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1810, \"height\": 511, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-vision-language-model-ip-protection-via-prompt-based-learning-cvpr-2025-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1810, \"height\": 509, \"label\": \"Table\"}]"
motivation: 当前VLM模型易被未经授权使用或微调，现有IP保护方法多依赖单一视觉特征，安全性和效率不足，亟需更灵活的保护机制。
method: 提出IP-CLIP，基于提示学习策略，在冻结的视觉编码器上学习域特定的提示，实现轻量级IP保护，限制模型只能在授权域内工作。
result: 实验显示，IP-CLIP能有效阻止未授权域使用，带IP保护的模型在目标域保持高性能，且对多种微调攻击具有鲁棒性。
conclusion: 该方法为VLM提供了高效的IP保护方案，有助于推动大型视觉语言模型在商业和隐私敏感场景中的安全部署。
---

## Abstract
Vision-language models (VLMs) like CLIP (Contrastive Language-Image Pre-Training) have seen remarkable success in visual recognition, highlighting the increasing need to safeguard the intellectual property (IP) of well-trained models. Effective IP protection extends beyond ensuring authorized usage; it also necessitates restricting model deployment to authorized data domains, particularly when the model is fine-tuned for specific target domains. However, current IP protection methods often rely solely on the visual backbone, which may lack sufficient semantic richness. To bridge this gap, we introduce IP-CLIP, a lightweight IP protection strategy tailored to CLIP, employing a prompt-based learning approach. By leveraging the frozen visual backbone of CLIP, we extract both image style and content information, incorporating them into the learning of IP prompt. This strategy acts as a robust barrier, effectively preventing the unauthorized transfer of features from authorized domains to unauthorized ones. Additionally, we propose a style-enhancement branch that constructs feature banks for both authorized and unauthorized domains. This branch integrates self-enhanced and cross-domain features, further strengthening IP-CLIP's capability to block features from unauthorized domains. Finally, we present new three metrics designed to better balance the performance degradation of authorized and unauthorized domains. Comprehensive experiments in various scenarios demonstrate its promising potential for application in IP protection tasks for VLMs.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过提示学习实现视觉语言模型的知识产权保护。

### 2. 核心内容
针对视觉语言模型（VLM）的知识产权保护需求，本文提出IP-CLIP方法，利用提示学习为CLIP嵌入IP信息，限定模型仅对授权数据域生效。该方法不修改视觉编码器，轻量高效，实验证明能有效防止未授权微调和部署，为VLM商业应用提供安全保障。

### 3. 对应检索需求
security threats and defenses for large language models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Wang_Vision-Language_Model_IP_Protection_via_Prompt-based_Learning_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Wang_Vision-Language_Model_IP_Protection_via_Prompt-based_Learning_CVPR_2025_paper.html)
