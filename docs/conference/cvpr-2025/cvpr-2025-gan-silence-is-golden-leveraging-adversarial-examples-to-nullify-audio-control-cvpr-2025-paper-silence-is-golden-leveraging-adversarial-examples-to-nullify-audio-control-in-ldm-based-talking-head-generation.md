---
title: "Silence is Golden: Leveraging Adversarial Examples to Nullify Audio Control in LDM-based Talking-Head Generation"
title_zh: 沉默是金：利用对抗样本使LDM虚拟人视频音频控制失效
authors: "Gan, Yuan, Miao, Jiaxu, Wang, Yunze, Yang, Yi"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Gan_Silence_is_Golden_Leveraging_Adversarial_Examples_to_Nullify_Audio_Control_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 7.0
evidence: 针对LDM虚拟人视频生成的主动防御方法
tldr: 针对基于潜在扩散模型的虚拟人生成视频可能被滥用于诈骗和虚假信息等安全风险，本文提出利用对抗样本来干扰音频控制，使生成视频质量大幅下降，从而保护肖像不被恶意利用。该方法结合空间、时间和扩散攻击模块，在保持图像不可察觉扰动的同时有效阻止视频生成，为主动防御AI生成滥用提供了新思路。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 891, \"height\": 834, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1798, \"height\": 896, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 812, \"height\": 248, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1788, \"height\": 808, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1789, \"height\": 614, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 867, \"height\": 646, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1776, \"height\": 487, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 850, \"height\": 435, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1773, \"height\": 527, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gan-silence-is-golden-leveraging-adversarial-examples-to-nullify-audio-control-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 847, \"height\": 376, \"label\": \"Table\"}]"
motivation: 虚拟人生成视频的真实性引发安全担忧，现有防御方法对音频操控无效。
method: 将对抗攻击功能化为空间、时间和扩散攻击模块，施加不可察觉扰动使生成视频质量退化。
result: 实验证明该方法能有效降低生成视频质量，阻止肖像滥用。
conclusion: 提出了一种主动防御方法，通过对抗样本保护用户免受虚拟人视频生成滥用的威胁。
---

## Abstract
Advances in talking-head animation based on Latent Diffusion Models (LDM) enable the creation of highly realistic, synchronized videos. These fabricated videos are indistinguishable from real ones, increasing the risk of potential misuse for scams, political manipulation, and misinformation. Hence, addressing these ethical concerns has become a pressing issue in AI security. Recent proactive defense studies focused on countering LDM-based models by adding perturbations to portraits. However, these methods are ineffective at protecting reference portraits from advanced image-to-video animation. The limitations are twofold: 1) they fail to prevent images from being manipulated by audio signals, and 2) diffusion-based purification techniques can effectively eliminate protective perturbations. To address these challenges, we propose Silencer, a two-stage method designed to proactively protect the privacy of portraits. First, a nullifying loss is proposed to ignore audio control in talking-head generation. Second, we apply anti-purification loss in LDM to optimize the inverted latent feature to generate robust perturbations. Extensive experiments demonstrate the effectiveness of Silencer in proactively protecting portrait privacy. We hope this work will raise awareness among the AI security community regarding critical ethical issues related to talking-head generation techniques. Code: https://github.com/yuangan/Silencer.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
针对LDM虚拟人视频生成的主动防御方法。

### 2. 核心内容
针对基于潜在扩散模型的虚拟人生成视频可能被滥用于诈骗和虚假信息等安全风险，本文提出利用对抗样本来干扰音频控制，使生成视频质量大幅下降，从而保护肖像不被恶意利用。该方法结合空间、时间和扩散攻击模块，在保持图像不可察觉扰动的同时有效阻止视频生成，为主动防御AI生成滥用提供了新思路。

### 3. 对应检索需求
security vulnerabilities of generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Gan_Silence_is_Golden_Leveraging_Adversarial_Examples_to_Nullify_Audio_Control_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Gan_Silence_is_Golden_Leveraging_Adversarial_Examples_to_Nullify_Audio_Control_CVPR_2025_paper.html)
