---
title: "FedGraph: Defending Federated Large Language Model Fine-Tuning Against Backdoor Attacks via Graph-Based Aggregation"
title_zh: "FedGraph: 通过基于图的聚合防御联邦大语言模型微调中的后门攻击"
authors: "Xi Chen, Chunyi Zhou, Rui Zeng, Xiaogang Xu, Zhe Liu, Shouling Ji"
date: 2025-09-17
pdf: "https://openreview.net/pdf?id=PUFCmGuuXg"
tags: ["query:priv-sec"]
score: 9.0
evidence: 利用图聚合防御联邦大语言模型微调中的后门攻击
tldr: 针对联邦大语言模型微调易受后门攻击且现有防御因高维更新而失效的问题，提出基于图聚合的防御方法FedGraph。实验表明该方法能有效检测并过滤恶意更新，保障模型安全性，为联邦学习部署提供实用安全方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 联邦微调大语言模型存在严重后门攻击风险，现有检测方法因高维更新而无效。
method: 提出FedGraph，利用图结构对模型更新进行聚合，基于图特征检测恶意更新。
result: 实验证明FedGraph在多种后门攻击下有效防御，优于现有方法。
conclusion: FedGraph为联邦微调大语言模型提供了实用的后门防御手段，增强了协同训练的安全性。
---

## Abstract
Federated fine-tuning of large language models (LLMs) enables collaborative training without sharing raw data, offering a promising solution to data scarcity and privacy concerns. However, this setting is highly vulnerable to backdoor attacks, where adversaries inject malicious updates that preserve normal performance on benign inputs but induce targeted responses when triggered. We first demonstrate that backdoor attacks remain effective in the federated LoRA fine-tuning scenario, exposing a critical security risk. We further show that existing federated learning defenses are inadequate, as the high dimensionality and entanglement of LLM updates undermine anomaly detection methods. To overcome these challenges, we introduce \textit{FedGraph}, a graph-based aggregation framework. FedGraph represents client updates as nodes in a dynamic graph, extracts topological features including Degree, Betweenness, and Closeness centrality, and uses these to construct low-dimensional fingerprints of client behavior. An unsupervised clustering process then separates malicious from benign participants. Extensive experiments confirm that FedGraph achieve state-of-the-art defense against LLM backdoor attacks, reducing the attack success rate to below 10\%, while delivering high detection accuracy (95.5\% on average) and low false positives (2.33\%), significantly outperforming existing defenses.

---

## 论文详细总结（自动生成）

由于提供的论文文本仅为 OpenReview 的验证页面，未能获取论文全文内容，以下总结完全基于论文标题、摘要及元数据信息，并尽可能结合常识推断，但部分细节可能缺失或不准确。若有需要，建议获取完整 PDF 后重新分析。

---

## 1. 研究背景与核心问题
- **联邦大语言模型微调**：联邦学习允许多方在不共享原始数据的情况下协同训练模型，以缓解数据稀缺和隐私顾虑，尤其适用于 LLM 的微调。
- **后门攻击威胁**：在此设定下，攻击者可通过注入恶意更新，使模型在正常输入上表现正常，但在包含特定触发模式的输入上产生恶意目标行为。
- **现有防御的不足**：作者指出，联邦 LLM 微调（尤其是基于 LoRA 的微调）面临严重后门攻击风险，而传统联邦学习防御方法因 LLM 更新具有高维度、强纠缠特性而失效，异常检测手段无法奏效。
- **核心问题**：如何有效检测并防御针对联邦 LLM 微调的后门攻击，保障模型安全。

## 2. 方法论：FedGraph 图聚合防御框架
- **核心思想**：将客户端上传的模型更新转化为动态图的节点，利用图拓扑特征捕捉客户端行为的结构异常，从而在无监督条件下分离恶意节点。
- **关键技术细节**（摘自摘要）：
  - **动态图构建**：每个客户端的更新被表示为图中的一个节点，节点间关系可能基于更新相似度或通信拓扑动态变化。
  - **拓扑特征提取**：计算图节点的多种中心性指标，包括 **度中心性（Degree）**、**介数中心性（Betweenness）** 和 **紧密中心性（Closeness）**，形成低维行为指纹。
  - **无监督聚类**：基于这些低维指纹，使用聚类方法自动将参与者划分为恶意与良性两类，无需预先知道攻击方式。
- **算法流程**（推测）：客户端上传更新 → 构建相似度图 → 提取各节点拓扑特征 → 聚类（例如 k-means 或谱聚类）→ 筛选出良性更新子集 → 聚合更新 → 更新全局模型。

## 3. 实验设计
- **场景与数据集**：摘要未具体列出所用数据集或领域，仅提到“联邦 LoRA 微调场景”和“广泛实验”。可能涉及标准的 NLU/NLG 任务，如文本分类、对话生成等（需原文核实）。
- **基准方法**：摘要中声称 FedGraph “显著优于现有防御”，但未列出具体对比防御方法的名称。推断可能包括 FL 领域中常见的鲁棒聚合方法（如 Krum、Multi-Krum、FoolsGold 等）或专门针对后门的防御（如 FLAME、RFA 等）。
- **评估指标**：攻击成功率（ASR）降低至 **10% 以下**；平均检测准确率达到 **95.5%**；误报率（FPR）仅 **2.33%**。此外，可能还评估了主任务性能保持情况。

## 4. 资源与算力
- 摘要及元数据中 **未明确提及** GPU 型号、数量及训练时长。鉴于需要微调大语言模型并进行多个防御方法的对比，推测使用多张高性能 GPU（如 A100 或 V100）和一定的计算时间，但具体信息缺失。

## 5. 实验数量与充分性
- 摘要仅提及“广泛实验”，未给出实验组数。为支撑 SOTA 声明，通常需在不同数据集、不同攻击方式（如多个触发模式、不同恶意客户端比例）、不同模型规模下进行测试，并包含消融实验（如改变聚类算法、特征组合）。目前无法判断实验是否充分，但从高分评分（9.0）和被拒 ICLR 2026 的元数据来看，评审可能认为实验有说服力但存在某些局限。

## 6. 主要结论与发现
- FedGraph 能有效防御联邦 LLM 微调中的后门攻击，将攻击成功率降至 10% 以下，同时保持低误报和高检测精度。
- 通过图拓扑特征构建低维指纹是解决 LLM 更新维度灾难的有效途径，优于现有异常检测防御。
- 该方法具有通用性，不依赖攻击先验知识，适合实用的联邦学习部署。

## 7. 方法优点
- **针对性强**：专门克服 LLM 更新高维、纠缠导致的防御失效问题。
- **拓扑视角创新**：首次将图中心性特征用于 FL 后门检测，能够捕获结构性的恶意行为。
- **无监督且通用**：不需要标签或已知攻击模式，可自适应多种后门策略。
- **性能优异**：在保持主任务精度的同时，ASR 大幅下降，FPR 很低，实用性高。

## 8. 不足与局限
- **信息不全**：由于未获得全文，无法评估实验覆盖范围、超参数敏感性、对非独立同分布（non-IID）数据的鲁棒性、以及攻击者可能针对图结构发起的自适应攻击。
- **潜在局限**（推测）：
  - 图构建方式可能依赖于客户端更新的相似度度量，高维稀疏更新下的相似度计算可能引入噪声。
  - 中心性特征的区分能力在恶意客户端比例较高或攻击者协同调整更新分布时可能下降。
  - 仅评估了 LoRA 微调，未验证其他参数高效微调方法或全量微调。
  - 聚类阈值的选择可能需要领域知识或额外调优。
- **应用限制**：要求服务端能够构建全连接图并计算全局拓扑特征，在超大规模客户端（跨设备 FL）下可能面临可扩展性挑战。

（完）
