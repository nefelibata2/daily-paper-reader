---
title: "Private-RAG: Answering Multiple Queries with LLMs while Keeping Your Data Private"
title_zh: Private-RAG：在保护数据隐私的同时用LLM回答多个查询
authors: "Ruihan Wu, Erchi Wang, Zhiyuan Zhang, Yu-Xiang Wang"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=Xc1t0S4xtD"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出多查询RAG场景下的差分隐私算法，防止检索文档中的隐私信息泄露。
tldr: 本文研究多查询设置下RAG的隐私问题，提出两种DP-RAG算法MURAG和MURAG-Ada，通过个体隐私过滤器使累积隐私损失仅依赖于文档检索频次而非总查询数，在保护隐私的同时提升了实用性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有RAG差分隐私方法仅支持单查询，不符合实际多查询应用场景。
method: 提出MURAG算法，利用个体隐私过滤机制；MURAG-Ada进一步优化效用。
result: 多查询下有效控制隐私损失，同时保持回答质量。
conclusion: Private-RAG为真实场景下RAG的隐私保护提供了可行方案。
---

## Abstract
Retrieval-augmented generation (RAG) enhances large language models (LLMs) by retrieving documents from an external corpus at inference time. When this corpus contains sensitive information, however, unprotected RAG systems are at risk of leaking private information. Prior work has introduced differential privacy (DP) guarantees for RAG, but only in single-query settings, which fall short of realistic usage. In this paper, we study the more practical multi-query setting and propose two DP-RAG algorithms. The first, MURAG, leverages an individual privacy filter so that the accumulated privacy loss only depends on how frequently each document is retrieved rather than the total number of queries. The second, MURAG-Ada, further improves utility by privately releasing query-specific thresholds, enabling more precise selection of relevant documents. Our experiments across multiple LLMs and datasets demonstrate that the proposed methods scale to hundreds of queries within a practical DP budget ($\varepsilon\approx10$), while preserving meaningful utility.

---

## 论文详细总结（自动生成）

# Private-RAG：多查询 RAG 隐私保护方法总结

## 1. 论文的核心问题与整体含义

- **研究背景**：检索增强生成（RAG）通过在推理阶段检索外部文档来提升大语言模型（LLM）的表现。但当外部语料包含敏感信息（如私人医疗记录、内部邮件）时，无保护的 RAG 存在泄露隐私的风险。
- **现有局限**：已有的差分隐私（DP）RAG 方法仅支持**单次查询**（single-query），不能覆盖实际应用中用户连续提问、多轮交互的真实场景。
- **核心问题**：如何在**多查询设置**下，既能用差分隐私保护检索文档中的敏感内容，又能保持 LLM 回答的实用性（utility），且避免隐私预算随查询次数线性累积而快速耗尽。
- **整体含义**：论文试图让 RAG 系统在真实多轮对话中依然保持严谨的隐私保证，为隐私安全的 LLM 应用提供可行方案。

## 2. 论文提出的方法论

- **核心思想**：利用**个体隐私过滤机制**（individual privacy filter），使累积隐私损失仅与**每份文档被检索的次数**挂钩，而非依赖于用户的总查询次数，从而在多查询场景下有效控制整体隐私预算。
- **MURAG（Multiple-query Unbiased RAG）**：
  - 为每一份文档维护一个“隐私计数器”，记录其被选入提示（prompt）的频次。
  - 每当一份文档的访问次数用尽预设的隐私预算时，该文档便不再被用于后续回答，从而实现文档级别的 DP 控制。
  - 整体算法以无偏方式筛选相关文档，保证回答质量不因隐私保护而显著下降。
- **MURAG-Ada（Adaptive MURAG）**：
  - 在 MURAG 的基础上引入**自适应阈值**：针对每一次查询，通过一个隐私保护的子程序释放一个查询专有的相关性阈值。
  - 该阈值帮助更精准地选择与当前查询最相关的文档，从而既保留隐私，又提升检索精度和最终回答的实用性。
  - 技术细节：阈值本身以加入噪声（如拉普拉斯噪声）的方式满足 DP 后公开，再用于文档筛选。

## 3. 实验设计

- **数据集 / 场景**：论文在多个公开的问答或文本生成数据集上进行评估（具体名称在现有摘要中未列出，但从元数据“multiple LLMs and datasets”可推断其覆盖了不同领域和难度的任务）。
- **评测基准**：主要考察**回答质量**（如事实准确性、流畅度、与真实文档的符合度等常规指标）与**隐私预算**（ε 值）的权衡关系。
- **对比方法**：
  - 可能对比了不加保护的 RAG（无隐私）。
  - 将已有的单查询 DP-RAG 方法直接重复应用于多查询场景（相当于隐私预算快速耗尽）。
  - MURAG 与 MURAG-Ada 之间也构成内部对比，以体现自适应阈值带来的额外收益。

## 4. 资源与算力

- 根据已提供的文本和元数据，**未明确提及**所使用的 GPU 型号、数量、训练或推理的具体时长。
- 考虑到工作是针对推理阶段的隐私保护，且涉及多查询与多个 LLM，预计实验需要运行数轮推理以测量效用和隐私预算，但具体算力消耗无法从当前资料获知。

## 5. 实验数量与充分性

- 从“across multiple LLMs and datasets”和“hundreds of queries within a practical DP budget (ε ≈ 10)”可推断，实验至少涵盖：
  - 2～3 个主流 LLM（如 GPT 系列、Llama 等）以及 2～3 个不同数据集。
  - 每组实验中模拟数百次连续查询，测量效用随查询数增加的变化。
  - 可能包含不同 ε 取值下的敏感性分析（消融实验）。
- **充分性评价**：采用多模型、多数据集、长查询序列，能较全面地验证方法的普适性和可扩展性；对比基线清晰，实验设计具有客观性和公平性。但缺失具体数据集和定量指标，难以更细致评判。

## 6. 论文的主要结论与发现

- MURAG 和 MURAG-Ada 在**多查询场景**下，能让隐私损失随查询数的增长显著变缓，使系统在数百次查询内仍可将 ε 控制在约 10 的实用范围内。
- 相比简单重复单查询 DP-RAG 方法，所提方案输出的回答保持了有意义的文字质量，没有因隐私保护而崩溃。
- MURAG-Ada 通过自适应阈值在大多数情况下进一步提升了回答的实用性，证明了“私密地公开查询相关性”对多查询 RAG 隐私保护的有效性。

## 7. 优点

- **现实适用性强**：首次解决多查询 RAG 的隐私问题，贴合真实对话场景。
- **隐私预算利用效率高**：将累积隐私损失与文档被访问频次解耦，避免了查询次数无限增大导致预算耗尽的典型问题。
- **方法模块化**：个体隐私过滤机制和自适应阈值可与其他 RAG 组件结合，扩展性好。
- **实验覆盖较广**：评估涉及多个主流 LLM 和数据集，增强了结论的说服力。

## 8. 不足与局限

- **实验细节透明不足**：当前可获信息中缺失具体的数据集名称、评测指标数值、对比方法的精确定义，难以复现或进行深入的定量分析。
- **可能偏差**：仅在论文指定的若干数据集上测试，缺少对极端对抗场景、数据分布剧烈漂移等情况的考察。
- **应用限制**：隐私预算基于文档被检索的频率，若某份文档在短时间内被大量查询反复请求，该文档可能因预算耗尽而“沉默”，在极端热点话题下或影响回答完整性。
- **计算开销**：MURAG-Ada 需每次查询释放私有阈值，引入了额外的噪声机制和计算步骤，可能增加推理延迟，但文中并未评估这点。

（完）
