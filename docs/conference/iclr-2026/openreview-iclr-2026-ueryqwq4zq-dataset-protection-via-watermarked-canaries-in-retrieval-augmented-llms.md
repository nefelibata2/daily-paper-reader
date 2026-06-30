---
title: Dataset Protection via Watermarked Canaries in Retrieval-Augmented LLMs
title_zh: 通过水印金丝雀保护检索增强型LLM中的数据集
authors: "Yepeng Liu, Xuandong Zhao, Dawn Song, Yuheng Bu"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=UERyQwQ4zq"
tags: ["query:priv-sec"]
score: 8.0
evidence: 引入水印金丝雀以保护RAG中数据集所有权，是一种安全缓解措施。
tldr: 检索增强生成（RAG）中数据集未经授权使用构成版权风险。本文提出CanaryTrace方法，通过插入水印金丝雀文档保护数据集所有权，可有效检测RAG是否违规使用了受保护数据。实验证明该方法在不修改原始数据的前提下实现高精度检测，为数据版权保护提供新思路。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: RAG系统可能未经授权使用IP数据集，缺乏有效的所有权检测手段。
method: 在数据中插入特制的水印金丝雀文档，利用RAG的检索特性进行成员推断。
result: 方法能高准确率检测出未经授权的数据集使用，且不影响原始数据。
conclusion: CanaryTrace为文本数据集在RAG环境中的版权保护提供可行方案。
---

## Abstract
Retrieval-Augmented Generation (RAG) has become an effective method for enhancing large language models (LLMs) with up-to-date knowledge. However, it may pose a significant risk of copyright infringement, as IP datasets may be incorporated into the knowledge database by malicious Retrieval-Augmented LLMs (RA-LLMs) without authorization. To protect the rights of the dataset owner, an effective dataset membership inference algorithm for RA-LLMs is needed. In this work, we introduce a novel approach, \textit{CanaryTrace}, to safeguard the ownership of text datasets and effectively detect unauthorized use by the RA-LLMs. Our approach preserves the original data completely unchanged while protecting it by inserting specifically designed canary documents into the IP dataset. These canary documents are created with synthetic content and embedded watermarks to ensure uniqueness, consistency, and statistical provability. During the detection process, unauthorized usage is identified by querying the canary documents and analyzing the responses of RA-LLMs for statistical evidence of the embedded watermark. Our experimental results demonstrate high query efficiency, detectability, and consistency, along with minimal perturbation to the original dataset, all without compromising the performance of the RAG system.

---

## 论文详细总结（自动生成）

# 论文《Dataset Protection via Watermarked Canaries in Retrieval-Augmented LLMs》中文总结

## 1. 研究动机与核心问题
- **背景**：检索增强生成（RAG）通过为大型语言模型（LLM）注入外部知识库，有效提升了回答的时效性与事实性。然而，恶意 RA‑LLM（检索增强型大模型）可能在未授权的情况下将受知识产权保护的数据集纳入其知识库，从而构成版权侵权风险。
- **核心问题**：数据集所有者需要一种可有效检测其文本数据集是否被 RA‑LLM 违规使用的方法，即实现“数据集成员推断”，以便在 RAG 场景下保护数据版权。
- **整体含义**：该工作通过引入“水印金丝雀”概念，在不修改原始数据内容的前提下，向数据集中插入特殊构造的文档（金丝雀），使得所有者能够通过查询黑盒 RA‑LLM 的响应，统计性地检测出数据集是否被未经授权地索引和使用。

## 2. 方法论
- **核心思想**：设计并插入一种名为“金丝雀”（canary）的合成文档，文档中嵌入可检测的水印。这些金丝雀与真实数据一同存入数据集。一旦恶意 RA‑LLM 将该数据集用作知识库，金丝雀文档就会被检索并在生成过程中留下痕迹；所有者通过向 RA‑LLM 发出特定查询，分析返回内容中的水印统计证据，实现高置信度的侵权判定。
- **关键技术细节**（根据摘要推断）：
  - **金丝雀文档生成**：使用合成内容创建金丝雀文档，保证内容与真实数据不重叠，避免干扰原始数据使用；同时在文档中嵌入可统计验证的水印（例如某些词频模式、token 序列特征等）。
  - **插入机制**：将金丝雀文档静默地添加到待保护的数据集中，对原始数据完全不做修改，保持其质量和可用性。
  - **检测流程**：
    1. 所有者向目标 RA‑LLM 发出设计好的查询，这些查询会触发检索系统召回金丝雀文档。
    2. 分析 RA‑LLM 的生成响应，提取水印信号（如特定 n‑gram 的出现频率、token 分布偏移等）。
    3. 基于假设检验（如二项检验、似然比检验）计算统计显著性，判断数据集是否被使用。
- **公式/算法流程**：摘要未给出具体公式，但提到“统计可证明性”（statistical provability），暗示采用了假设检验框架，设置零假设（H₀：数据集未被使用），通过查询返回的水印证据计算 p 值，低于阈值则拒绝零假设，输出侵权判定。

## 3. 实验设计
由于论文原文未能完整提取，详细实验设计仅能从摘要和元数据推断：
- **使用数据/场景**：可能包含若干文本数据集（如通用知识、对话、特定领域文档等），用于构造 RAG 知识库，模拟授权和未授权使用场景。
- **评估基准（Benchmark）**：
  - 检测准确率（真阳性率、假阳性率）
  - 查询效率（需要多少次查询才能达到可靠判定）
  - 可检测性（detectability，指水印信号在生成文本中的显著程度）
  - 一致性（consistency，指不同查询、不同模型或不同配置下检测结果的稳定程度）
  - 对 RAG 系统性能的影响（金丝雀插入后的生成质量变化）
- **对比方法**：未明确列出，可能包括无保护的空白对照，或其他数据集水印/成员推断方法（如基于文本指纹、数据污染检测等）。由于原文未提供，无法详述。

## 4. 资源与算力
- **原文信息缺失**：用户提供的提取文本中未包含算力消耗、GPU 型号与数量、训练时长等内容。论文摘要及元数据同样未提及这些信息。因此无法给出具体算力评估。

## 5. 实验数量与充分性
- **无法准确评估**：由于缺乏全文，无法获知实验总数、消融研究、不同数据集规模、不同检索器/LLM 组合等细节。
- 根据摘要中“实验结果表明高查询效率、可检测性和一致性，且对原始数据扰动极小”的描述，推测作者可能进行了多组实验以验证各项指标，但具体数量未知。若需判断充分性，必须参阅完整论文。

## 6. 主要结论与发现
- **方法可行性**：CanaryTrace 能够在不改动原始数据的前提下，有效检测 RA‑LLM 对受保护数据集的未授权使用。
- **性能表现**：实验显示该方法实现了高检测准确率、低查询次数即可达到统计显著性，且不会降低 RAG 系统本身的生成质量。
- **实际意义**：该方案为文本数据集在 RAG 环境下的版权保护提供了一种轻量、隐蔽、可事后验证的实用手段。

## 7. 优点与亮点
- **完全无侵入性**：原始数据零修改，不影响正常使用和模型性能，易于被数据所有者采纳。
- **黑盒检测**：仅需查询访问 RA‑LLM，不需了解其内部参数、检索库或模型结构，通用性强。
- **统计可证明**：检测结果不是黑箱判断，而是有统计显著性支撑，降低了误报风险。
- **隐蔽性好**：金丝雀文档以合成内容出现，难以被恶意用户察觉或过滤，增强了保护的实际效力。

## 8. 不足与局限
- **实验细节不明**：由于无法获取全文，难以评估实验覆盖的广度和公平性，如不同领域数据集、不同检索策略、不同 LLM 规模等是否充分验证。
- **依赖检索触发**：检测效果高度依赖金丝雀被检索到的概率，若攻击者刻意过滤或屏蔽特定查询，可能降低可检测性（文中未说明对抗性防御的鲁棒性）。
- **统计假设的敏感性**：水印检测需预设统计模型，可能在低检索命中率或高语言模型随机性下面临假阴性风险。
- **插入策略约束**：金丝雀文档需精心设计，避免与真实数据产生语义冲突，这在特定垂直领域可能面临挑战。
- **适用范围的推广性**：当前仅讨论文本数据集，对于多模态、代码等数据类型的扩展尚待验证。

（完）
