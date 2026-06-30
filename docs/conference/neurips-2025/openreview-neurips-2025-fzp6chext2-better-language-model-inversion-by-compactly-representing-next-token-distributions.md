---
title: Better Language Model Inversion by Compactly Representing Next-Token Distributions
title_zh: 通过紧凑表示下一个标记分布来改进语言模型反演
authors: "Murtaza Nazir, Matthew Finlayson, John Xavier Morris, Xiang Ren, Swabha Swayamdipta"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=FZp6cheXt2"
tags: ["query:priv-sec"]
score: 9.0
evidence: 从大模型API输出恢复隐藏提示的隐私攻击
tldr: 语言模型反演可通过输出恢复隐藏提示，威胁隐私。现有方法受限于单步信息，无法恢复较长提示。PILS发现模型输出的概率向量的低维特性，通过线性映射无损压缩多步中间分布，从而联合推理更长序列。实验表明PILS显著提升了反演长度和准确率，甚至能恢复完整的系统消息。该工作警示了LLM部署中的信息泄露风险。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有提示反演仅利用单步输出，难以恢复较长的隐藏提示。
method: PILS利用输出logprob低维特性，线性压缩多步概率分布，实现联合反演。
result: 在多个LLM上成功恢复远超此前方法的长系统消息，反演准确率大幅提升。
conclusion: PILS揭示了LLM API存在严重的隐藏提示泄露风险，需加强防护。
---

## Abstract
Language model inversion seeks to recover hidden prompts using only language model outputs. This capability has implications for security and accountability in language model deployments, such as leaking private information from an API-protected language model’s system message. We propose a new method – prompt inversion from logprob sequences (PILS) – that recovers hidden prompts by gleaning clues from the model’s next-token probabilities over the course of multiple generation steps. Our method is enabled by a key insight: The vector-valued outputs of a language model occupy a low-dimensional subspace. This enables us to losslessly compress the full next-token probability distribution over multiple generation steps using a linear map, allowing more output information to be used for inversion. Our approach yields massive gains over previous state-of-the-art methods for recovering hidden prompts, achieving 2–3.5 times higher exact recovery rates across test sets, in one case increasing the recovery rate from 17% to 60%. Our method also exhibits surprisingly good generalization behavior; for instance, an inverter trained on 16 generations steps gets 5–27% higher prompt recovery when we increase the number of steps to 32 at test time. Furthermore, we demonstrate strong performance of our method on the more challenging task of recovering hidden system messages. We also analyze the role of verbatim repetition in prompt recovery and propose a new method for cross-family model transfer for logit-based inverters. Our findings suggest that next-token probabilities are a considerably more vulnerable attack surface for inversion attacks than previously known.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：语言模型反演（Language Model Inversion）攻击，即仅通过观察语言模型（如 API 返回的 `logprobs`）的输出，逆向恢复模型内部隐藏的提示（prompt），尤其是受 API 保护的系统消息（system message）。
- **研究动机**：
  - 现代大语言模型（LLM）部署常通过 API 暴露 token 级别的概率（`logprobs`），这为攻击者提供了表面。
  - 现有反演方法仅利用**单步生成**的输出分布，对较长提示（如完整的系统消息）恢复能力极弱，因为单步信息有限。
  - 论文意在揭示：多步输出的概率分布比已知的更脆弱，可以通过紧凑表示实现高效的联合反演，从而大幅提升攻击效果，警示 LLM 部署的隐私风险。

## 2. 论文提出的方法论
- **核心思想**：**从 logprob 序列中反演出提示（Prompt Inversion from Logprob Sequences, PILS）**。
  - **关键洞察**：语言模型在每一步输出的下一个 token 概率向量（`next-token distribution`）存在于一个**低维子空间**中。
  - **技术路线**：利用这一低维特性，通过一个**线性映射**将多步生成的完整概率分布无损压缩成紧凑表示，从而在一次反演中联合利用更多步的输出信息，突破长度限制。
- **算法流程（文字描述）**：
  1. 运行目标模型生成若干步（如 16 或 32 步），收集每一步的 `next-token distribution`（通常为词表大小的概率向量）。
  2. 对这些高维向量序列应用预训练的线性压缩矩阵，将其投影到低维空间，得到紧凑的特征序列。
  3. 将压缩后的序列输入一个反演模型（如 Transformer 解码器或优化器），使其联合学习多步状态与隐藏提示之间的映射。
  4. 反演模型输出恢复的 prompt token 序列。
- **区别于已有方法**：以往方法仅使用单步分布，PILS 通过“压缩-联合”策略，将更多步的分布无损融合，极大增加了可用于反演的信息量。

## 3. 实验设计
- **数据集 / 场景**：
  - 多个标准提示反演基准测试集（具体名称未在摘要和元数据中列出，但提到“test sets”）。
  - 更具挑战性的**隐藏系统消息恢复**场景，模拟 API 泄露真实系统指令。
- **对比方法**：与当时最先进（SOTA）的基于 logit/logprob 的反演方法进行比较（元数据中提及“previous state-of-the-art methods”）。
- **评估指标**：**完全匹配恢复率（exact recovery rate）**，部分结果提到提升倍数和百分比。

## 4. 资源与算力
- 论文提供的文本中**未明确说明**使用的 GPU 型号、数量或训练时长。摘要和元数据中均未涉及算力细节，无法给出具体数值。

## 5. 实验数量与充分性
- 从摘要和元数据推断，至少包含以下几组实验：
  - 在不同 LLM 上的性能测试（multiple LLMs）。
  - 多组测试集上的完全恢复率对比（recovery rates across test sets）。
  - 泛化性实验：在 16 步上训练，在 32 步上测试，观察恢复率提升（5–27%）。
  - 隐藏系统消息恢复的专项任务。
  - 跨模型迁移实验（cross-family model transfer）。
  - 可能包含消融实验（如压缩维度影响、步数影响等），但细节未在提供文本中列出。
- **充分性评价**：从结果描述看，实验覆盖了性能对比、可扩展性、迁移性、真实攻击场景，设计较为充分和客观；但受限于仅有摘要，无法完全确认实验细节是否公平（如是否对对比方法做了同等调参）。

## 6. 论文的主要结论与发现
- PILS 在隐藏提示恢复上达到远超以往的性能，完全匹配恢复率提升 **2–3.5 倍**（例如从 17% 提升到 60%）。
- 通过紧凑表示，多步概率序列可以联合利用，成功恢复**比以往方法更长的提示**，甚至完整恢复系统消息。
- 方法展现出惊人的泛化能力：在训练步数（如 16）和测试步数（如 32）不一致时，仍能取得更好结果。
- 还分析了提示中逐字重复对恢复的作用，并提出一种跨模型家族的 logit 逆变器迁移方法。
- **最终警示**：`next-token probabilities` 是比先前认知**更脆弱**的攻击面，LLM API 存在严重的隐藏提示泄露风险。

## 7. 优点：方法或实验设计上的亮点
- **无损压缩长序列分布**：利用低维子空间特性，不丢失信息，使反演可用知识显著增多。
- **允许测试时步长扩展**：训练和推理可解耦，表明模型学到的是通用的压缩表示，而非死记步数。
- **攻克更具现实威胁的任务**：恢复系统消息比普通 prompt 恢复更有实际安全意义。
- **跨模型迁移**：提出的迁移方法降低了攻击者训练反演模型的成本。
- **量化证据充分**：用完全匹配率、提升倍数等客观指标，对比效果突出。

## 8. 不足与局限
- **实验细节不透明**：受限于仅有摘要，未能评估具体数据集大小、模型的多样性、有无防御设置、对比方法是否完全对齐等。
- **攻击假设较强**：需要目标模型 API 返回完整的 `logprobs` 向量（或经压缩处理的中间值）；若 API 仅返回 top-k 概率或屏蔽概率，PILS 可能失效。
- **计算偏差风险**：模型和数据集选取可能存在偏向，但摘要未提及。泛化到现实复杂场景（如多轮对话、噪声输出）的能力待验证。
- **应用限制**：文章定位于揭示风险，并非提供防御措施；若防御方案（如差分隐私）被施加，效果可能下降。
- **未讨论防御**：全文似乎聚焦攻击，对缓解策略的讨论可能较少。

（完）
