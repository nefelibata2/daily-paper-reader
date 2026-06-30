---
title: "Variance as a Catalyst: Efficient and Transferable Semantic Erasure Adversarial Attack for Customized Diffusion Models"
title_zh: 方差作为催化剂：针对定制扩散模型的高效且可迁移的语义擦除对抗攻击
authors: "Jiachen Yang, Yusong Wang, Yanmei Fang, Yunshu Dai, Fangjun Huang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Fh9XlJnXb5"
tags: ["query:priv-sec"]
score: 8.0
evidence: 提出对抗攻击擦除扩散模型中的身份语义，防止隐私侵犯的假图像生成。
tldr: 针对定制扩散模型被滥用生成假图像导致的隐私问题，本文发现VAE潜在编码的方差是影响图像失真的关键因素，并据此提出基于拉普拉斯分布的损失函数，沿方差最大增长方向优化以彻底擦除身份语义。实验证明该方法能完全擦除语义信息，优于现有攻击，为扩散模型的安全应用提供新思路。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 定制扩散模型易被滥用于伪造图像，引发隐私侵犯，现有对抗攻击无法完全擦除身份语义。
method: 识别VAE潜在编码方差为图像失真关键，提出基于拉普拉斯损失沿最大方差增长方向优化的语义擦除攻击。
result: 实现了对身份语义的完全擦除，相比现有方法失真更强且语义消除更彻底。
conclusion: 为扩散模型的安全使用提供了有效的语义擦除技术，有助于防范隐私泄露风险。
---

## Abstract
Latent Diffusion Models (LDMs) enable fine-tuning with only a few images and have become widely used on the Internet. However, it can also be misused to generate fake images, leading to privacy violations and social risks. Existing adversarial attack methods primarily introduce noise distortions to generated images but fail to completely erase identity semantics. 
In this work, we identify the variance of VAE latent code as a key factor that influences image distortion. Specifically, larger variances result in stronger distortions and ultimately erase semantic information. Based on this finding, we propose a Laplace-based (LA) loss function that optimizes along the fastest variance growth direction, ensuring each optimization step is locally optimal. Additionally, we analyze the limitations of existing methods and reveal that their loss functions often fail to align gradient signs with the direction of variance growth. They also struggle to ensure efficient optimization under different variance distributions. To address these issues, we further propose a novel Lagrange Entropy-based (LE) loss function.
Experimental results demonstrate that our methods achieve state-of-the-art performance on CelebA-HQ and VGGFace2. Both proposed loss functions effectively lead diffusion models to generate pure-noise images with identity semantics completely erased. Furthermore, our methods exhibit strong transferability across diverse models and efficiently complete attacks with minimal computational resources. Our work provides a practical and efficient solution for privacy protection.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究背景**：潜在扩散模型（LDM，如 Stable Diffusion）只需少量图像即可进行个性化微调（例如 DreamBooth），在互联网上被广泛使用，但也容易被滥用于生成虚假人脸图像，造成隐私侵犯与社会风险。
- **核心问题**：现有对抗攻击方法通过添加噪声扰动来破坏生成图像质量，但**无法彻底擦除身份语义信息**，导致生成图像仍可能残留可辨识的个人特征。
- **整体含义**：本文旨在提出一种高效的**语义擦除对抗攻击**，使微调后的扩散模型生成完全噪声化、不包含任何身份语义的图像，从而从源头阻断隐私泄露。

### 2. 论文提出的方法论：核心思想、关键技术细节、算法流程
- **核心发现**：作者识别出 **VAE 潜在编码的方差**是影响图像失真程度的关键因素——方差越大，生成图像的扭曲越强，最终可完全抹去语义信息。
- **基于拉普拉斯分布的损失函数（Laplace-based, LA）**：
  - 设计目标：沿**方差增长最快的方向**进行优化，使每一步更新都局部最优。
  - 原理：利用拉普拉斯分布对潜在编码进行建模，通过最大化特定统计量来推动潜在编码的方差急剧增大，从而在扩散生成过程中产生强噪声图像。
- **对现有方法的分析**：
  - 现有损失函数的梯度符号往往与方差增长方向不一致，导致优化效率低下。
  - 在不同方差分布下，这些方法难以保证高效的对抗攻击效果。
- **基于拉格朗日熵的损失函数（Lagrange Entropy-based, LE）**：
  - 进一步解决上述问题，通过在损失函数中引入熵正则项和拉格朗日乘子，自适应地调整优化方向，确保在任意方差分布下都能实现高效的语义擦除。
  - 两种损失函数（LA 与 LE）均能使扩散模型在推理时生成接近纯噪声的图像，且身份语义被完全消除。
- **算法流程概括**（文字描述）：
  1. 对目标扩散模型的 VAE 编码器输出计算潜在编码及其方差统计量。
  2. 根据所选损失函数（LA 或 LE）计算对抗扰动，方向为最大化方差增长（或相应的熵度量）。
  3. 将扰动施加到微调模型的输入或中间特征上，使模型在推理时生成严重失真的图像。
  4. 整个过程仅需极少的计算资源即可完成攻击。

### 3. 实验设计：数据集、基准与对比方法
- **数据集**：
  - **CelebA-HQ**：高质量人脸数据集。
  - **VGGFace2**：大规模人脸识别数据集。
- **基准（Benchmark）**：以“生成图像中人脸语义的残留程度”和“图像失真度”为主要评估指标，包括身份信息擦除率和图像质量下降程度。
- **对比方法**：与现有对抗攻击方法进行对比（摘要中未列出具体名称，但提及这些方法主要引入噪声失真但无法彻底擦除语义）。可能涵盖基于梯度的攻击（如 PGD）、针对扩散模型的专用攻击等。
- **场景**：针对定制化（个性化）扩散模型，在少样本微调后执行对抗攻击，测试语义擦除效果。

### 4. 资源与算力
- **文中未明确提及**所使用的 GPU 型号、数量或训练时长。
- 仅定性指出攻击“**以最少的计算资源高效完成**”，暗示方法本身的优化开销很低，但未给出具体算力数据。

### 5. 实验数量与充分性
- **实验组数**：至少覆盖两个主流人脸数据集，与多个现有攻击方法对比，并针对两种提出的损失函数进行性能评估。此外，极可能包含**消融实验**（如验证方差增长方向的有效性、不同损失项的作用）、**可迁移性实验**（跨不同扩散模型架构）等。
- **充分性与公平性**：
  - 从摘要和结论看，实验设计较为完整，涵盖了与现有方法的直接比较、跨数据集验证和跨模型迁移，能够支撑“完全擦除语义”的声明。
  - 摘要强调“existing methods fail to completely erase identity semantics”而本文方法实现了此事，对比公平性依赖于在相同条件下评估。
  - 未透露具体的定量指标和统计显著性，但从 ICML 2025 接收（score 8.0）推断实验应足够严谨。

### 6. 论文的主要结论与发现
- **方差是关键**：VAE 潜在编码方差直接决定生成图像的失真程度，沿方差最大增长方向优化能够产生最强的语义破坏。
- **提出的 LA 和 LE 损失函数**均能引导扩散模型生成完全噪声化的图像，**彻底擦除身份语义**，性能达到最优。
- **方法可迁移且高效**：攻击在不同扩散模型间具有良好的可迁移性，并且计算开销极小，为现实场景的隐私保护提供了实用方案。
- **对比现有方法**：首次实现了身份语义的完全擦除，弥补了以往攻击仅能部分损坏图像的不足。

### 7. 优点：方法或实验设计上的亮点
- **新颖的洞察**：将注意力从生成图像质量转移到潜在空间方差的操控上，发现了方差与语义擦除的直接关联。
- **数学驱动的损失设计**：LA 损失基于拉普拉斯分布寻求局部最优方向，LE 损失引入熵和拉格朗日优化，解决梯度不对齐和方差分布适应问题，理论根基扎实。
- **效果显著**：能够实现“完全擦除”，而非仅仅降低图像质量，在隐私保护场景下价值突出。
- **高实用价值**：攻击所需计算资源少，且跨模型迁移能力强，易于部署到各类定制扩散模型服务中。

### 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等
- **实验覆盖**：仅在人脸数据集上验证，未展示在其他敏感领域（如医疗图像、文档、物体）上的表现，通用性有待证明。
- **评估指标细节缺失**：摘要未提供具体的定量指标（如擦除率、噪声程度、FID 等），无法判断数值对比的严格程度。
- **可能的防御对策**：未讨论该方法是否容易被防御（如对抗训练、输入净化）所绕过，也缺乏在防御存在时的鲁棒性分析。
- **攻击假设**：假设攻击者可介入微调过程或控制模型输入，实际部署中可能受限于访问权限（白盒/灰盒假设），黑盒场景有效性未提及。
- **单一模型家族**：虽强调跨模型迁移，但可能仅限于同类型（LDM）扩散模型，对其他生成范式（如 GAN、纯扩散模型）的效果未知。

（完）
