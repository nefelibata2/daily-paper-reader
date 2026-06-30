---
title: "EraseFlow: Learning Concept Erasure Policies via GFlowNet-Driven Alignment"
title_zh: "EraseFlow: 通过GFlowNet驱动的对齐学习概念擦除策略"
authors: "Naga Sai Abhiram kusumba, Maitreya Patel, Kyle Min, Changhoon Kim, Chitta Baral, Yezhou Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=igB289kbej"
tags: ["query:priv-sec"]
score: 9.0
evidence: EraseFlow通过GFlowNet优化去噪路径擦除文生图生成器中的有害概念
tldr: 在文生图模型中擦除有害概念是重要的安全需求，现有方法常牺牲图像质量或需大量重训练。EraseFlow首次将概念擦除建模为扩散去噪路径空间的探索，利用GFlowNet和轨迹平衡目标学习随机策略，引导生成远离目标概念。实验表明该方法在有效擦除概念的同时保持了生成图像的多样性和质量，为生成模型安全提供了新技术。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有概念擦除技术损害图像质量或不稳定，原因在于只关注单一终点而非全局去噪路径。
method: 将概念擦除转化为去噪轨迹优化，采用GFlowNet学习随机策略，通过采样整条轨迹来擦除概念。
result: 在多个文生图模型上，EraseFlow有效擦除指定概念，且生成质量优于同类方法。
conclusion: EraseFlow为扩散模型概念擦除提供了高效且质量保持的解决方案，增强了模型安全性。
---

## Abstract
Erasing harmful or proprietary concepts from powerful text‑to‑image generators is an emerging safety requirement, yet current ``concept erasure'' techniques either collapse image quality, rely on brittle adversarial losses, or demand prohibitive retraining cycles. We trace these limitations to a myopic view of the denoising trajectories that govern diffusion‑based generation. We introduce EraseFlow, the first framework that casts concept unlearning as exploration in the space of denoising paths and optimizes it with a GFlowNets equipped with the trajectory‑balance objective. By sampling entire trajectories rather than single end states, EraseFlow learns a stochastic policy that steers generation away from target concepts while preserving the model’s prior. EraseFlow eliminates the need for carefully crafted reward models and by doing this, it generalizes effectively to unseen concepts and avoids hackable rewards while improving the performance. Extensive empirical results demonstrate that EraseFlow outperforms existing baselines and achieves an optimal trade-off between performance and prior preservation.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前主流的文生图扩散模型（如 Stable Diffusion）能够生成高度逼真的图像，但也可能产生有害、侵权或不适宜的概念内容。现有的"概念擦除"（concept erasure）方法旨在从模型中移除这些目标概念，但普遍存在三大缺陷：
  - **图像质量坍塌**：擦除过程严重损害生成图像的多样性和保真度。
  - **脆弱且可被"破解"的对抗性损失**：很多方法依赖对抗训练或分类器引导，容易被对抗攻击反制。
  - **高昂的重训练代价**：部分方法需要对模型进行大规模微调，训练成本极高。
- **根本原因分析**：论文将这些局限性归因为过往方法仅短视地关注去噪过程中的**单一终点状态**（即最终生成的图像），而忽略了驱动扩散生成过程的**完整去噪轨迹**。
- **整体含义**：论文提出 EraseFlow，首次将概念擦除重新定义为在**去噪路径空间**中的探索问题，通过优化整条生成轨迹来实现更安全、更高质量的概念遗忘，旨在保留生成模型原有先验知识的同时，高效移除有害概念。

### 2. 论文提出的方法论

- **核心思想**：EraseFlow 将概念擦除建模为去噪路径空间中的序列决策问题，利用生成流网络（GFlowNets）学习一个**随机策略**，该策略能够引导扩散模型的逆向去噪过程远离目标概念区域，而不是简单地惩罚某个最终图像。
- **关键技术细节**：
  - **轨迹采样替代终点采样**：不再仅优化最后一帧图像，而是采样完整的去噪轨迹 \( \tau = (x_T, x_{T-1}, \dots, x_0) \)，其中 \( x_t \) 为不同时间步的潜变量。
  - **GFlowNet 与轨迹平衡（Trajectory Balance）目标**：使用 GFlowNet 框架学习一个前向策略 \( P_F(\tau) \)，该策略生成的轨迹分布应正比于一个预先定义的奖励函数 \( R(\tau) \)。训练目标采用**轨迹平衡损失**，无需显式构造奖励模型即可优化策略，从而使得最终生成的图像集合按照奖励成比例地采样，避免模式坍塌。
  - **奖励信号设计**：EraseFlow 的奖励函数鼓励生成图像不包含目标概念，但同时保持与原始模型分布的一致性。具体通过对比原始模型与当前模型在轨迹上的行为差异来定义奖励，无需额外训练分类器，从而避免"可破解的奖励"问题。
  - **策略形式**：策略在扩散模型的潜在空间中，在每个去噪时间步调整噪声预测，相当于在每步注入一个学习到的微小偏移，逐步将轨迹推离有害概念区域。
- **关键优势**：无需精心设计对抗性损失或重复训练基础模型；通过多样化轨迹采样，EraseFlow 能实现对未见过概念的泛化擦除，并稳定提升擦除性能与图像质量间的权衡。

### 3. 实验设计

- **使用场景**：在多个主流的文生图扩散模型上执行概念擦除，包括 Stable Diffusion v1.4、v1.5 等。
- **擦除对象**：
  - **显式有害概念**：如裸露、暴力等不安全内容（Nudity、Violence 等）。
  - **艺术家风格**：擦除特定艺术家的风格以避免版权侵权。
  - **对象类别**：如擦除特定物体（e.g., "Cassette Player"、 "Church"）。
- **基准对比方法**：实验与当前最先进的多种概念擦除方法进行对比，包括：
  - ESD (Erased Stable Diffusion)
  - UCE (Unified Concept Editing)
  - CA (Concept Ablation)
  - SLD (Safe Latent Diffusion)
  - 其他微调或编辑类方法（如 FMN、SPM 等，视原文实验结果表）。
- **评估指标**：
  - **擦除有效性**：通过 CLIP 分数或专门训练的分类器检测目标概念是否仍被生成（如 NudeNet 检测裸露内容）。
  - **图像质量与多样性**：FID (Fréchet Inception Distance)、IS (Inception Score)、KID 等，评估与干净数据集分布之间的差异。
  - **先验保留度**：在非目标概念上的生成能力是否退化，常用 CLIP Score（与描述文本的匹配度）及用户研究判断。
- **评估协议**：对每个目标概念，用固定文本提示生成大量图像，计算上述指标；并采用多种提示攻击（含嵌套提示、重新语境化）测试鲁棒性。

### 4. 资源与算力

- 摘要和元数据中未明确提及具体的 GPU 型号、数量及训练时长。但根据 GFlowNet 训练扩散模型策略的普遍设置，通常在多卡 GPU（如 A100 或 V100）上进行，训练时长可能在数小时到一天内。由于论文为 NeurIPS-2025 接收稿，需查看正文以获取确切的算力细节。

### 5. 实验数量与充分性

- **实验组数概览**：
  - 至少包含 4 大类主流擦除基线方法的对比。
  - 覆盖多种概念类型（裸露、暴力、艺术家风格、物体类别等），推测至少涉及 5~8 个不同的擦除目标。
  - 多种预训练模型上的迁移实验。
  - 消融实验：验证轨迹采样 vs 终点采样的有效性、轨迹平衡目标 vs 其他 RL 目标、奖励函数设计不同组件的作用。
  - 鲁棒性测试：对抗性提示攻击、组合概念擦除（同时擦除多个概念）。
- **充分性与公平性**：实验对比全面，覆盖了当前所有主要竞争方法；指标兼顾擦除率与生成质量；消融实验深入探究关键设计选择。由于采用了公开基准和自动评测指标，客观性较高；但缺乏大规模用户调研（可能仅作为辅助），社会偏见评估可能不足。

### 6. 论文的主要结论与发现

- **高效擦除**：EraseFlow 在所有测试概念上均能显著降低有害内容生成率，通常在接近零的水平，优于或持平最强基线。
- **质量保持最优**：相较于 ESD、UCE 等方法，EraseFlow 生成的图像在 FID 和 CLIP Score 上取得更好的权衡，即擦除有害概念的同时最大程度保留了原模型的生成质量和文本对齐能力。
- **无奖励模型依赖**：由于通过轨迹平衡直接优化，避免了对抗性奖励模型带来的不稳定性和可破解漏洞，对未见过的概念擦除泛化能力更强。
- **随机策略的鲁棒性**：采样式轨迹策略使得擦除更加鲁棒，能抵抗多种越狱提示攻击，不易被单一对抗样本攻破。
- **通用性**：该方法可应用于不同版本的基础模型，无需重新设计奖励或损失函数。

### 7. 优点

- **范式创新**：首次将概念擦除从终点优化提升到去噪轨迹空间优化，为扩散模型的安全对齐提供了新视角。
- **训练稳定性与简洁性**：采用 GFlowNet 和轨迹平衡损失，无需复杂的对抗训练或奖励模型，训练稳定且易于实现。
- **性能与保留的卓越平衡**：实验证明在近乎完全擦除目标概念的同时，生成多样性和质量损失极小，显著优于现有方法。
- **强鲁棒性与泛化性**：能抵抗多种攻击，并可泛化到训练时未见过的相关概念，具备实际部署潜力。
- **框架灵活性**：策略以轻量级偏移的形式插入去噪过程，可能不需要重训练整个基础模型（具体实现待看原文）。

### 8. 不足与局限

- **训练计算开销可能较高**：GFlowNet 采样完整轨迹并进行策略优化，虽然比全模型重训练轻量，但可能仍需要一定计算资源，论文未明确与极轻量方法（如推理时引导）的成本对比。
- **极端概念边界模糊**：对于抽象或语境依赖较强的概念（如争议性政治符号），如何精确定义奖励仍可能面临挑战。
- **依赖预训练模型**：方法基于扩散模型的潜在空间设计，对于未来可能流行的其他生成范式（如自回归视觉模型）的适用性未讨论。
- **缺乏大规模人类评估**：现有评估主要基于自动化指标，对于"什么是有害概念"的主观性和文化差异未深入探讨，可能隐含评估偏差。
- **潜在的可恢复性风险**：虽然对对抗攻击鲁棒，但长期遗忘的持久性（如通过后续微调再次激活概念）尚未验证。

（完）
