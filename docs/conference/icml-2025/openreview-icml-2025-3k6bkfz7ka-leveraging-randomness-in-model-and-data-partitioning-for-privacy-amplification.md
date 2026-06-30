---
title: Leveraging Randomness in Model and Data Partitioning for Privacy Amplification
title_zh: 利用模型与数据分区中的随机性实现隐私放大
authors: "Andy Dong, Wei-Ning Chen, Ayfer Ozgur"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=3K6BkFZ7ka"
tags: ["query:priv-sec"]
score: 7.0
evidence: 通过训练随机性实现隐私放大，可应用于医学AI联邦学习
tldr: 本文研究训练过程中数据和模型分区的内在随机性对差分隐私的放大效应，证明了现有方法（如模型切分、dropout）的隐私增益被严重低估。该理论框架为联邦学习等场景提供了更强的隐私保障，对隐私敏感领域如医学AI具有重要价值。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 传统隐私分析低估了训练随机性（如部分训练、部分模型更新）的隐私保护潜力。
method: 建立框架分析数据和模型分区随机性对差分隐私的放大作用，应用于联邦学习模型并行。
result: 理论证明现有方法能提供显著更高的隐私放大增益，优于以往分析。
conclusion: 该研究为利用固有随机性增强隐私保护提供了理论基础，可指导更高效的隐私设计。
---

## Abstract
We study how inherent randomness in the training process—where each sample (or client in federated learning) contributes only to a randomly selected portion of training—can be leveraged for privacy amplification. This includes (1) data partitioning, where a sample participates in only a subset of training iterations, and (2) model partitioning, where a sample updates only a subset of the model parameters. We apply our framework to model parallelism in federated learning, where each client updates a randomly selected subnetwork to reduce memory and computational overhead, and show that existing methods, e.g. model splitting or dropout, provide a significant privacy amplification gain not captured by previous privacy analysis techniques. Additionally, we introduce balanced iteration subsampling, a new data partitioning method where each sample (or client) participates in a fixed number of training iterations. We show that in certain regimes, this method yields stronger privacy amplification than Poisson (i.i.d.) sampling of data (or clients). Our results demonstrate that randomness in the training process, which is  structured rather than i.i.d. and interacts with data in complex ways, can be systematically leveraged for nontrivial privacy amplification.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
通过训练随机性实现隐私放大，可应用于医学AI联邦学习。

### 2. 核心内容
本文研究训练过程中数据和模型分区的内在随机性对差分隐私的放大效应，证明了现有方法（如模型切分、dropout）的隐私增益被严重低估。该理论框架为联邦学习等场景提供了更强的隐私保障，对隐私敏感领域如医学AI具有重要价值。

### 3. 对应检索需求
privacy preserving techniques for medical AI and generative models。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=3K6BkFZ7ka](https://openreview.net/forum?id=3K6BkFZ7ka)
