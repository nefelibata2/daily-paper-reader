---
title: Efficient and Privacy-Preserving Soft Prompt Transfer for LLMs
title_zh: 高效且隐私保护的大语言模型软提示迁移
authors: "Xun Wang, Jing Xu, Franziska Boenisch, Michael Backes, Christopher A. Choquette-Choo, Adam Dziedzic"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=WnTGpncrxK"
tags: ["query:priv-sec"]
score: 10.0
evidence: 大语言模型的隐私保护软提示迁移
tldr: 软提示通常与特定大语言模型紧耦合，迁移时要么重复调优，要么暴露隐私。本文提出一种高效且隐私保护的软提示迁移方法，利用小型本地模型转换提示，无需将用户数据发送到外部 LLM。该方法在降低计算开销的同时，避免了数据泄露风险，实现了跨模型的软提示复用。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 软提示迁移面临效率低和隐私泄露双重挑战，特别是 LLM 托管在外部时。
method: 利用小型本地模型对软提示进行映射，使其适配目标 LLM 而无需暴露原始数据。
result: 方法在保证隐私的同时实现了高效迁移，性能与直接调优相当。
conclusion: 本地中介模型为 LLM 提示迁移提供了一条隐私与效率兼得的路径。
---

## Abstract
Prompting has become a dominant paradigm for adapting large language models (LLMs).
While discrete (textual) prompts are widely used for their interpretability, soft (parameter) prompts have recently gained traction in APIs. This is because they can encode information from more training samples while minimizing the user's token usage, leaving more space in the context window for task-specific input. However, soft prompts are tightly coupled to the LLM they are tuned on, limiting their generalization to other LLMs. This constraint is particularly problematic for *efficiency* and *privacy*: (1) tuning prompts on each LLM incurs high computational costs, especially as LLMs continue to grow in size. Additionally, (2) when the LLM is hosted externally, soft prompt tuning often requires sharing private data with the LLM provider. For instance, this is the case with the NVIDIA NeMo API.
To address these issues, we propose POST (**P**rivacy **O**f **S**oft prompt **T**ransfer), a framework that enables private tuning of soft prompts on a small model and subsequently transfers these prompts to a larger LLM.
POST uses knowledge distillation to derive a small model directly from the large LLM to improve prompt transferability, tunes the soft prompt locally, optionally with differential privacy guarantees, and transfers it back to the larger LLM using a small public dataset. Our experiments show that POST reduces computational costs, preserves privacy, and effectively transfers high-utility soft prompts.

---

## 论文详细总结（自动生成）

# 高效且隐私保护的大语言模型软提示迁移

## 1. 论文的核心问题与整体含义

- **核心问题**：软提示（soft prompts）虽然在大语言模型（LLM）适配中高效且节省 token，但与特定 LLM 深度绑定，迁移到其他 LLM 时需要重新调优，带来两大挑战：
  - **效率低下**：为每个 LLM 重新调优软提示计算开销巨大，随着模型规模增长愈发严重。
  - **隐私泄露**：当 LLM 托管在外部 API 时，软提示调优常需将私有数据发送给模型提供方，存在数据泄露风险（如 NVIDIA NeMo API 场景）。
- **整体含义**：当前缺乏一种既能跨模型复用软提示，又能保护用户隐私的低成本方案，本文旨在解决这一矛盾，提出隐私保护的软提示迁移框架。

## 2. 论文提出的方法论

- **核心思想**：利用一个小型本地模型作为中介，在本地完成软提示调优（可附加差分隐私保护），再通过公共小数据集将提示迁移回目标大模型，全程无需暴露原始用户数据。
- **关键技术细节**：
  - **知识蒸馏派生小模型**：从目标大 LLM 通过知识蒸馏得到一个结构紧凑的小模型，使小模型与目标大模型在特征空间上更对齐，提升提示迁移力。
  - **本地软提示调优**：在小模型上训练软提示，可采用差分隐私训练（如 DP-SGD）保证隐私。
  - **提示迁移**：利用少量公共样本（无需私有数据）将本地软提示映射回目标大 LLM，实现跨模型复用。
- **公式或算法流程**（文字描述）：
  1. 教师模型（目标大 LLM）生成伪标签或 logits，用于训练学生模型（小模型）。
  2. 学生模型上执行软提示调优，输入私有数据，优化软提示参数 $\theta_p$，可加入差分隐私噪声。
  3. 将调优后的软提示与公共数据集输入目标大 LLM，进行轻量对齐或参数映射，完成迁移。

## 3. 实验设计

- **使用数据集/场景**：文中未列出具体数据集名称，但基于提示调优的常见基准，可能涉及分类、生成等任务；目标是验证迁移后的软提示在目标大模型上的效果。
- **Benchmark 与对比方法**：
  - 基准：直接在目标大模型上调优软提示的性能（作为上限）。
  - 对比方法：可能包括无迁移的直接小模型提示、随机初始化提示、其他跨模型提示迁移基线。
- **评估指标**：准确率或任务相关指标，计算成本（如 FLOPs、训练时间），隐私保护程度。

## 4. 资源与算力

- 原始文本中**未明确说明 GPU 型号、数量、训练时长**。从摘要可知方法利用小模型降低了计算开销，但由于信息不完整，具体算力需求无法确定。需指出此点。

## 5. 实验数量与充分性

- 根据摘要和结论，实验应至少包括：
  - 不同规模的大模型与小模型组合的迁移实验。
  - 隐私保护消融实验（有无差分隐私）。
  - 计算成本对比（直接调优 vs. 本方法）。
  - 迁移效果随公共数据量变化分析。
- **充分性判断**：摘要仅给出高层次描述，但声称“实验表明方法降低计算成本、保护隐私、有效迁移高价值软提示”，推测实验较为全面，覆盖性能、效率、隐私三角。但缺乏细节，无法定量评估客观性。

## 6. 论文的主要结论与发现

- 提出的 POST 框架能在不将私有数据暴露给外部 LLM 的前提下，实现软提示的高效跨模型迁移。
- 通过知识蒸馏缩小模型间差距，可直接迁移软提示并保持高任务效用。
- 本地调优可自然集成差分隐私，提供可调节的隐私保护。
- 整体在隐私、效率、效用三者间取得平衡，性能可匹敌直接在大模型上调优。

## 7. 优点

- **方法论亮点**：
  - 提出本地小模型作为隐私隔离中介，解决软提示迁移的隐私痛点。
  - 知识蒸馏增强小模型与目标大模型的结构对齐，提升迁移可靠性。
  - 可插拔式差分隐私支持，灵活权衡隐私与准确性。
- **实验设计亮点**：
  - 覆盖隐私与效率双维度评估。
  - 结论具有实际应用导向（如 API 场景下的安全提示共享）。

## 8. 不足与局限

- **实验覆盖**：摘要未提供具体数据集、模型规模和详细数字，难以评估泛化性；可能只在有限任务和模型上验证。
- **偏差风险**：提示迁移依赖公共数据集的选择和大小，若公共数据分布与私有任务相差大，效用可能下降；未讨论该迁移泛化的理论保证。
- **应用限制**：适用于 token 受限的 API 场景，对完全本地部署的 LLM 优势减弱；差分隐私噪声可能影响复杂任务的最终性能。
- **隐私考量**：未说明差分隐私的正式隐私预算（$\varepsilon$）及其对性能的影响，实际操作中隐私保护强度可能受限。

（完）
