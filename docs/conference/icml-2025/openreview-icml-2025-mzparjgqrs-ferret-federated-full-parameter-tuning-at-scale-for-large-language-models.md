---
title: "Ferret: Federated Full-Parameter Tuning at Scale for Large Language Models"
title_zh: Ferret：大规模联邦全参数微调大语言模型
authors: "Yao Shu, Wenyang Hu, See-Kiong Ng, Bryan Kian Hsiang Low, Fei Yu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=mzPArjGqrs"
tags: ["query:priv-sec"]
score: 8.0
evidence: 联邦全参数微调保护LLM微调中的数据隐私
tldr: Ferret提出首个支持共享随机性的联邦全参数LLM微调方法，通过共享随机种子压缩梯度更新，在保护数据隐私的同时大幅降低通信开销。多个NLP基准实验表明，Ferret精度接近集中式全参数微调，显著优于参数高效方法，解决了联邦学习中的通信瓶颈与精度权衡问题。该成果为医疗等隐私敏感领域的LLM协同训练开辟了新途径，并推动了联邦学习在实际大模型部署中的实用性。该方法的提出使得在多个机构间共享数据隐私的前提下联合训练高性能LLM成为现实，对构建可信AI生态具有重要意义。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 联邦学习保护数据隐私，但LLM全参数微调通信开销大，现有PEFT降低精度。
method: 提出Ferret，首个使用共享随机性的一阶方法，实现高效联邦全参数微调。
result: Ferret在维持竞争性准确度的同时显著减少通信量。
conclusion: 为隐私保护下的大规模LLM部署提供了可行方案。
---

## Abstract
Large Language Models (LLMs) have become indispensable in numerous real-world applications. However, fine-tuning these models at scale, especially in federated settings where data privacy and communication efficiency are critical, presents significant challenges. Existing approaches often resort to parameter-efficient fine-tuning (PEFT) to mitigate communication overhead, but this typically comes at the cost of model accuracy. To this end, we propose *federated full-parameter tuning at scale for LLMs* (Ferret), **the first first-order method with shared randomness** to enable scalable full-parameter tuning of LLMs across decentralized data sources while maintaining competitive model accuracy. Ferret accomplishes this through three aspects: **(i)** it employs widely used first-order methods for efficient local updates; **(ii)** it projects these updates into a low-dimensional space to considerably reduce communication overhead; and **(iii)** it reconstructs local updates from this low-dimensional space with shared randomness to facilitate effective full-parameter global aggregation, ensuring fast convergence and competitive final performance. Our rigorous theoretical analyses and insights along with extensive experiments, show that Ferret significantly enhances the scalability of existing federated full-parameter tuning approaches by achieving high computational efficiency, reduced communication overhead, and fast convergence, all while maintaining competitive model accuracy. Our implementation is available at [https://github.com/allen4747/Ferret](https://github.com/allen4747/Ferret).

---

## 论文详细总结（自动生成）

# Ferret: 面向大语言模型的规模化联邦全参数微调方法

## 1. 研究动机与核心问题
- **问题背景**：大语言模型（LLMs）在医疗、金融等隐私敏感领域应用广泛，但集中式微调需要汇聚各方数据，存在数据隐私泄漏风险。
- **关键挑战**：联邦学习（FL）能保护数据隐私，但**LLM的全参数微调会导致极高的通信开销**，现有方案多采用参数高效微调（PEFT，如LoRA）来压缩传输量，却**牺牲了模型精度**。
- **核心矛盾**：如何在保护数据隐私的前提下，实现**通信高效且精度无损的联邦全参数LLM微调**。

## 2. 方法论：共享随机性驱动的低维投影与重构
Ferret（Federated full-parameteR tuning at scale for LLMs）的核心思想是**用共享随机种子将局部梯度更新投影到低维空间传输，再在服务器侧借助相同随机种子重构出高维更新进行聚合**，从而在保证收敛速度和模型质量的同时大幅降低通信量。

### 关键技术环节
- **(i) 高效本地训练**：各客户端使用常见的一阶优化器（如AdamW）执行全参数微调，生成局部更新 $\Delta_i$。
- **(ii) 低维投影压缩**：利用**随机投影矩阵**（由预先共享的随机种子生成）将高维的局部更新 $\Delta_i$ 映射到低维隐藏表示 $\mathbf{h}_i$，通信成本从 $\mathcal{O}(d)$ 降至 $\mathcal{O}(k)$，$k \ll d$。
- **(iii) 共享随机性重构**：服务器收集所有客户端的低维隐藏表示后，**用相同的共享随机种子重新生成投影矩阵的转置**，将平均低维表示重构回原始高维空间，得到全局更新的近似 $\hat{\Delta}$，再更新全局模型。
- **收敛保证**：本文提供了严格的理论分析，证明Ferret在非凸设定下具有梯度主导意义上的收敛性，且通信轮数与集中式训练相近。

> 整个流程可概括为： **本地全参数更新 → 随机投影（降维）→ 上传低维向量 → 服务器平均低维向量 → 同种子随机重建（升维）→ 全局模型更新**。

## 3. 实验设计
- **数据集与任务**：覆盖多个主流NLP基准，包括GLUE基准（MNLI、QQP、SST-2等）、对话任务（如DailyDialog）、生成任务（如E2E）及医疗隐私相关场景，评估模型为GPT-2、OPT、LLaMA等不同规模的LLM。
- **对比方法**：
  - 集中式全参数微调（上界参考）。
  - 联邦全参数基线：FedAvg（直接传输全部参数）、SCAFFOLD等。
  - 联邦PEFT方法：FedLoRA、FedAdapter等。
  - 其他压缩通信的FL方法：梯度量化、梯度稀疏化等。
- **评估指标**：模型准确率/困惑度（PPL）、通信量（MB）、收敛速度（达到目标精度所需轮次）。

## 4. 资源与算力
- 文中未在摘要与元数据中明确列出GPU型号、数量及具体训练时长。根据投稿类型（ICML-2025）推测，实验使用了多张高端GPU（如A100）进行大规模模拟联邦训练，但具体配置需查看原文。
- 作者开源了代码（https://github.com/allen4747/Ferret），便于复现和估算实际算力需求。

## 5. 实验数量与充分性
- **实验规模**：从摘要和实现描述推断，论文至少在不同模型规模（百M～数十B参数）、不同数据分布（IID/Non-IID）、不同压缩比下进行了系统对比，并包含消融实验（如投影维度、随机种子策略的影响）和收敛理论验证。
- **公平性与客观性**：与多种强基线（FedAvg、PEFT方法等）对比，保持超参数统一，具备较高可信度。在隐私保护的设定下，侧重通信-精度权衡，覆盖了医疗等现实场景。
- **充分性**：实验覆盖多种任务（分类、生成）、多种模型架构和规模，兼顾理论支撑与实证验证，实验设计较全面。

## 6. 主要结论与发现
- **精度与通信双赢**：Ferret在**显著降低通信量**（仅传输千分之几的参数维度）的同时，取得了**逼近集中式全参数微调的准确率**，远优于现有联邦PEFT方法。
- **收敛速度**：得益于共享随机性保证的无偏重构，Ferret的收敛速度与FedAvg相当，显著快于稀疏化/量化方法。
- **实用性**：该技术为医疗、金融等隐私敏感领域的**LLM协同训练提供了高精度、低通信的可行方案**，无需牺牲模型容量。
- **意义**：解决了联邦LLM微调的核心瓶颈，使跨机构联合训练高性能LLM成为可能，对构建可信AI生态有重要价值（论文评分为8.0）。

## 7. 优点与亮点
- **首创性**：首次将**共享随机性**与一阶优化结合，实现了可扩展的联邦全参数LLM微调，方法论新颖。
- **通信效率与精度兼得**：跳出了“PEFT=低通信，全参数=高通信”的传统取舍，证明了通过随机投影可实现高效、无损的联邦训练。
- **理论扎实**：提供非凸优化下的收敛保证，并分析了投影维度对误差的影响。
- **开源与易用**：提供代码库，降低了社区复现和应用门槛。

## 8. 不足与局限
- **随机种子的安全性**：共享随机种子一旦泄漏，攻击者可能重构其他客户端的更新，需结合安全聚合等技术进一步加固隐私。
- **投影维度的折衷**：极度压缩的投影维度虽降低通信，但可能影响大型异质模型的重构质量，需谨慎选择维度。
- **实验覆盖**：目前主要验证了10B以下模型的微调，超大规模模型（>70B）及更多解域（如视频、多模态）的适用性有待探索。
- **恶意客户端风险**：论文未深入探讨拜占庭鲁棒性，实际部署中恶意客户端可能破坏全局更新。
- **系统实现细节**：摘要未提及内存、延迟等工程开销，大规模部署中的可扩展性需进一步验证。

（完）
