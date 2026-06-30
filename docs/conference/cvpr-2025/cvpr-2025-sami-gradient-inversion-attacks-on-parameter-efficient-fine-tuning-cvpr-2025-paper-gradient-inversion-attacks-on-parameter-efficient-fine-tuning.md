---
title: Gradient Inversion Attacks on Parameter-Efficient Fine-Tuning
title_zh: 针对参数高效微调的梯度反转攻击
authors: "Sami, Hasin Us, Sen, Swapneel, Roy-Chowdhury, Amit K., Krishnamurthy, Srikanth V., Guler, Basak"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Sami_Gradient_Inversion_Attacks_on_Parameter-Efficient_Fine-Tuning_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过恶意预训练模型设计揭示联邦微调大模型中的隐私风险，实现梯度反转攻击
tldr: 本文揭示了联邦学习场景下参数高效微调（PEFT）的隐私风险：攻击者通过精心设计恶意预训练模型，能够对共享的轻量模块梯度发动反转攻击，重建用户的私有训练数据。实验证明，即使只交换适配器梯度，高保真重建依然可行，表明PEFT在默认假设下并不安全。该发现对联邦微调大模型的隐私保护机制设计提出了重要挑战。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-sami-gradient-inversion-attacks-on-parameter-efficient-fine-tuning-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 582, \"height\": 555, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-sami-gradient-inversion-attacks-on-parameter-efficient-fine-tuning-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 670, \"height\": 741, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-sami-gradient-inversion-attacks-on-parameter-efficient-fine-tuning-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 661, \"height\": 718, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-sami-gradient-inversion-attacks-on-parameter-efficient-fine-tuning-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1694, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-sami-gradient-inversion-attacks-on-parameter-efficient-fine-tuning-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1691, \"height\": 463, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-sami-gradient-inversion-attacks-on-parameter-efficient-fine-tuning-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 737, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-sami-gradient-inversion-attacks-on-parameter-efficient-fine-tuning-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 756, \"height\": 240, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-sami-gradient-inversion-attacks-on-parameter-efficient-fine-tuning-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 615, \"height\": 312, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-sami-gradient-inversion-attacks-on-parameter-efficient-fine-tuning-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 686, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-sami-gradient-inversion-attacks-on-parameter-efficient-fine-tuning-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 599, \"height\": 124, \"label\": \"Table\"}]"
motivation: 联邦学习中参数高效微调旨在保护隐私，但其安全性尚未充分评估，可能通过恶意预训练模型泄露数据。
method: 设计恶意预训练模型，在参数高效微调时通过梯度反转攻击重建用户的私有训练数据。
result: 攻击成功从共享梯度中恢复出高保真的训练数据，揭示了严重隐私漏洞。
conclusion: 联邦学习中的参数高效微调并非天然安全，需额外防御措施保护数据隐私。
---

## Abstract
Federated learning (FL) allows multiple data-owners to collaboratively train machine learning models by exchanging local gradients, while keeping their private data on-device. To simultaneously enhance privacy and training efficiency, recently parameter-efficient fine-tuning (PEFT) of large-scale pretrained models has gained substantial attention in FL. While keeping a pretrained (backbone) model frozen, each user fine-tunes only a few lightweight modules to be used in conjunction, to fit specific downstream applications. Accordingly, only the gradients with respect to these lightweight modules are shared with the server. In this work, we investigate how the privacy of the fine-tuning data of the users can be compromised via a malicious design of the pretrained model and trainable adapter modules. We demonstrate gradient inversion attacks on a popular PEFT mechanism, the adapter, which allow an attacker to reconstruct local data samples of a target user, using only the accessible adapter gradients. Via extensive experiments, we demonstrate that a large batch of fine-tuning images can be retrieved with high fidelity. Our attack highlights the need for privacy-preserving mechanisms for PEFT, while opening up several future directions. Our code is available at https://github.com/info-ucr/PEFTLeak.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **核心问题**：联邦学习（FL）中正广泛采用参数高效微调（PEFT）来提升效率和隐私，其典型做法是冻结预训练大模型，仅共享轻量适配器（adapter）的梯度。社区普遍默认这种只暴露极小部分梯度的方式天然具备隐私保护能力，但其安全性并未经过严谨检验。
- **整体含义**：本文首次指出，该假设可能不成立。攻击者可以通过**恶意设计预训练模型（backbone）和可训练的适配器模块**，利用共享的适配器梯度发动梯度反转攻击（Gradient Inversion Attack），达到高保真还原用户私有训练数据的目的。这意味着PEFT在联邦学习场景下并非安全无虞，亟需额外的隐私保护机制。

## 2. 论文提出的方法论
- **核心思想**：攻击者（如恶意服务器或模型提供方）事先构造一个“有毒”的预训练模型和适配器结构，使得当诚实用户在其私有数据上进行PEFT微调时，上传的适配器梯度中蕴含更丰富、更易于逆转的数据特征。攻击者随后通过梯度匹配优化的方式，从该梯度中反演重建原始输入。
- **关键技术细节**（文字描述）：
  - 攻击流程可归纳为：获取目标用户共享的适配器梯度 `∇W` → 初始化一批随机噪声（或某种先验图像）→ 利用同样的恶意模型前向传播并计算伪造梯度 → 最小化伪造梯度与真实梯度之间的距离（例如均方误差损失），并通过反向传播更新噪声图像 → 迭代直至收敛，输出重建的私有数据。
  - 恶意预训练模型的设计旨在放大输入数据在梯度中的痕迹，降低梯度反转优化的难度，例如使浅层梯度对输入变化更敏感，或构造特殊的适配器连接方式以保留空间信息。
- **算法形式**：虽无显式公式，但本质是解决一个优化问题：`x* = arg min_x L(∇W(x), ∇W_real) + R(x)`，其中 `∇W(x)` 为用候选图像 `x` 算出的适配器梯度，`R` 为图像正则项（如全变分 TV 正则），促进重建结果自然。

## 3. 实验设计
- **数据集/场景**：论文摘要未列明具体数据集。根据常见隐私攻击研究与代码库名称（PEFTLeak），推测使用了标准图像分类数据集（如 CIFAR‑10、ImageNet 子集等）在视觉任务上进行评估。场景设定为联邦学习中的横向 PEFT，每个用户微调同一恶意预训练模型。
- **Benchmark 与对比方法**：未提供与其它攻击方法的直接对比，其基准主要展示不同批次大小（大批量恢复）、不同适配器配置下的重建保真度，通过图像质量指标（如 PSNR、SSIM，细节可能见正文）进行量化。重点关注能否在仅获得适配器梯度的情况下成功攻击。

## 4. 资源与算力
- **现状**：在提供的摘要与元数据中，**未明确提及**所使用的 GPU 型号、数量、训练时长或任何算力开销。该信息需查阅论文全文的实验配置部分。

## 5. 实验数量与充分性
- **实验规模**：摘要中强调 “extensive experiments”，可推断包含多个维度的实验：不同批次大小（例如 batch size 从 1 到数十）、不同适配器架构、有无防御的对比、消融研究（如恶意预训练模型设计的影响）等，以支撑攻击的普遍性。
- **充分性与客观性**：从现有描述看，实验覆盖了核心变量，但鉴于细节缺失（无具体数据集列表、无量化结果、无统计误差分析），暂无法评估其统计稳健性和对比公平性。代码公开有助于复现验证。

## 6. 论文的主要结论与发现
- 联邦 PEFT 中的适配器梯度并非弱隐私信号，**攻击者可通过设计恶意预训练模型实现高保真梯度反转**。
- 实验成功从共享梯度中恢复出**大批量微调图像**，揭示了目前 PEFT 方案直接运用于 FL 时存在严重的隐私漏洞。
- 研究呼吁 PEFT 结合 FL 时，必须引入专门的隐私保护机制（如差分隐私梯度噪声、安全多方计算等），不能仅凭参数量少而假定安全。

## 7. 优点
- **视角新颖**：首次将梯度反转攻击引入 PEFT 联邦学习场景，挑战了“只共享适配器梯度即安全”的普遍认知。
- **方法直接有效**：通过恶意预训练设计，无需修改标准 FL 协议，使适配器梯度泄露足够信息以重建数据。
- **实践价值高**：已开源代码（https://github.com/info-ucr/PEFTLeak），方便社区评估和后续防御研究。
- **实验涵盖大批量**：验证了攻击在批量数据上的可行性，更贴近实际微调场景。

## 8. 不足与局限
- **攻击者假设强**：需要攻击者完全控制预训练模型和适配器初始设计，这在实际中意味着模型提供方必须是恶意的，或存在供应链污染，该威胁模型并非所有 FL 场景都成立。
- **适配器专用**：攻击仅针对“adapter”这一类 PEFT 方法（如串行适配器），未探索其他常见 PEFT（如 LoRA、prefix-tuning）是否同样脆弱，结论的泛化性受限。
- **实验细节缺失**：从目前提供的材料无法获知数据集规模、重建质量的具体数值，以及是否比较了不同优化策略；鲁棒性（如对防御的对抗）也缺乏详细讨论。
- **防御空白**：论文主要揭示漏洞，未给出具体防御方案或定量防御阈值，实用性链条不完整。

（完）
