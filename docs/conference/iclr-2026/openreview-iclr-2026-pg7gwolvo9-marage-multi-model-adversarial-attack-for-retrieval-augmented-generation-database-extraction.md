---
title: "MARAGE: Multi-Model Adversarial Attack for Retrieval-Augmented Generation Database Extraction"
title_zh: "MARAGE: 针对检索增强生成数据库提取的多模型对抗攻击"
authors: "Xiao Hu, Eric Liu, Weizhou Wang, Xiangyu Guo, David Lie"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=Pg7gwolvo9"
tags: ["query:priv-sec"]
score: 9.0
evidence: 针对RAG数据库的对抗性抽取攻击
tldr: 本文提出MARAGE，一种基于优化的RAG数据库抽取攻击方法，通过语义感知查询策略和对抗性字符串，实现对知识数据库的高覆盖检索和逐字提取，扩大了RAG抽取攻击的能力范围。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有RAG抽取攻击未能同时实现高覆盖检索和长文本逐字提取，攻击能力受限。
method: 设计语义感知查询选择策略优化检索多样性，并对每个查询附加对抗字符串强制逐字泄露数据。
result: 实验证明MARAGE能够高覆盖地抽取整个知识库，并准确还原长文本内容。
conclusion: 该方法揭示了RAG系统严重的数据泄露风险，为安全防御提供了新的攻击基准。
---

## Abstract
Retrieval-Augmented Generation (RAG) mitigates hallucinations in Large Language Models using externally retrieved data. Although useful, RAG can expose the retrieved data to extraction attacks. Previous work has demonstrated the feasibility of RAG extraction, but has failed to simultaneously ensure high-coverage retrieval of the entire knowledge database and verbatim extraction of lengthy retrieved data. To broaden attack capabilities, we propose MARAGE, an optimization-based RAG database extraction method. To obtain high-coverage retrieval, we propose a semantic-aware query selection strategy which optimizes the diversity of retrieved chunks from the database. We then employ an adversarial string appended to each query to force verbatim output of the retrieved RAG chunks. To adapt to the uniquely lengthy target of RAG databases, we introduce Primacy weighting, which prioritizes initial tokens in the optimization target to enhance the extraction capability of optimized adversarial strings. Our evaluations show that MARAGE outperforms both manual and optimization-based baselines across multiple LLMs and RAG databases. On an end-to-end RAG pipeline, MARAGE surpasses the manual attack baseline by 329 +- 165% in extracting RAG data. To understand why MARAGE is more effective than the baselines, we probe and analyze the model's internal state to isolate the benefit of our approach.

---

## 论文详细总结（自动生成）

# MARAGE: 针对检索增强生成数据库提取的多模型对抗攻击

## 1. 论文的核心问题与整体含义
- **研究背景**：检索增强生成（RAG）通过引入外部知识库来缓解大语言模型（LLM）的幻觉问题，但同时也将检索到的数据库内容暴露给用户，带来了数据泄露风险。
- **现有瓶颈**：先前的RAG抽取攻击研究验证了提取可行性，但未能同时实现两大目标——① 对整个知识库的高覆盖检索（即抽取出尽可能多的不同数据块）；② 对长文本的逐字精确提取（攻击者需要获得原样长内容而不仅是摘要）。
- **整体含义**：该工作提出一种更强的攻击方法MARAGE，揭示了RAG系统在优化对抗攻击下的严重数据泄露威胁，为安全防御设立新的攻击基准。

## 2. 论文提出的方法论
- **核心思想**：通过**语义感知的查询选择**实现高覆盖检索，并利用**对抗性后缀字符串**迫使模型逐字输出检索到的长文本块。
- **关键技术细节**：
  - **语义感知查询选择策略**：优化查询集合以最大化数据库中检索块的多样性，从而提升对知识库的整体覆盖度。
  - **对抗字符串附加**：在每个查询后附加一个优化出的对抗字符串，该字符串专门设计用于强制LLM逐字复现检索到的RAG数据块，而非进行总结或改写。
  - **Primacy weighting（优先权重）**：针对RAG数据库中目标文本异常长的特点，在优化对抗字符串时对目标序列的**起始tokens赋予更高权重**，使优化过程优先关注前部内容的逐字还原，从而提升长文本的整体提取能力。
- **算法流程（文字描述）**：
  1. 基于语义多样性目标生成一组查询；
  2. 为每个查询优化一条对抗后缀，优化目标为：当查询连同对抗后缀一起输入RAG系统时，模型输出与对应检索块的内容尽可能逐字匹配，且在损失函数中通过Primacy weighting放大起始token的惩罚；
  3. 组合所有提取到的输出，重建数据库内容。

## 3. 实验设计
- **数据集/场景**：在多个LLM与多个RAG数据库上进行测试，并在端到端RAG流水线中评估。具体数据库名称在现有摘要中未列出。
- **基准对比方法**：
  - **手工攻击基线（manual attack baseline）**：人工构造的查询提取攻击。
  - **基于优化的基线（optimization-based baselines）**：其他利用优化的抽取方法。
- **评估指标**：给出“提取RAG数据”的相对提升比例（329% ± 165%），表明用提取内容量或逐字匹配度来度量。

## 4. 资源与算力
- 原文摘要与提供材料中**未明确说明**使用的GPU型号、数量、训练时长等算力信息。推测实际论文中可能包含，但基于当前可获得的内容无法给出。

## 5. 实验数量与充分性
- **实验覆盖面**：涉及多个LLM和多个RAG数据库，至少包含端到端流水线上的对比，还包含内部状态探测分析来理解方法有效性来源。
- **推测实验量**：从描述看，至少完成了以下几组实验：
  - 不同LLM上的攻击效果对比；
  - 不同数据库上的攻击效果对比；
  - 与手工基线、优化基线的性能比较；
  - 消融分析（通过内部状态探测来分离各设计因素的贡献）。
- **充分性评价**：基于摘要信息，对比了多种基准，覆盖多模型、多库，并进行了机理分析，实验设计相对客观、公平。但具体数据集规模和重复次数未知。

## 6. 论文的主要结论与发现
- MARAGE在提取RAG数据上显著优于手工和现有优化攻击基线，在端到端流水线上超出手工攻击基线**329% ± 165%**。
- 语义感知查询选择和Primacy weighting是提升长文本逐字提取和高覆盖检索的关键设计。
- 通过对模型内部状态的分析，揭示了该方法为何比基线更有效（具体的归因结论在摘要中未展开，但指出通过探测分离了方法的增益来源）。
- 整体表明RAG系统面临严峻的数据抽取风险，现有防御可能不足以应对此类优化攻击。

## 7. 优点
- **方法论创新**：首次将高覆盖检索和长文本逐字提取两个目标统一在一个优化框架中，弥补了先前工作的能力缺口。
- **Primacy weighting设计**：针对RAG长文本特点调整优化权重，有针对性的技术贡献。
- **实验设计合理**：多模型、多库、端到端评估，并辅以内部状态探测，提供了对攻击机理的深入理解。
- **实际意义强**：为安全社区提供了新的攻击基准，能推动更有效的防御研究。

## 8. 不足与局限
- **信息不完整**：由于仅基于摘要，数据集、模型版本、具体超参数、对抗字符串长度限制等细节未知，难以评估实验的覆盖广度和可复现性。
- **防御侧缺失**：文中似乎侧重攻击，未提及攻击的防御方法或攻击在受保护RAG系统上的有效性。
- **应用限制**：攻击假设攻击者可以对查询附加任意后缀，且目标模型完全按检索块生成输出，现实中可能受输入过滤、输出长度限制等影响，但摘要未讨论这些实际障碍。
- **偏差风险**：如果只测试了有限类型的LLM或数据库结构，结论的外推性需要谨慎。

（完）
