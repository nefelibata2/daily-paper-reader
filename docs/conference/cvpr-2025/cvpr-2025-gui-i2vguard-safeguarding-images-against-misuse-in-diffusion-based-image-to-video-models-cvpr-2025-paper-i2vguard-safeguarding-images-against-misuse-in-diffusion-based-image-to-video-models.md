---
title: "I2VGuard: Safeguarding Images against Misuse in Diffusion-based Image-to-Video Models"
title_zh: "I2VGuard: 保护图像免受扩散图像转视频模型滥用"
authors: "Gui, Dongnan, Guo, Xun, Zhou, Wengang, Lu, Yan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Gui_I2VGuard_Safeguarding_Images_against_Misuse_in_Diffusion-based_Image-to-Video_Models_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 8.0
evidence: 通过对抗扰动保护图像免受扩散图像转视频模型滥用
tldr: 图像到视频生成模型可能被滥用以侵犯隐私和版权。本文提出I2VGuard，通过对图像施加人眼不可见的对抗扰动，使生成的视频质量严重退化，从而保护图像免受白盒扩散模型滥用。该方法结合空间、时间和扩散攻击模块，在保持图像视觉质量的同时有效防止恶意视频生成。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gui-i2vguard-safeguarding-images-against-misuse-in-diffusion-based-image-to-video-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1786, \"height\": 959, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gui-i2vguard-safeguarding-images-against-misuse-in-diffusion-based-image-to-video-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1742, \"height\": 885, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gui-i2vguard-safeguarding-images-against-misuse-in-diffusion-based-image-to-video-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 858, \"height\": 251, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gui-i2vguard-safeguarding-images-against-misuse-in-diffusion-based-image-to-video-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1721, \"height\": 1517, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gui-i2vguard-safeguarding-images-against-misuse-in-diffusion-based-image-to-video-models-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1714, \"height\": 1423, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-gui-i2vguard-safeguarding-images-against-misuse-in-diffusion-based-image-to-video-models-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 866, \"height\": 332, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gui-i2vguard-safeguarding-images-against-misuse-in-diffusion-based-image-to-video-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 875, \"height\": 1144, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gui-i2vguard-safeguarding-images-against-misuse-in-diffusion-based-image-to-video-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1799, \"height\": 218, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-gui-i2vguard-safeguarding-images-against-misuse-in-diffusion-based-image-to-video-models-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 858, \"height\": 153, \"label\": \"Table\"}]"
motivation: 图像转视频扩散模型存在隐私和版权滥用风险。
method: 施加不可见对抗扰动，集成空间、时间和扩散攻击模块以破坏视频生成。
result: 实验验证该方法大幅降低生成视频质量，保护图像不被滥用。
conclusion: 提出了一种主动防御框架，有效应对图像转视频生成模型的滥用威胁。
---

## Abstract
Recent advances in image-to-video generation have enabled animation of still images and offered pixel-level controllability. While these models hold great potential to transform single images into vivid and dynamic videos, they also carry risks of misuse that could impact privacy, security, and copyright protection. This paper proposes a novel approach that applies imperceptible perturbations on images to degrade the quality of the generated videos, thereby protecting images from misuse in white-box image-to-video diffusion models. Specifically, we function our approach as an adversarial attack, incorporating spatial, temporal, and diffusion attack modules. The spatial attack shifts image features from their original distribution to a lower-quality target distribution, reducing visual fidelity. The temporal attack disrupts coherent motion by interfering with temporal attention maps that guide motion generation. To enhance the robustness of our approach across different models, we further propose a diffusion attack module leveraging contrastive loss. Our approach can be easily integrated with mainstream diffusion-based I2V models. Extensive experiments on SVD, CogVideoX, and ControlNeXt demonstrate that our method significantly impairs generation quality in terms of visual clarity and motion consistency, while introducing only minimal artifacts to the images. To the best of our knowledge, we are the first to explore adversarial attacks on image-to-video generation for security purposes.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过对抗扰动保护图像免受扩散图像转视频模型滥用。

### 2. 核心内容
图像到视频生成模型可能被滥用以侵犯隐私和版权。本文提出I2VGuard，通过对图像施加人眼不可见的对抗扰动，使生成的视频质量严重退化，从而保护图像免受白盒扩散模型滥用。该方法结合空间、时间和扩散攻击模块，在保持图像视觉质量的同时有效防止恶意视频生成。

### 3. 对应检索需求
privacy risks in generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Gui_I2VGuard_Safeguarding_Images_against_Misuse_in_Diffusion-based_Image-to-Video_Models_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Gui_I2VGuard_Safeguarding_Images_against_Misuse_in_Diffusion-based_Image-to-Video_Models_CVPR_2025_paper.html)
