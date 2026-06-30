---
title: "Pisces: Cryptography-based Private Retrieval-Augmented Generation with Dual-Path Retrieval"
title_zh: Pisces：基于密码学的双路检索私有检索增强生成
authors: "Xiaojian Liang, Lushan Song, Shishuai Du, Weicheng Zhu, Tan Li Hui Faith, Jun Jie Sim, Haibing Jin, Zhenghao Wu, Yingting Liu, Xin Zhang, Jiang-Ming Yang, Pu Duan"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=Re3A6vzCTC"
tags: ["query:priv-sec"]
score: 9.0
evidence: 首个实用的基于密码学的RAG框架，保护双路检索中的查询和文档隐私。
tldr: 针对RAG中用户查询和知识库文档的隐私问题，提出Pisces框架，采用不经意过滤和同态加密等技术实现双路检索的隐私保护，在语义检索和精确匹配路径上保障隐私且降低成本。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: RAG中查询和文档可能含敏感信息，现有方法未能同时保护两者。
method: Pisces使用粗到细策略，通过不经意过滤器私密选择候选集，结合安全检索协议。
result: 实现实用的隐私保护RAG，开销降低，检索质量高。
conclusion: Pisces证明了密码学在RAG隐私保护中的实用可行性。
---

## Abstract
Retrieval-augmented generation (RAG) enhances the response quality of large language models (LLMs) when handling domain-specific tasks, yet raises significant privacy concerns. This is because both the user query and documents within the knowledge base often contain sensitive or confidential information. To address these concerns, we propose $\texttt{Pisces}$, the first practical cryptography-based RAG framework that supports dual-path retrieval, while protecting both the query and documents. Along the semantic retrieval path, we reduce computation and communication overhead by leveraging a coarse-to-fine strategy. Specifically, a novel oblivious filter is used to privately select a candidate set of documents to reduce the scale of subsequent cosine similarity computations. For the lexical retrieval path, to reduce the overhead of repeatedly invoking labeled PSI, we implement a multi-instance labeled PSI protocol to compute term frequencies for BM25 scoring in a single execution. $\texttt{Pisces}$ can also be integrated with existing privacy-preserving LLM inference frameworks to achieve end-to-end privacy. Experiments demonstrate that $\texttt{Pisces}$ achieves retrieval accuracy comparable to the plaintext baselines, within a 1.87% margin.

---

## 论文详细总结（自动生成）

# Pisces：基于密码学的双路检索私有检索增强生成（论文总结）

## 1. 论文的核心问题与整体含义

- **研究背景**：检索增强生成（RAG）可显著提升大语言模型在领域任务中的回答质量，但存在隐私风险——用户查询和知识库中的文档往往包含敏感或机密信息。
- **核心问题**：现有方法无法在**同时保护用户查询隐私和知识库文档隐私**的前提下，实现实用的检索增强生成。
- **论文含义**：提出 `Pisces`，首个实用的基于密码学的 RAG 框架，支持双路检索（语义检索 + 词汇检索），在保护双方隐私的同时保持较高的检索质量，并可与私有 LLM 推理系统结合实现端到端隐私。

## 2. 方法论

`Pisces` 采用密码学技术保护双路检索中的查询和文档隐私，核心思想与关键技术如下：

- **整体策略**：针对语义检索路径和词汇检索路径分别设计隐私保护协议，通过 **“粗到细”** 等策略降低计算与通信开销。
- **语义检索路径**：
  - 使用一种新型的 **不经意过滤器（Oblivious Filter）**，隐私地筛选出一组候选文档，极大缩减后续余弦相似度计算的规模。
  - 后续仅对候选集进行安全的高精度相似度计算，从而在保证隐私的同时显著降低开销。
- **词汇检索路径**：
  - 为了实现 BM25 等词汇匹配评分，需要计算词频。论文设计了一种 **多实例标签 PSI 协议（Multi-Instance Labeled PSI）**，在一次执行中联合计算多个词项的频率，避免反复调用标签 PSI，从而减少通信轮次和计算量。
- **系统集成**：`Pisces` 可被嵌入现有的隐私保护 LLM 推理框架中，实现从检索到生成的端到端隐私保护。

## 3. 实验设计

- **数据集与场景**：暂未在元数据中给出具体数据集名称，原文应包含用于评估检索质量的标准 RAG 基准或自定义敏感知识库场景。
- **对比方法**：与明文基线进行对比（plaintext baselines），衡量隐私保护条件下的检索精度损失。
- **评估指标**：主要采用检索精度指标，报告了 `Pisces` 与明文基线之间的精度差距。

## 4. 资源与算力

- 提供的元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长或推理硬件配置。若原文包含实验环境配置，需查阅完整论文。

## 5. 实验数量与充分性

- 元数据未详细罗列实验组数，但摘要提到实验表明 `Pisces` 检索精度与明文基线的差距在 **1.87% 以内**。
- 从动机和结论推测，实验可能覆盖：
  - 不同检索路径（语义 vs. 词汇）的消融研究；
  - 通信/计算开销的详细测量；
  - 与纯明文方案在多项 RAG 指标上的对比；
- 鉴于该工作宣称实现首个实用密码学 RAG，预计实验设计较充分，涵盖效率、精度及安全性分析，但无具体内容无法判断是否存在偏差风险。

## 6. 主要结论与发现

- `Pisces` 在保护用户查询和文档隐私的条件下，检索准确率与明文方案的差距仅为 **1.87%**，证明基于密码学的隐私保护 RAG 已具备实用价值。
- 通过粗到细策略和多实例标签 PSI 等优化，计算与通信开销被有效降低，使系统在现实场景中可行。
- 该框架可无缝集成私有 LLM 推理，实现端到端隐私保障。

## 7. 优点

- **首个实用方案**：在 RAG 场景中同时保护查询和文档隐私，并达成实用效率，属开创性工作。
- **双路径覆盖**：同时支持语义检索和词汇检索，满足复杂 RAG 任务需求。
- **精巧的密码学优化**：不经意过滤器和多实例标签 PSI 的设计显著降低开销，体现出密码工程的优势。
- **可组合性**：与现有私有 LLM 推理框架兼容，为构建端到端隐私 RAG 系统铺平道路。
- **精度损失极小**：仅 1.87% 的明文性能差距，接近无损。

## 8. 不足与局限

- **具体实验细节未知**：由于仅提供元数据，无法评估数据集规模、硬件平台、对比方法的全面性和公平性，亦无法确认是否涵盖真实大规模知识库场景。
- **实时性挑战**：密码学操作虽然被优化，但在极高并发或超大规模语料下仍可能成为瓶颈，实用业务中的延迟阈值需进一步验证。
- **安全性模型依赖**：安全性依赖于基础密码学假设（如同态加密、不经意传输等），可能存在侧信道或实现层面的风险，论文是否给出完整安全性证明尚未可知。
- **功能限制**：文中仅涉及检索阶段隐私保护，生成阶段的隐私由外部 LLM 推理框架负责，若生成框架自身不隐私，则无法实现完整保护，需用户注意整体部署。

（完）
