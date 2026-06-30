---
title: "Safety Pretraining: Toward the Next Generation of Safe AI"
title_zh: 安全预训练：迈向下一代安全AI
authors: "Pratyush Maini, Sachin Goyal, Dylan Sam, Alexander Robey, Yash Savani, Yiding Jiang, Andy Zou, Matt Fredrikson, Zachary Chase Lipton, J Zico Kolter"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=91H9CSvdwl"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出安全预训练框架，通过安全过滤、改写和原生拒绝来防止LLM生成有害内容
tldr: 大模型在实际部署中可能产生有害内容，事后对齐方法脆弱。本文提出数据驱动的安全预训练框架，包括安全分类过滤、不安全数据改写为安全叙述、以及合成原生拒绝数据集，将安全直接构建入模型。实验表明该方法从源头降低有害生成，减少了后续对齐的难度，提升了模型的基础安全性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 事后对齐方法难以彻底消除预训练中习得的不安全模式，需要从源头植入安全。
method: 四步安全预训练：安全过滤、不安全数据安全改写、原生拒绝合成、以及混合训练。
result: 安全预训练模型在多个安全基准上有害生成率显著降低，且保持语言能力。
conclusion: 安全预训练为构建本质安全的大模型提供了可行路径，比事后对齐更稳健。
---

## Abstract
As large language models (LLMs) are increasingly deployed in high-stakes settings, the risk of generating harmful or toxic content remains a central challenge. Post-hoc alignment methods are brittle: once unsafe patterns are learned during pretraining, they are hard to remove.
In this work, we present a data-centric pretraining framework that builds safety into the model from the start. Our framework consists of four key steps:
(i) Safety Filtering: building a safety classifier to classify webdata into safe and unsafe categories;
(ii) Safety Rephrasing: we recontextualize unsafe webdata into safer narratives;
(iii) Native Refusal: we synthetically generate pretraining datasets that actively teach models to refuse on unsafe content and the moral reasoning behind it, and
(iv) Harmfulness-Tag annotated pretraining: we flag unsafe content during pretraining using a special token, and use it to steer models away from unsafe generations at inference-time.
Our safety-pretrained models reduce attack success rates from 38.8% to 8.4% on standard LLM safety benchmarks with no performance degradation on general tasks.

---

## 论文详细总结（自动生成）

# 安全预训练：迈向下一代安全AI 详细总结

## 1. 论文的核心问题与整体含义
- **研究背景**：大语言模型（LLM）在高风险场景中迅速部署，生成有害内容（如仇恨言论、非法指导等）的风险成为核心挑战。
- **核心痛点**：当前主流的事后对齐方法（如RLHF）存在根本性脆弱性——模型在预训练阶段一旦习得不安全表示模式，后期很难彻底移除，属“打补丁”式补救，而非从源头解决。
- **整体含义**：作者提出“安全预训练”理念，主张在预训练的数据构造阶段就系统性植入安全性，让模型从语料源头学习拒绝对有害请求，实现“天生安全”而非“事后治理”。

## 2. 论文提出的方法论
**核心思想**：以数据为中心，通过四个关键步骤重塑预训练数据集，使模型在预训练期间即建立安全价值观。具体步骤如下：

- **(i) 安全过滤**  
  训练一个安全分类器，将大规模网页数据自动分类为“安全”与“不安全”两类。只保留安全数据进入预训练语料，从而剔除明确的极端有害内容。

- **(ii) 不安全数据的安全改写**  
  对于被判定为不安全的数据，并非简单删除，而是将其内容进行“再语境化”（recontextualize），重写成安全、教育性的叙述（例如将仇恨言论改写为对仇恨言论危害的讨论），保留语言多样性但消除直接有害性。

- **(iii) 原生拒绝合成**  
  生成专门的预训练数据集，主动教会模型拒绝执行危险指令。该数据集包含不安全请求以及模型应有的拒绝回答，并伴有**道德推理**过程，让模型学会为什么需要拒绝，而不仅仅是死板回避。

- **(iv) 有害标签注释预训练**  
  在预训练时，对不安全内容使用特殊标记（harmfulness tag）进行标注。在推理阶段，可利用该标记引导模型远离生成不安全方向（例如通过条件控制或提示，使模型回避触发标记对应的内容模式）。

> **公式或算法流程**（文字描述）：整个流程可概括为“预训练数据重构管道”——原始网页数据 → 安全分类 → 安全数据保留 / 不安全数据改写 / 合成拒绝样本 → 混合成最终训练集 → 标准自回归预训练，但数据本身已内嵌安全信号。

## 3. 实验设计
- **基准测试**：使用“标准LLM安全基准”（standard LLM safety benchmarks）评估有害生成水平，具体名称未在摘要中列出，但常见安全基准可能包含如RealToxicityPrompts、Anthropic harmlessness 数据集或攻击成功率的红队测试。
- **评估指标**：攻击成功率（ASR），即模型在接到恶意提示时生成有害响应的比例。
- **对比方法**：隐含与未做安全预训练、仅做事后对齐的模型对比。摘要中给出的攻击成功率从38.8%降至8.4%，即安全预训练模型相对基线降低了约78%的攻击成功率。
- **能力保留验证**：在通用任务上确认无性能下降，表明安全性提升未损害语言能力。

## 4. 资源与算力
- 提供的摘要及元数据**未明确提及**所使用GPU型号、数量、训练时长或能耗。论文全文可能包含此类信息，但基于现有文本无法推断。

## 5. 实验数量与充分性
- 摘要仅报道了核心安全基准上的结果，未展开说明消融研究或不同数据配方的对比实验。然而典型安全预训练工作通常包含：
  - 不同步骤（如是否启用改写、是否加入原生拒绝）的消融实验；
  - 多个下游安全任务评估；
  - 多个模型规模或类型的实验。
- 基于摘要，我们无法量化实验总数，但结果反映了关键指标的显著改善，初步证明方法有效性。

## 6. 主要结论与发现
- 安全预训练能够将模型的攻击成功率从38.8%大幅降低至8.4%，同时保持通用语言能力不退化。
- 说明从数据端植入安全比事后对齐更稳健，为构建“出厂即安全”的下一代LLM提供了可行路径。

## 7. 优点
- **方法论创新**：提出“安全改写”而非简单删除，保留数据多样性；创造“原生拒绝”数据集，主动教授拒绝与道德推理。
- **数据驱动**：避免了模型架构修改，兼容现有预训练范式，迁移成本低。
- **效果显著**：在关键安全指标上取得约4.6倍的相对改善，且无性能代价。
- **方向前瞻**：将安全从后置任务转移到预训练阶段，解决了安全对齐的根本矛盾。

## 8. 不足与局限
- **实验覆盖不透明**：摘要未给出基准具体名称、模型规模、预训练数据量，难以评估泛化性与公平性。
- **安全改写质量未评估**：改写后的数据是否引入偏见、事实扭曲或新的隐蔽风险未知。
- **特殊标记依赖**：推理时需使用特殊标签引导，可能引入额外的部署复杂度或控制脆弱性。
- **算力开销不明**：安全分类、改写、合成拒绝数据等都增加了预处理成本，效率影响未量化。
- **潜在偏差**：安全分类器自身可能带有标注偏差，导致过度过滤或遗漏某些类型的有害内容。

（完）
