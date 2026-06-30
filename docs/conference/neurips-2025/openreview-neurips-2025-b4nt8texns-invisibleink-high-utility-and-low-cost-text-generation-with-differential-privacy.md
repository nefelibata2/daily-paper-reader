---
title: "InvisibleInk: High-Utility and Low-Cost Text Generation with Differential Privacy"
title_zh: InvisibleInk：高实用低成本的差分隐私文本生成
authors: "Vishnu Vinod, Krishna Pillutla, Abhradeep Guha Thakurta"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=B4NT8TexNS"
tags: ["query:priv-sec"]
score: 10.0
evidence: 提出一种面向LLM和RAG的差分隐私文本生成框架
tldr: 为解决大语言模型在长文本生成中融入敏感信息且满足差分隐私的难题，本文提出InvisibleInk框架，创新地将LLM的token采样视为带隐私约束的指数机制，通过隔离并裁剪模型logits中的敏感部分来降低隐私预算消耗，同时优化采样过程保证文本质量，最终在检索增强生成等多种场景下实现了高实用性且严格隐私保护的长文本生成，为医学问答等领域的隐私敏感应用铺平了道路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 在LLM长文本生成中安全融入隐私信息是尚未解决的问题，尤其涉及RAG场景。
method: 将LLM的下一token分布采样视为指数机制，通过隔离裁剪敏感信息降低隐私成本，并改进采样提升质量。
result: 实现了严格差分隐私保障下的高质量长文本生成，适用于RAG等范式。
conclusion: 为需要外部敏感知识的生成任务提供了实用的隐私保护方案。
---

## Abstract
As major progress in LLM-based long-form text generation enables paradigms such as retrieval-augmented generation (RAG) and inference-time scaling, safely incorporating private information into the generation remains a critical open question. We present InvisibleInk, a highly scalable long-form text generation framework satisfying rigorous differential privacy guarantees with respect to the sensitive reference texts. It interprets sampling from the LLM's next-token-distribution as the exponential mechanism over the LLM logits with two innovations. First, we reduce the privacy cost by isolating and clipping only the sensitive information in the model logits (relative to the public logits). Second, we improve text quality by sampling without any privacy cost from a small superset of the top-$k$ private tokens. Empirical evaluations demonstrate a consistent $8\times$ (or more) reduction in computation cost over state-of-the-art baselines to generate long-form private text of the same utility across privacy levels. InvisibleInk is able to generate, for the first time, high-quality private long-form text at less than $4\text{-}8\times$ times the computation cost of non-private generation, paving the way for its practical use. We open-source a pip-installable Python package (invink) for InvisibleInk at https://github.com/cerai-iitm/invisibleink.

---

## 论文详细总结（自动生成）

# InvisibleInk：高实用低成本的差分隐私文本生成 论文总结

## 1. 论文的核心问题与整体含义
- **研究背景**：随着大语言模型（LLM）在长文本生成中的重大进展，检索增强生成（RAG）、推理时扩展（inference‑time scaling）等范式得以落地，但如何在生成过程中安全地融入私有信息仍是一个尚未解决的关键问题。
- **核心问题**：当生成模型需要引用外部敏感文本（如私有文档、用户数据）时，如何保证生成结果 **严格满足差分隐私**（differential privacy），同时维持文本的高实用性（utility）与可接受的计算成本。
- **整体含义**：提出一个可扩展的长文本生成框架 **InvisibleInk**，首次在差分隐私约束下实现高质量长文本生成，且计算代价仅为非隐私生成的 4‑8 倍，为医学问答、法律文书等隐私敏感场景提供了实用路径。

## 2. 方法论
- **核心思想**：将 LLM 的 **下一 token 分布采样** 重新解释为 **指数机制**（exponential mechanism）作用于模型 logits，并对敏感信息进行精细化隔离与扰动。
- **关键技术细节**：
  - **敏感‑公共 logits 解耦**：将模型输出 logits 拆分为 **公共部分**（来自非敏感上下文或预训练知识）和 **敏感部分**（由私有参考文本带来的贡献）。
  - **敏感 logits 裁剪**：仅对敏感部分的 logits 进行裁剪（clipping）并添加噪声，从而大幅降低隐私预算消耗，因为公共部分无需消耗隐私。
  - **低隐私成本的采样优化**：从私有 token 的 **top‑k 超集** 中直接采样，该采样过程不增加隐私成本，有效提升文本质量。
  - **整体流程**：
    1. 给定公有上下文和私有参考文本，计算出公共 logits 向量 ℓ_public。
    2. 利用私有文本计算敏感偏移 Δ，经裁剪后加噪，得到私有敏感 logits Δ̃。
    3. 合并 logits：ℓ = ℓ_public + Δ̃，构成满足差分隐私的最终分布。
    4. 从 top‑k 私有 token 超集中无隐私消耗地采样，生成下一个 token，逐 token 生成全文。
- **隐私保障**：严格遵循差分隐私定义，将全文本生成视为多次指数机制的组合，通过组合定理和隐私放大技术提供端到端隐私保证。

## 3. 实验设计
- **数据集与场景**：论文摘要及元数据未列出具体数据集名称，仅提及 “多种场景，尤其检索增强生成（RAG）”、“医学问答等领域的隐私敏感应用” 作为动机。实际接受论文中可能使用了问答、摘要或对话类基准。
- **Benchmark 与对比方法**：
  - 对比了 **当前最先进的差分隐私长文本生成基线**（state‑of‑the‑art baselines），但未在给出的信息中具体命名。
  - 评估指标包括 **文本实用性**（utility）与 **计算成本**。
- **实验结论概述**：在所有隐私等级下，InvisibleInk 生成等实用性文本所需的计算量 **相比最强基线一致减少 8 倍以上**；首次实现高质量差分隐私长文本生成，计算开销仅为非隐私生成的 4‑8 倍。

## 4. 资源与算力
- 在提供的 OpenReview 元数据及摘要中 **未明确说明** 使用的 GPU 型号、数量、训练时长或推理的具体算力。
- 若完整论文中提及，通常此类工作会报告推理延时的相对倍数或绝对延迟，但本次可获取的信息不足以给出确切算力数据。

## 5. 实验数量与充分性
- **实验组数**：基于有限摘要，仅知进行了多组 “实证评估”（empirical evaluations），覆盖不同隐私等级和与基线的比较，但 **具体实验表格、消融研究、不同数据集的组数均未提供**。
- **充分性与客观性**：
  - 声称 “consistent 8× reduction in computation cost” ，表明在不同设置下重复验证，呈现一致性，但无法确认是否包含统计显著性检验或误差棒。
  - 缺乏对实验细节的描述（如任务类型、私有/公有信息比例、文本长度等），在现有信息下无法完全评判充分性与公平性。
  - 开源了 Python 包 `invink`，有助于后续复现与独立评测。

## 6. 论文的主要结论与发现
- **主要结论**：
  - 通过将 token 采样视为指数机制并隔离敏感信息，可以 **大幅度降低差分隐私文本生成的计算成本**。
  - **InvisibleInk 首次实现** 在严格差分隐私保障下生成实用性高的长文本，使私有 RAG、推理时私有知识注入等场景成为现实。
  - 方法将计算开销压缩到不可忽略但可工程化的水平（< 4‑8 倍非隐私生成），为落地应用扫清主要障碍。
- **发现**：隐私成本可以通过不处理公共模型知识而集中于敏感偏移上来节省；基于 top‑k 的超集采样可在不额外消耗隐私的前提下提升解码质量。

## 7. 优点
- **方法论亮点**：
  - 巧妙地将指数机制与 LLM 生成对齐，理论清晰且符合差分隐私标准。
  - **“敏感‑公共 logits 解耦 + 仅裁剪敏感部分”** 的设计极为精巧，极大降低隐私预算损耗，是核心创新。
  - 在不增加隐私开销的情况下改进解码（top‑k 超集采样），兼顾理论与工程。
- **实验与实用性**：
  - 展现出 **显著的计算成本优势**（8 倍以上减少），并且首次做到与无隐私生成可比的开销。
  - 提供可直接安装的 Python 包，推动技术落地与学术复现。
  - 适用面广：覆盖 RAG、推理时扩展等多种当前前沿范式。

## 8. 不足与局限
- **实验覆盖不足**：限于提供的摘要，无法确认其在 **多领域、多语种、多模型** 上的泛化性；对比的基线方法、具体任务与数据集的缺失削弱了结论的可复现评判。
- **可能的偏差风险**：
  - 文本质量评价依赖自动指标，可能不足以完全体现 “实用性”，真实用户感知的隐私‑实用权衡尚不清楚。
  - 若私有信息占比极小或极分散，方法可能退化为普通扰动，优势会减弱。
- **应用限制**：
  - 仍需要 4‑8 倍的非隐私计算代价，在超大规模实时场景中可能仍存瓶颈。
  - 框架假设能够明确划分公有与私有部分，对于复杂混杂输入或训练时已记忆的敏感信息，划分边界可能模糊。
  - 差分隐私参数 ε 的选择会影响输出质量，文内未见针对 ε 的敏感度分析详情（需看全文）。

（完）
