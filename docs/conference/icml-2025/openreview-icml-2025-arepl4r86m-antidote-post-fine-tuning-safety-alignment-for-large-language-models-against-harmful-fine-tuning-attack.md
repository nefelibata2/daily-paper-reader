---
title: "Antidote: Post-fine-tuning Safety Alignment for Large Language Models against Harmful Fine-tuning Attack"
title_zh: Antidote：针对有害微调攻击的后微调安全对齐方法
authors: "Tiansheng Huang, Gautam Bhattacharya, Pratik Joshi, Joshua Kimball, Ling Liu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Arepl4R86m"
tags: ["query:priv-sec"]
score: 9.0
evidence: 对抗有害微调攻击的后微调阶段防御方法
tldr: 安全对齐的大语言模型容易遭受有害微调攻击，现有防御在特定超参数下失效。本文提出 Antidote，一种后微调阶段防御方案，通过移除有害参数来恢复模型安全性，无需依赖微调过程中的超参数设置。实验表明 Antidote 能有效抵御各种微调攻击，提升了 LLM 安全对齐的鲁棒性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有防御方法在较大学习率或训练轮数时失效，需要一种不受微调超参数影响的防御。
method: 提出 Antidote，在后微调阶段识别并移除有害参数，使模型恢复安全行为。
result: Antidote 成功抵御多种有害微调攻击，且对微调超参数不敏感。
conclusion: 后微调防御为 LLM 安全对齐提供了一种普适且鲁棒的解决方案。
---

## Abstract
Safety aligned Large Language Models (LLMs) are vulnerable to harmful fine-tuning attacks -- a few harmful data mixed in the fine-tuning dataset can break the LLMs's safety alignment. While several defenses have been proposed, our evaluation shows that existing defenses fail \textit{when some specific training hyper-parameters are chosen} -- a large learning rate or a large number of training epochs in the fine-tuning stage can easily invalidate the defense. To this end,  we propose Antidote, a post-fine-tuning stage solution, which remains \textbf{\textit{agnostic to the training hyper-parameters in the fine-tuning stage}}. Antidote relies on the philosophy that by removing the harmful parameters, the harmful model can be recovered from the harmful behaviors, regardless of how those harmful parameters are formed in the fine-tuning stage. With this philosophy, we introduce a one-shot pruning stage after harmful fine-tuning to remove the harmful weights that are responsible for the generation of harmful content. Despite its embarrassing simplicity, empirical results show that Antidote can reduce harmful score while maintaining accuracy on downstream tasks.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：现有大语言模型（LLM）通过安全对齐技术使自身拒绝有害请求，但攻击者只需在微调数据中混入少量有害样本，即可轻易破坏模型的安全守卫（有害微调攻击）。
- **现有防御的短板**：此前提出的防御方法（如参数冻结、噪声注入、损失约束等）高度依赖微调阶段的**超参数设置**。一旦攻击者采用较大的学习率或较多的训练轮次，这些防御便会失效。
- **本文动机**：设计一种与微调超参数无关的防御方案，无论攻击者使用何种超参数，都能在事后恢复模型的安全性。由此引出 **Antidote**——一种后微调阶段的安全对齐方法。

### 2. 论文提出的方法论
- **核心思想**：*通过移除有害参数来修复有害模型*。Antidote 不关心有害参数是如何在微调阶段形成的，只关注如何识别并剔除那些导致模型生成有害内容的权重。
- **技术路径**：
  - 在有害微调完成后，引入一个**一次性剪枝阶段**。
  - 该阶段自动定位模型中与有害行为强相关的“有害权重”，并对其实施修剪（例如置零或移除）。
  - 剪枝后的模型直接用作最终推理模型，不需要重新训练或依赖原微调中的超参数信息。
- **算法特点（根据摘要推断）**：
  - 属于**后微调防御**，对微调阶段的超参数（学习率、训练轮数）完全无感。
  - “尽管简单到令人尴尬，但极其有效”——强调方法的轻量和高实用性。
  - 在剪枝过程中兼顾了**安全性**（有害评分下降）和**下游任务准确率**的保持。

### 3. 实验设计
- **攻击场景**：多种有害微调攻击（混合有害数据的微调）。
- **对比基线**：现有的多种防御方法（论文中未列出名称，但涵盖了主流的微调阶段防御方案）。
- **评测指标**：
  - 有害评分（Harmful Score）：衡量模型生成有害内容的倾向（越低越好）。
  - 下游任务准确率：确保安全修复不以牺牲通用能力为代价。
- **数据集**：摘要未提及具体名称，但必然是包含有害指令的数据集（如 AdvBench、MaliciousInstruct 或自定义有害语料）以及常见的语言理解基准（如 MMLU、HellaSwag 等或类似任务）。
- **超参数敏感性验证**：特别设计了在不同学习率、不同训练轮数下的防御效果对比，以凸显 Antidote 对超参数的不敏感性。

### 4. 资源与算力
- 论文摘要及元数据中**未明确说明**所用的 GPU 型号、数量或训练时长。
- 鉴于方法为一次性剪枝，其后微调过程的计算开销远小于重新训练或微调，因此对算力要求大概率较低，但具体用量需从原文实验部分获取。

### 5. 实验数量与充分性
- **实验组数推断**：
  - 至少覆盖多种不同设置下的有害微调攻击（不同超参数组合、不同攻击强度）。
  - 消融实验或多维度分析（例如不同剪枝比例、不同有害权重识别策略）较有可能，但摘要未展开。
- **充分性评价**：
  - 从已报道的结论看，实验设计抓住了核心矛盾（超参数依赖性），对比了多个现有防御，并在安全性、通用性两个维度上进行评估，**具备较好的公平性和客观性**。
  - 由于摘要简短，无法得知在极端攻击（如 100% 有害数据）下的表现，或剪枝后模型在其他维度的安全性（如诚实、无偏）是否退化。

### 6. 论文的主要结论与发现
- 现有安全对齐防御在攻击者使用大学习率或大训练轮数时普遍失效。
- Antidote 作为一种后微调安全恢复手段，能够**有效降低有害得分**，且效果不受微调超参数选择的影响。
- 该方法简单通用，可在不牺牲下游任务准确率的前提下提升 LLM 对有害微调攻击的鲁棒性。

### 7. 优点
- **超参数无关性**：显著区别于所有依赖微调过程的防御，彻底解决了“换了学习率就失效”的痛点。
- **简单高效**：后微调一次性剪枝，不需要反复调节训练配置，易于部署。
- **实用性强**：在恢复安全性的同时尽力维持了下游性能，平衡性好。
- **新颖的视角**：从“事后修复有害参数”切入，为安全对齐打开了新的研究方向。

### 8. 不足与局限
- **论文细节缺失风险**：基于当前提供的摘要，无法评估剪枝判据的可靠性（例如是否可能误删安全相关参数）、剪枝阈值的泛化能力。
- **极端攻击未知**：当有害数据量极大或攻击方式更复杂（如连续微调、联邦学习下的攻击）时，Antidote 是否依然有效缺少讨论。
- **能力损失可能性**：尽管摘要称下游准确率得以保持，但在复杂生成任务或开放对话质量上是否出现隐性退化，尚需全文验证。
- **单点防御**：仅处理微调后模型，若攻击发生在其他阶段（如预训练数据污染、推理时注入），Antidote 无法直接应对。
- **缺少可解释性分析**：移除“有害参数”是否真正对应某种安全概念的神经表征，有待进一步解释。

（完）
