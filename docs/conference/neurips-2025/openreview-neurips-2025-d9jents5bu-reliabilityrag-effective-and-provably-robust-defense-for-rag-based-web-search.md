---
title: "ReliabilityRAG: Effective and Provably Robust Defense for RAG-based Web-Search"
title_zh: "ReliabilityRAG: 面向基于RAG的Web搜索的有效且可证明鲁棒防御"
authors: "Zeyu Shen, Basileal Yoseph Imana, Tong Wu, Chong Xiang, Prateek Mittal, Aleksandra Korolova"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=D9JeNTs5Bu"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出利用可靠性信息的RAG web搜索防御框架，抵御提示注入攻击
tldr: 基于RAG的搜索系统如Google AI Overview易受检索语料攻击，需利用可靠性信号。ReliabilityRAG框架显式利用文档排名等先验可靠性信息，结合可证明鲁棒聚合，在抵御提示注入等攻击的同时保持生成质量。实验表明该方法在Web搜索场景下显著提升了对抗鲁棒性，为RAG安全部署提供了理论保障。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: RAG搜索系统面临检索语料注入攻击，防御可受益于文档可靠性信号，但现有方法缺乏有效利用。
method: 提出ReliabilityRAG，显式建模文档可靠性分数，并设计可证明鲁棒聚合算法对抗攻击。
result: 在模拟Google搜索实验中，ReliabilityRAG有效抵御攻击，且生成质量接近无攻击基线。
conclusion: ReliabilityRAG为RAG搜索提供了可证明的鲁棒防御，提升了实际部署的可信度。
---

## Abstract
Retrieval-Augmented Generation (RAG) enhances Large Language Models by grounding their outputs in external documents. These systems, however, remain vulnerable to attacks on the retrieval corpus, such as prompt injection. RAG-based search systems (e.g., Google’s Search AI Overview) present an interesting setting for studying and protecting against such threats, as defense algorithms can benefit from built-in reliability signals—like document ranking—and represent a non-LLM challenge for the adversary due to decades of work to thwart SEO.

Motivated by, but not limited to, this scenario, this work introduces ReliabilityRAG, a framework for adversarial robustness that explicitly leverages reliability information of retrieved documents.

Our first contribution adopts a graph-theoretic perspective to identify a ``consistent majority'' among retrieved documents to filter out malicious ones. We introduce a novel algorithm based on finding a Maximum Independent Set (MIS) on a document graph where edges encode contradiction. Our MIS variant explicitly prioritizes higher-reliability documents and provides provable robustness guarantees against bounded adversarial corruption under natural assumptions. Recognizing the computational cost of exact MIS for large retrieval sets, our second contribution is a scalable weighted sample and aggregate framework. It explicitly utilizes reliability information, preserving some robustness guarantees while efficiently handling many documents.

We present empirical results showing ReliabilityRAG provides superior robustness against adversarial attacks compared to prior methods, maintains high benign accuracy, and excels in long-form generation tasks where prior robustness-focused methods struggled. Our work is a significant step towards more effective, provably robust defenses against retrieved corpus corruption in RAG.

---

## 论文详细总结（自动生成）

# ReliabilityRAG：面向基于 RAG 的 Web 搜索的有效且可证明鲁棒防御

## 1. 论文的核心问题与整体含义
- **核心问题**：基于检索增强生成（RAG）的大语言模型（LLM）虽然能通过外部文档提高准确性，但其检索语料库容易受到**提示注入**等对抗攻击，导致输出被恶意操控。
- **场景聚焦**：以基于 RAG 的搜索引擎（如 Google AI Overview）为典型场景。这类系统天然携带**内置可靠性信号**（如文档排名），且攻击者面临搜索引擎优化（SEO）等非 LLM 层面的防御挑战，为设计更有效的防御提供了新机会。
- **研究动机**：现有防御方法未能有效利用文档的**先验可靠性信息**，亦缺少**可证明的鲁棒性保证**。作者旨在填补这一空白，既提升防御有效性，又为安全部署提供理论保障。

## 2. 方法论
- **核心思想**：构建 **ReliabilityRAG** 框架，显式地利用检索文档的可靠性分数，通过图论方法寻找文档间“一致多数”，以过滤恶意文档，并提供可证明鲁棒性。
- **关键技术细节**：
  - **图构建**：将文档作为节点，若两文档**内容矛盾**则建立边，形成文档关系图。
  - **基于最大独立集（MIS）的过滤**：在图上求解一个加权最大独立集问题。算法变体**优先选择高可靠性文档**，使得选出的集合内部无矛盾，并尽可能保留可信的多数信息。
  - **可证明鲁棒保证**：在一定的自然假设下（如攻击者只能污染有限数量的文档），该 MIS 变体能够从数学上保证过滤掉恶意文档，给出对抗有界破坏的鲁棒性上限。
  - **可伸缩扩展**：考虑到精确求解 MIS 在大型检索集上计算开销大，进一步提出**加权采样与聚合**框架，显式使用可靠性权重，在保留部分鲁棒性保证的同时高效处理大量文档。
- **算法流程（文字描述）**：
    1. 对检索到的文档计算或获取先验可靠性分数（例如排名分）。
    2. 构建矛盾图，根据文档间的冲突添加边。
    3. 执行加权 MIS 算法（或面向大规模集的采样聚合）选出可信文档子集。
    4. 仅将选定文档送入 LLM 生成最终回答。

## 3. 实验设计
- **数据集/场景**：在**模拟 Google 搜索**的环境下进行评估，具体底层数据集名称未在摘要中明确给出。任务涉及长文本生成场景。
- **评测基准**：以**无攻击基线的生成质量**和**对抗攻击下的鲁棒性**作为核心指标，特别关注长文本生成任务上的表现。
- **对比方法**：与先前的防御方法（prior methods）以及先前专注于鲁棒性的方法（prior robustness-focused methods）进行直接比较，但方法名称未在摘要中列举。

## 4. 资源与算力
- 摘要及提供的元数据中**未提及**任何 GPU 型号、数量、训练或推理时长等计算资源信息。

## 5. 实验数量与充分性
- 论文展示了足够的实证结果（empirical results），具体实验组数（如不同对抗强度、不同文档集规模、消融实验等）未在摘要中展开。
- **充分性评价**：从摘要结论看，实验覆盖了鲁棒性、良性准确性、长文本生成等多个维度，并进行了多种方法对比，**看似较充分**。但因缺乏确切的实验表、数及统计检验信息，无法对公平性和客观性做出精确判断。

## 6. 主要结论与发现
- ReliabilityRAG 相比先前方法，在抵御对抗攻击时提供了**显著更优的鲁棒性**，同时**保持了高良性准确性**（接近无攻击基线）。
- 尤其在**长文本生成任务**上，ReliabilityRAG 表现出色，解决了先前鲁棒性方法在此类任务中表现不佳的问题。
- 该工作是将**可证明鲁棒防御**应用于 RAG 检索语料污染攻击的重要一步，提升了 RAG 搜索系统实际部署的可信度。

## 7. 优点
- **理论保障**：提出了一种具有可证明鲁棒性的图算法，在对抗有界污染下提供数学保证，区别于纯经验方法。
- **实用信号利用**：显式整合文档排名等先验可靠性信息，贴合搜索引擎的实际特征，且不依赖特定 LLM 架构。
- **可伸缩性设计**：同时关注精确性与效率，通过采样聚合框架使方法能处理大规模检索集，增强了实用性。
- **长文本能力**：解决了以往鲁棒防御在长文本生成上的薄弱环节，对需要综合多文档信息的摘要类任务尤为有效。

## 8. 不足与局限
- **信息缺失严重**：摘要及元数据未提供数据集、对比方法清单、算力成本等关键实验细节，难以评估方法的可复现性与实际成本。
- **假设依赖性**：可证明鲁棒性依赖于“自然假设”（如攻击只能污染少量文档、可靠性信号本身可靠），现实中这些假设可能被打破（例如排名可被操纵），文中对假设失效情况讨论不详。
- **图构建成本**：矛盾判定规则可能带来开销与噪声，尤其在开放域文本中定义“矛盾”并非易事，可能影响图质量。
- **应用限制**：重点验证场景为 Web 搜索，向其他 RAG 应用（如私有知识库、对话系统）的泛化性尚未明确。

（完）
