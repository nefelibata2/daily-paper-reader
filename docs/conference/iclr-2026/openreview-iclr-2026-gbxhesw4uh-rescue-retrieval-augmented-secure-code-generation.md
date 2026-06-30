---
title: "RESCUE: Retrieval Augmented Secure Code Generation"
title_zh: "RESCUE: 检索增强安全代码生成"
authors: "Jiahao Shi, Tianyi Zhang"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=gbxhesw4UH"
tags: ["query:priv-sec"]
score: 7.0
evidence: 利用检索增强生成提升大语言模型代码生成安全性的框架
tldr: 本文提出RESCUE框架，通过混合知识库构建和安全语义感知检索，增强大语言模型生成安全代码的能力，解决了传统RAG中安全文档噪声大、安全语义捕捉不足的问题。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 大语言模型仍常生成含安全漏洞的代码，传统RAG设计无法有效利用安全知识。
method: 设计RESCUE框架，结合LLM辅助的聚类-摘要蒸馏与程序切片构建混合知识库，实现安全导向检索。
result: 实验表明RESCUE显著提升了代码生成的安全性，减少了漏洞。
conclusion: 该框架为安全代码生成提供了一种有效的检索增强方案，推进了LLM在安全领域的应用。
---

## Abstract
Despite recent advances, Large Language Models (LLMs) still generate vulnerable code. 
Retrieval-Augmented Generation (RAG) has the potential to enhance LLMs for secure code generation by incorporating external security knowledge. However, the conventional RAG design struggles with the noise of raw security-related documents, and existing retrieval methods overlook the significant security semantics implicitly embedded in task descriptions.
To address these issues, we propose \textsc{Rescue}, a new RAG framework for secure code generation with two key innovations. 
First, we propose a hybrid knowledge base construction method that combines LLM-assisted cluster-then-summarize distillation with program slicing, producing both high-level security guidelines and concise, security-focused code examples. Second, we design a hierarchical multi-faceted retrieval that traverses the constructed knowledge base from top to bottom and integrates multiple security-critical facts at each hierarchical level, ensuring comprehensive and accurate retrieval. 
We evaluated \textsc{Rescue} on four benchmarks and compared it with five state-of-the-art secure code generation methods on six LLMs. The results demonstrate that \textsc{Rescue} improves the SecurePass@1 metric by an average of 4.8 points, establishing a new state-of-the-art performance for security. Furthermore, we performed in-depth analysis and ablation studies to rigorously validate the effectiveness of individual components in \textsc{Rescue}. Our code is available at \url{https://github.com/steven1518/RESCUE}.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **背景与动机**：大语言模型在代码生成中仍频繁产生安全漏洞，常规的检索增强生成虽能引入外部安全知识，但面临两大难点：
  - 原始安全文档中的噪声干扰严重，难以直接作为检索源。
  - 现有检索方法忽略任务描述中隐含的深层安全语义，导致检索结果不够精准。
- **整体含义**：本文提出 **RESCUE** 框架，通过构建高质量的混合知识库并设计安全语义感知的检索机制，有效提升了检索增强生成在安全代码生成上的性能，为 LLM 的安全应用提供了一条可行路径。

## 2. 论文提出的方法论

- **核心思想**：将安全知识蒸馏为“高纲领指南 + 精简代码示例”，并以层级化、多面化的方式检索与当前编码任务最相关的安全事实。
- **关键技术细节**：
  - **混合知识库构建**：
    - **LLM 辅助的聚类-摘要蒸馏**：对原始安全文档进行聚类，再利用大语言模型生成简明、高层的安全指南。
    - **程序切片**：从安全相关的代码片段中抽取出与安全缺陷直接相关的精简代码示例，形成低层次、聚焦安全的关键示例。
  - **分层多面检索**：
    - 自顶向下遍历知识库（从高层指南到具体代码示例）。
    - 在每一层级中整合多个安全关键事实（即“多面”），保证检索结果全面且精确，弥补传统检索对安全语义捕捉不足的缺陷。
- **算法流程描述**（文字化）：
  1. 离线构建：对安全语料进行聚类 → LLM 摘要 → 程序切片 → 形成混合知识库。
  2. 在线生成：接收编码任务描述 → 分层多面检索从知识库中提取相关安全信息 → 将检索到的上下文增强后传入大语言模型，生成安全代码。

## 3. 实验设计

- **数据集/场景**：在 **四个基准** 上评测（论文未列出具体名称，但从语境判断应为安全代码生成相关的公开数据集）。
- **对比方法**：与 **五种当前最先进的 Secure Code Generation 方法** 进行比较。
- **基础模型**：在 **六个主流大语言模型**（模型名称未在摘要列出）上验证框架的有效性。
- **评估指标**：主要采用 `SecurePass@1`（一次生成通过安全检查的概率），关注安全性的提升。

## 4. 资源与算力

- 本文提供的摘要及元数据中 **未明确说明 GPU 型号、数量、训练时长** 等算力细节。如需了解具体资源配置，需查阅论文正文。

## 5. 实验数量与充分性

- **实验组合**：摘要提及 “in-depth analysis and ablation studies”，可推知进行了：
  - 多基准（4个）× 多模型（6个）× 多方法（5个对比+RESCUE）的全量对比。
  - 针对 RESCUE 各组件的消融实验（如去除聚类-摘要、去除程序切片、改用扁平检索等）。
- **公平性与充分性**：在多个模型和基准上与 SOTA 进行对比，并进行严谨的消融分析，实验设计较为全面客观，能有力支撑核心主张。

## 6. 论文的主要结论与发现

- RESCUE 在 **SecurePass@1** 平均提升 **4.8 点**，在安全代码生成任务上取得 **新的最优性能**。
- 混合知识库构建和分层多面检索是性能增益的关键来源，二者均对减少漏洞有显著贡献。
- 验证了通过结构化知识增强和语义感知检索，可以大幅提高大语言模型在安全敏感场景下的可靠性。

## 7. 优点

- **方法论创新**：将聚类-摘要蒸馏与程序切片结合，有效降低安全知识的噪声，同时保留关键信息。
- **检索机制贴合任务**：分层多面检索显式考虑安全语义，使检索到的示例与高层指南高度相关，避免了传统 RAG 的盲目检索。
- **实验充分**：涵盖 4 个基准、6 个模型、5 个对比方法，辅以消融研究，证据链完整。
- **可复现性**：论文提供了代码仓库链接，便于后续研究验证。

## 8. 不足与局限

- **摘要未提及的潜在局限**（基于常识推断）：
  - 构建混合知识库依赖大语言模型的摘要能力，若初始安全文档质量差或领域特殊，蒸馏效果可能受限。
  - 分层检索的级联设计可能引入额外推理延迟，实时性影响未在摘要中说明。
  - 四个基准的具体性质未知，未见不同编程语言或漏洞类型的泛化验证细节。
- **实验覆盖局限**：未说明在私有或工业级代码库上的表现，跨域迁移性存疑。
- **偏差风险**：知识库构建过程中使用的 LLM 本身可能存在安全偏见，极端情况下可能产生误导性指南。

（完）
