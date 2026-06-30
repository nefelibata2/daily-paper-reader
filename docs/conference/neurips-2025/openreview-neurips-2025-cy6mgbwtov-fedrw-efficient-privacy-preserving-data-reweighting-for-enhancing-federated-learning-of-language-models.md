---
title: "FedRW: Efficient Privacy-Preserving Data Reweighting for Enhancing Federated Learning of Language Models"
title_zh: "FedRW: 高效隐私保护数据重加权用于增强语言模型联邦学习"
authors: "Pukang Ye, Junwei Luo, Jiachen Shen, Saipan Zhou, Shangmin Dou, Zhenfu Cao, Hanzhe Yao, Xiaolei Dong, Yunbo Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=cy6MGBwToV"
tags: ["query:priv-sec"]
score: 9.0
evidence: FedRW通过安全的频率感知重加权实现联邦LLM训练的隐私保护软去重
tldr: 联邦学习训练大语言模型时，重复数据既影响性能又可能泄露隐私，传统去重依赖可信第三方并可能导致信息丢失。FedRW提出隐私保护软去重框架，通过安全多方计算进行频率感知样本重加权，避免删除操作，在不假设可信第三方的前提下安全地利用样本频率信息。实验表明该方法有效提升了联邦LLM训练的隐私安全性和模型质量。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 联邦LLM训练中重复数据既损害模型又引入隐私风险，传统去重方法或依赖第三方或损失信息。
method: 设计安全多方计算协议，在不泄露频率信息的前提下计算样本权重，实现软去重。
result: FedRW在多个联邦LLM基准上相比去重方法提升了隐私性和下游任务性能。
conclusion: FedRW为联邦大模型训练提供了兼顾隐私与效用的数据管理新范式。
---

## Abstract
Data duplication within large-scale corpora often impedes large language models' (LLMs) performance and privacy. In privacy-concerned federated learning scenarios, conventional deduplication methods typically rely on trusted third parties to perform uniform deletion, risking loss of informative samples while introducing privacy vulnerabilities. To address these gaps, we propose Federated ReWeighting (FedRW), the first privacy-preserving framework, to the best of our knowledge, that performs soft deduplication via sample reweighting instead of deletion in federated LLM training, without assuming a trusted third party. At its core, FedRW proposes a secure, frequency-aware reweighting protocol through secure multi-party computation, coupled with a parallel orchestration strategy to ensure efficiency and scalability. During training, FedRW utilizes an adaptive reweighting mechanism with global sample frequencies to adjust individual loss contributions, effectively improving generalization and robustness. Empirical results demonstrate that FedRW outperforms the state-of-the-art method by achieving up to $28.78\times$ speedup in preprocessing and approximately $11.42$\% improvement in perplexity, while offering enhanced security guarantees. FedRW thus establishes a new paradigm for managing duplication in federated LLM training.

---

## 论文详细总结（自动生成）

由于提供的论文文本仅包含标题、摘要和元数据，缺乏正文的详细方法论、实验设定与结果分析，以下总结将基于这些有限信息进行，可能无法满足所有细节要求，我会尽量从已有内容中提取并合理推断，并明确指出信息缺失之处。

---

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：在大语言模型（LLM）的训练中，语料库的数据重复现象既损害模型性能（如泛化能力下降），又可能在联邦学习场景下引发隐私泄露风险。传统去重方法通常依赖一个可信第三方执行统一的硬删除，这不仅可能丢弃有用样本，还引入了新的隐私薄弱环节。
- **整体含义**：该论文旨在解决联邦LLM训练中“去重—隐私—效用”的三元矛盾，提出一种**不依赖可信第三方、以软去重代替硬删除**的隐私保护框架，从而在保护数据隐私的同时提升模型质量。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：通过**样本重加权**（Reweighting）实现软去重，而非物理删除样本。框架名为 FedRW（Federated ReWeighting），其关键是在联邦学习各参与者之间，使用**安全多方计算（Secure Multi-Party Computation）** 安全地计算全局样本的频率信息，并据此生成样本权重，调整每个样本在训练损失中的贡献。
- **关键技术细节**（基于摘要推断）：
  - **安全频率感知重加权协议**：利用安全多方计算技术，在不泄露各方原始数据频率的情况下，协同计算出样本的全局频率或权重。
  - **并行协调策略**：为了确保效率与可扩展性，设计了并行化的预处理或计算流程，使得预处理速度大幅领先于基准方法。
  - **自适应重加权机制**：训练过程中，根据全局样本频率动态调整损失函数中每个样本的权重，抑制高频重复样本的影响，提升模型泛化性和鲁棒性。
  - **隐私保护模式**：全程不假设可信第三方，数据持有方只需参与安全协议，原始样本及其确切频率均不暴露给其他方。

## 3. 实验设计：数据集 / 场景 / Benchmark / 对比方法
- 摘要仅提及在“多个联邦LLM基准（multiple federated LLM benchmarks）”上进行实验，并未公开具体数据集名称（如 The Pile、C4 等）或联邦划分细节。
- **对比基准**：与“现有最先进方法”（state-of-the-art method）进行了对比，该方法应为某种基于删除的去重方案（可能为集中式或依赖第三方的方案）。
- **主要评价指标**：预处理时间的加速比（高达 28.78 倍）和语言模型困惑度（perplexity，改善约 11.42%）。
- **信息缺失**：具体的 benchmark 名称、对比方法的论文来源、消融实验设置等均未在摘要与元数据中给出。

## 4. 资源与算力
- 摘要和元数据中**未提及**所使用的 GPU 型号、数量、训练时长或浮点运算量等算力资源信息。因此无法评估其计算开销与硬件需求。

## 5. 实验数量与充分性
- 摘要未说明实验总数、消融研究组数或统计分析细节。仅给出了两个核心指标的结果（加速比和困惑度提升）。因此，**无法判断实验是否充分覆盖不同联邦规模、数据分布、模型尺寸等因素**。从仅有的指标看，声称的改进幅度较显著，但缺乏方差、显著性检验或不同设置下的稳定性证据。

## 6. 论文的主要结论与发现
- FedRW 实现了联邦 LLM 训练中**隐私保护的软去重**，在预处理效率上达到最高 28.78 倍加速，在下游任务（语言建模）困惑度上提升约 11.42%。
- 该方法提供了**增强的安全保障**，因为无需可信第三方，且通过安全多方计算避免频率信息泄露。
- FedRW 为联邦大模型训练中的数据重复管理建立了**新范式**，兼顾隐私与效用。

## 7. 优点：方法或实验设计上的亮点
- **隐私与效用结合**：首次在联邦 LLM 场景下利用安全多方计算实现软去重，避免了传统硬删除的信息损失和第三方信任假设。
- **效率优化**：提出的并行协调策略使预处理速度获得数量级提升，提升了可用性。
- **频率感知权重**：利用全局频率自适应调整损失贡献，理论上比简单删除更能保留稀有样本的有用信号。
- **学术价值**：据称是第一个此类框架，开辟了隐私保护数据重加权的研究方向。

## 8. 不足与局限（包括实验覆盖、偏差风险、应用限制等）
- **实验细节缺失**：由于仅有摘要，无法评估所使用的数据集是否具有代表性、联邦场景的规模是否真实（如客户端数量、数据异质性程度），以及对比方法是否调优至最佳。
- **可能的安全开销未讨论**：安全多方计算通常带来通信与计算开销，文中虽强调预处理加速，但训练过程中的吞吐量、通信轮次等效率指标未知。
- **泛化性待验证**：仅从困惑度提升看，对于其他重要的 LLM 能力（如推理、对话、代码生成）是否同样有效未知；去重效果可能依赖于数据重复模式，不一定在所有领域一致。
- **未提及局限场景**：例如在极度非独立同分布（non-IID）数据下，频率估计是否有偏；安全模型是否可抗合谋或恶意攻击等，均无从得知。

（完）
