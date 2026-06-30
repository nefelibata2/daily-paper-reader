---
title: "Steering Away from Harm: An Adaptive Approach to Defending Vision Language Model Against Jailbreaks"
title_zh: 远离危害：一种防御视觉语言模型越狱的自适应方法
authors: "Wang, Han, Wang, Gang, Zhang, Huan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_Steering_Away_from_Harm_An_Adaptive_Approach_to_Defending_Vision_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过自适应激活引导防御视觉语言模型的越狱攻击
tldr: 视觉语言模型面临越狱攻击风险，现有防御措施成本高昂。本文提出ASTRA，通过寻找可迁移的有害响应方向向量，在推理时自适应地引导模型激活远离这些方向，以极低计算成本有效抵抗VLM攻击，为实际部署提供了高效的安全防御机制。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-steering-away-from-harm-an-adaptive-approach-to-defending-vision-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1800, \"height\": 694, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-steering-away-from-harm-an-adaptive-approach-to-defending-vision-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1796, \"height\": 267, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-steering-away-from-harm-an-adaptive-approach-to-defending-vision-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1749, \"height\": 647, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-steering-away-from-harm-an-adaptive-approach-to-defending-vision-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1766, \"height\": 525, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-steering-away-from-harm-an-adaptive-approach-to-defending-vision-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1766, \"height\": 526, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-steering-away-from-harm-an-adaptive-approach-to-defending-vision-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 781, \"height\": 280, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-steering-away-from-harm-an-adaptive-approach-to-defending-vision-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1626, \"height\": 453, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-steering-away-from-harm-an-adaptive-approach-to-defending-vision-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1625, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-steering-away-from-harm-an-adaptive-approach-to-defending-vision-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1622, \"height\": 326, \"label\": \"Table\"}]"
motivation: VLM易受对抗攻击生成有害内容，现有防御方法实际部署成本过高。
method: 发现可迁移的有害响应方向向量，在推理时自适应调整激活值以消除有害方向。
result: ASTRA在多种攻击下显著降低有害输出率，且计算开销极低。
conclusion: 为多模态大模型安全提供了一种轻量级、易部署的防御策略。
---

## Abstract
Vision Language Models (VLMs) can produce unintended and harmful content when exposed to adversarial attacks, particularly because their vision capabilities create new vulnerabilities. Existing defenses, such as input preprocessing, adversarial training, and response evaluation-based methods, are often impractical for real-world deployment due to their high costs. To address this challenge, we propose ASTRA, an efficient and effective defense by adaptively steering models away from adversarial feature directions to resist VLM attacks. Our key procedures involve finding transferable steering vectors representing the direction of harmful response and applying adaptive activation steering to remove these directions at inference time. To create effective steering vectors, we randomly ablate the visual tokens from the adversarial images and identify those most strongly associated with jailbreaks. These tokens are then used to construct steering vectors. During inference, we perform the adaptive steering method that involves the projection between the steering vectors and calibrated activation, resulting in little performance drops on benign inputs while strongly avoiding harmful outputs under adversarial inputs. Extensive experiments across multiple models and baselines demonstrate our state-of-the-art performance and high efficiency in mitigating jailbreak risks. Additionally, ASTRA exhibits good transferability, defending against unseen attacks (i.e., structured-based attack, perturbation-based attack with project gradient descent variants, and text-only attack).

---

## 论文详细总结（自动生成）

- # 论文核心问题与整体含义

- **研究背景**：视觉语言模型（VLMs）在受到对抗攻击时容易生成非预期和有害的内容，尤其是其视觉感知能力引入了新的攻击面。此类越狱攻击主要分为扰动型攻击（perturbation‑based）和结构型攻击（structured‑based），严重威胁模型安全。
- **现有防御的不足**：已有的防御方法——如输入预处理、对抗训练、基于响应评估的检测——在实际部署中计算成本过高，难以大规模应用。推理阶段的多次生成也导致严重延迟。
- **本文动机**：提出一种高效且易于部署的防御框架 **ASTRA**，在几乎不增加推理时间的前提下，通过自适应地引导模型内部激活远离有害特征方向，实现对 VLM 越狱攻击的有效防御。

# 方法论

- **核心思想**：
  - 找到可迁移的**引导向量 (steering vectors)**，表示模型输出有害响应的特征方向。
  - 在推理时**自适应地调整激活值**，仅在输入可能引发有害输出时才进行引导，避免降低良性输入的可用性。

- **关键技术细节**：
  1. **构造引导向量（图像归因激活引导）**：
     - 对对抗图像（由 PGD 生成）随机消融视觉令牌（visual tokens），计算每批消融后模型生成指定有害响应（如 “Sure, …”）的对数概率。
     - 使用 **Lasso 线性代理模型**拟合消融向量与越狱概率的关系，获取每个视觉令牌的**归因分数**。
     - 选择属于**Top‑k** 分数的视觉令牌，将其对应的激活（与空用户查询配对）与将这些令牌掩码后的激活相减，得到差异向量；对多张对抗图像的结果取平均，即得引导向量 \( \mathbf{v}_l \)。
  2. **自适应激活引导**：
     - 为避免无条件线性引导降低正常性能，引入**校准激活** \( \mathbf{h}_l^0 \)（大量测试数据的平均激活）。
     - 对当前层 \( l \) 的激活 \( \mathbf{h}_l \)，计算**校准后激活** \( \mathbf{h}_l - \mathbf{h}_l^0 \) 与引导向量的余弦投影；仅当投影为正时才施加引导，引导强度由超参数 \( \alpha \) 控制。
     - 公式直观理解为：仅将激活中“指向有害方向”的分量减去，保持其他成分不变，从而自适应地区分良性与对抗输入。

- **算法流程**：见论文中的 Algorithm 1，主要包含随机消融、训练代理模型、挑选关键视觉令牌、计算引导向量，以及推理时的投影引导步骤。

# 实验设计

- **评估场景与数据集**：
  - **对抗攻击防御**：使用 ImageNet 良性图像，通过 PGD 生成不同扰动半径 \( \epsilon \) （16/255, 32/255, 64/255，无约束）的对抗图像。
  - 文本提示来自 **RealToxicityPrompt**（毒性测试）、**Advbench** 和 **Anthropic‑HHH**（越狱测试），并分别与对抗图像随机配对。
  - **良性效用评估**：采用 **MM‑Vet**、**MM‑Bench** 以及安全指令集 **XSTest**。
  - **迁移性评估**：包括分布内（不同 \( \epsilon \) 的对抗图像）和分布外场景（MM‑SafetyBench 的结构化攻击、多种 PGD 变体如 Auto‑PGD 和 MI‑FGSM，以及文本纯攻击 GCG）。

- **比较方法**：
  - **VLM 防御基线**：Self‑reminder（提示增强）、JailGuard（输入扰动+响应一致性检测）、ECSO（图转文）。
  - **LLM 引导方法**：基于对比激活的 Refusal Pairs、基于文本越狱模板的 Jailbreak Templates。

- **模型**：Qwen2‑VL‑7B、MiniGPT‑4‑13B、LLaVA‑v1.5‑13B。

- **评估指标**：毒性分数（Detoxify 分类器）、攻击成功率（ASR，HarmBench 分类器），以及良性场景下的效用分数和对抗场景下的困惑度。

# 资源与算力

- 论文中**未明确说明**具体的 GPU 型号、数量或训练时长。方法本身**无需重新训练或微调**，仅需少量推理来构造引导向量（例如使用 16 张对抗图像，96 次消融），且推理时几乎无额外计算开销。因此对硬件要求极低，属于轻量级防御。

# 实验数量与充分性

- 进行了**大规模实验**，涵盖：
  - 3 种不同规模的 VLM 在多种 \( \epsilon \) 对抗强度下的防御性能对比（主表）。
  - 对抗自适应攻击的实验（表 3）。
  - 多种攻击类别的**迁移性实验**（表 5），包括结构化攻击、多种扰动攻击变体和纯文本攻击。
  - **效用保持实验**（表 6）：在多个基准上比较防御前后的模型性能。
  - 细致的**消融研究**（表 7）：验证校准激活、图像归因（与“整个图像激活”及“随机噪声”对比）的关键作用。
  - 推理时间对比（表 4）。
- 实验设计客观、公平：所有对比方法均使用相同的攻击生成策略和评估指标，并且自适应攻击假设攻击者完全了解防御机制，增强了说服力。额外消融实验（如引导层选择、α 系数、对抗图像数量）在附录中有提供。

# 主要结论与发现

- **防御效果领先**：ASTRA 在所有扰动型攻击下均显著降低毒性分数和攻击成功率，优于现有 VLM 防御和直接迁移 LLM 引导的方法。
- **高效性**：推理时间几乎与无防御模型持平，比需要多次生成响应的 JailGuard 和 ECSO 快 5–10 倍。
- **良性性能保持**：自适应投影机制使模型在 MM‑Vet、MM‑Bench 等基准上的性能损失极小，在安全指令集上过拒绝率低。
- **强迁移性**：构建的引导向量不仅能防御不同 \( \epsilon \) 的 PGD 攻击，还能跨攻击类型迁移，有效抵御结构型攻击、其他 PGD 变体甚至纯文本攻击。
- **抗自适应攻击**：即便攻击者掌握模型引导向量的全部细节，ASTRA 仍能显著降低越狱成功率。

# 优点

- **轻量级与高实用性**：无需训练，推理开销极低，适合真实世界部署。
- **自适应设计**：基于投影的引导系数避免了固定系数带来的过度拒绝或防御失效，兼顾安全与可用性。
- **图像归因提取关键视觉令牌**：精准定位对越狱贡献大的视觉特征，而非盲目使用整个图像激活，提升引导向量的有效性与可迁移性。
- **全面的安全评估**：覆盖多种攻击类型、自适应攻击和迁移性测试，实验说服力强。

# 不足与局限

- **实验覆盖范围**：虽然测试了三种 VLM，但仍限于 7B‑13B 参数量的开源模型，对更大模型或商业 API 的适用性未验证。
- **引导向量构建依赖对抗样本**：使用 PGD 生成的对抗图像构造引导向量，可能对新型攻击或特定分布外恶意图像泛化不佳，尽管迁移性实验已部分缓解该担忧。
- **校准激活的计算**：需要预先收集大量数据计算平均激活，可能引入对特定数据分布的依赖性。
- **超参数调优**：引导层选择、α 系数等可能需要针对不同模型调整，通用性有待进一步提升。
- **仅关注视觉令牌层面**：虽然能够防御文本攻击，但方法的核心仍是视觉模态的引导，对纯文本越狱的防御完全依赖提取到的有害方向，可能不够专门化。

（完）
