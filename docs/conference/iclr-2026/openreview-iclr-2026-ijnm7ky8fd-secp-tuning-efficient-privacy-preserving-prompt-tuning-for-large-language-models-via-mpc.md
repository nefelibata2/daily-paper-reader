---
title: "SecP-Tuning: Efficient Privacy-Preserving Prompt Tuning for Large Language Models via MPC"
title_zh: SecP-Tuning：基于多方安全计算的大语言模型高效隐私保护提示微调
authors: "Jinglong Luo, Zhuo Zhang, Yehong Zhang, Shiyu Liu, Ye Dong, Hui Wang, Yue Yu, Xun Zhou, Zenglin Xu"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=iJNM7KY8FD"
tags: ["query:priv-sec"]
score: 10.0
evidence: 基于MPC的大语言模型高效隐私保护提示微调
tldr: 本文提出SecP-Tuning框架，利用安全多方计算（MPC）实现大语言模型的高效隐私保护提示微调。通过解决后向传播、优化器和自注意力操作中的效率瓶颈，使LLM在医疗等隐私敏感领域的适应性微调成为现实，在保护数据和模型参数隐私的同时保持较低的计算开销。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: LLM在医疗等隐私域微调面临数据稀缺和隐私泄露风险。
method: 基于MPC的隐私保护提示微调框架，克服微调中的关键效率挑战。
result: 实现了实用高效的隐私保护LLM微调，性能与明文微调接近。
conclusion: SecP-Tuning为LLM在隐私敏感领域的应用提供了安全高效的微调方案。
---

## Abstract
Large Language Models (LLMs) have revolutionized numerous fields, yet their adaptation to specialized tasks in privacy-sensitive domains such as healthcare and finance remains constrained due to the scarcity of accessible training data caused by stringent privacy requirements. Secure Multi-party Computation (MPC)-based privacy-preserving machine learning provides theoretical guarantees for the privacy of model parameters and data. However, its application to LLMs has been predominantly limited to inference, as fine-tuning introduces significant efficiency challenges, particularly in backward propagation, optimizer, and self-attention operations. To address these challenges, we propose SecP-Tuning, the MPC-based framework designed for efficient, privacy-preserving prompt tuning of LLMs. SecP-Tuning innovatively integrates Forward-only Tuning through the ''data owner-server interaction" paradigm, effectively removing the need for privacy-preserving computations in backward propagation and optimization processes. Furthermore, it devises an efficient privacy-preserving Random Feature Attention, effectively mitigating the computational complexity of softmax-based self-attention and circumventing MPC-incompatible nonlinear operations. Experimental results demonstrate that, compared to full-Parameter Supervised Fine-Tuning and gradient-based prompt tuning, SecP-Tuning achieves approximately 12$\times$ and 16$\times$ end-to-end acceleration, as well as 17$\times$ and 20$\times$ reductions in communication overhead, respectively. Moreover, it delivers performance comparable to gradient-based methods across multiple few-shot tasks. Additionally, the ''black-box/API-style" privacy-preserving tuning paradigm of SecP-Tuning effectively avoids memory leakage risks caused by gradient/parameter transmission, thereby striking an optimal balance between privacy, efficiency, performance, and deployability.

---

## 论文详细总结（自动生成）

# 论文总结：SecP-Tuning: 基于多方安全计算的大语言模型高效隐私保护提示微调

## 1. 研究动机与核心问题
- **背景**：大语言模型（LLM）在医疗、金融等隐私敏感领域的任务适配面临两难：这些领域数据稀疏且受严格的隐私法规约束，直接收集训练数据几乎不可行。
- **已有方案的局限**：基于安全多方计算（MPC）的隐私保护机器学习能对模型参数和数据同时提供理论上的隐私保障，但目前相关工作几乎仅限LLM推理，无法高效支撑微调（fine-tuning）。
- **微调在MPC中的瓶颈**：将MPC引入LLM微调会带来巨大的计算与通信开销，关键障碍集中在三个环节——反向传播、优化器操作以及自注意力中的softmax等非线性函数。
- **整体含义**：论文旨在设计一个**高效、可部署的MPC原生隐私保护微调框架**，让LLM既能利用私有数据适配下游任务，又能在合理资源消耗下保护数据和模型隐私。

## 2. 方法论（核心思想与关键技术）
- **核心思想**：将“仅需前向传播”的调优范式与MPC结合，从根本上消除反向传播和优化过程中昂贵的隐私计算；同时用MPC友好的操作替代自注意力中不兼容的非线性函数。
- **关键技术一：Data Owner-Server交互式Forward-only Tuning**
  - 抛弃传统基于梯度的微调，采用一种仅依赖前向传播的范式（作者称为“Forward-only Tuning”）。
  - 数据拥有者（如医院）与模型服务器之间以交互方式完成对提示（prompt）的调优，**全程不需要进行隐私保护的反向传播和优化器计算**。
  - 这种设计将微调过程转化为“黑盒/API风格”的隐私保护调优，避免了因梯度或参数传输导致的内存泄露风险。
- **关键技术二：高效隐私保护随机特征注意力（Privacy-Preserving Random Feature Attention）**
  - 标准Transformer的自注意力需要计算softmax，在MPC中实现极其昂贵。
  - 采用随机特征映射（Random Feature, RF）的方法对注意力进行近似，将非线性softmax转化为可分解的线性操作，从而大幅降低MPC计算复杂度。
  - 该近似注意力机制全程在MPC协议内执行，既保护中间结果隐私，又保持计算效率。

## 3. 实验设计
- **任务场景**：论文在多个**少样本（few-shot）下游任务**上验证了框架的有效性（摘要中未列出具体数据集名称，推测可能涵盖文本分类、推理等常见NLP任务）。
- **对比基准**：
  - **全参数监督微调**（full-Parameter Supervised Fine-Tuning, SFT）作为明文下的强基线。
  - **基于梯度的提示微调**（gradient-based prompt tuning）作为另一种参数高效微调方法。
- **评估指标**：端到端运行时间、通信开销、最终任务性能。

## 4. 资源与算力
- 论文摘要及可见元数据中**未明确给出**所使用GPU型号、数量或训练时长等具体算力信息。因此无法评估其实验对硬件资源的依赖程度。

## 5. 实验数量与充分性
- 由于仅获得摘要内容，**无法判断具体实验组数**（如消融实验、不同模型规模、不同MPC协议设置的对比等）。
- 给出的核心结论（加速12×/16×、通信降低17×/20×、性能与梯度方法持平）表明至少进行了覆盖主要对比方法的端到端实验，但缺少细节（如任务数量、统计显著性、不同隐私强度下的表现）使其**充分性难以评估**。
- 如果论文后续未提供足够的消融实验（例如对RF注意力的替代效果、仅前向调优单独贡献的分析），则实验可能不够全面。

## 6. 主要结论与发现
- SecP-Tuning成功实现了**实用级别的隐私保护LLM微调**，性能与基于梯度的明文提示微调基本持平。
- 相比全参数SFT和梯度提示微调，其在端到端时间上分别获得约 **12倍与16倍的加速**，通信开销分别降低 **17倍和20倍**。
- 所提出的“黑盒/API风格”微调范式有效兼顾**隐私、效率、模型性能和可部署性**，为LLM在敏感领域的私有化适配提供了可行路径。

## 7. 优点（方法或实验设计的亮点）
- **根除反向传播瓶颈**：通过仅需前向的调优范式，创造性地绕过了MPC微调中最难攻克的部分。
- **算法-系统协同设计**：随机特征注意力直接适配MPC限制，既保证注意力近似的有效性又大幅提升效率，非简单工程优化。
- **隐私模型完备**：“数据拥有者-服务器”交互模式避免了梯度/参数泄露，天然适配以API为中心的服务场景。
- **显著的实际加速**：两位数的加速比和通信缩减证明了框架的实用性，从原先“理论可行”推进到“工程可用”。

## 8. 不足与局限
- **实验透明度不足**：摘要未列出具体任务数据集、模型规格及MPC协议实现（如使用了多少参与方、何种安全模型），导致难以复现和客观对比。
- **可能的性能退化边界不清**：随机特征注意力相对于真实softmax的近似误差可能在某些任务上放大，缺少对注意力度量的深入分析。
- **仅涵盖提示微调**：框架目前针对提示调优，未扩展到LoRA或全参数微调等更通用的参数高效方法，适用性存在边界。
- **安全性假设未阐述**：未说明MPC的安全模型（半诚实/恶意）、诚实多数假设等，安全性强度不确定。
- **无明文调优的完整性能对比**：虽声称与梯度方法性能持平，但未给出与明文下强力基线的具体分数差异，难以判断隐私带来的精度代价是否完全可忽略。

（完）
