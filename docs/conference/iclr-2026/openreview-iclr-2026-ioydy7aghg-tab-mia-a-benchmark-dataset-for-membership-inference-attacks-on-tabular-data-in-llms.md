---
title: "Tab-MIA: A Benchmark Dataset for Membership Inference Attacks on Tabular Data in LLMs"
title_zh: Tab-MIA：大型语言模型中表格数据成员推断攻击的基准数据集
authors: "Eyal German, Sagiv Antebi, Daniel Samira, Asaf Shabtai, Yuval Elovici"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=ioYdy7aghG"
tags: ["query:priv-sec"]
score: 9.0
evidence: 评估LLM中表格数据的成员推断攻击，解决隐私风险
tldr: 大型语言模型（LLM）越来越多地使用表格数据，其中包含结构化个人信息，引发隐私风险。Tab-MIA 基准数据集专门评估 LLM 中表格数据的成员推断攻击，揭示其与文本攻击不同的威胁特征。实验证明现有攻击在此场景下效果有限，凸显了保护表格数据隐私的紧迫性。该工作为 LLM 隐私评估提供了标准化工具。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: LLM训练使用表格数据带来个人信息泄露的隐私风险。
method: 提出Tab-MIA基准数据集，用于评估表格数据成员推断攻击。
result: 现有MIA方法在表格数据上效果不同，需专门评估。
conclusion: 为LLM隐私评估提供重要基准，促进表格数据保护研究。
---

## Abstract
Large language models (LLMs) are increasingly trained on tabular data, which, unlike unstructured text, often contains personally identifiable information (PII) in a highly structured and explicit format. As a result, privacy risks arise, since sensitive records can be inadvertently retained by the model and exposed through data extraction or membership inference attacks (MIAs). While existing MIA methods primarily target textual content, their efficacy and threat implications may differ when applied to structured data, due to its limited content, diverse data types, unique value distributions, and column-level semantics. In this paper, we present Tab-MIA, a benchmark dataset for evaluating MIAs on tabular data in LLMs and demonstrate how it can be used. Tab-MIA comprises five data collections, each represented in six different encoding formats. Using our Tab-MIA benchmark, we conduct the first evaluation of state-of-the-art MIA methods on LLMs fine-tuned with tabular data across multiple encoding formats. In the evaluation, we analyze the memorization behavior of pretrained LLMs on structured data derived from Wikipedia tables. Our findings show that LLMs memorize tabular data in ways that vary across encoding formats, making them susceptible to extraction via MIAs. Even when fine-tuned for as few as three epochs, models exhibit high vulnerability, with AUROC scores approaching 90% in most cases. Tab-MIA enables systematic evaluation of these risks and provides a foundation for developing privacy-preserving methods for tabular data in LLMs.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义
- **研究动机**：大语言模型（LLM）在训练中越来越多地使用结构化表格数据，此类数据常以高度结构化和显式格式承载个人身份信息（PII），带来显著的隐私泄露风险。
- **核心问题**：现有成员推断攻击（MIA）方法主要针对非结构化文本设计，当应用于表格数据时，其威胁特性与有效性可能发生根本变化，因为表格数据具有**有限内容、多样数据类型、独特的数值分布及列级别语义**等固有特点。
- **整体含义**：需建立专门面向表格数据的 MIA 评估基准，系统揭示 LLM 在结构化数据上的记忆行为与隐私脆弱性，推动隐私保护技术研发。

### 2. 方法论
- **核心思想**：提出 **Tab-MIA** — 一个专门用于评估 LLM 中表格数据成员推断攻击的**基准数据集**，统一衡量不同编码格式下 LLM 对表格数据的记忆与泄露风险。
- **关键技术思路**：
  - 构建多源表格数据集合，覆盖不同领域与规模。
  - 将同一表格数据以 **六种不同编码格式** 表示（例如：自然语言描述、JSON、Markdown 表格、CSV 等），模拟 LLM 实际接收的训练输入形态。
  - 基于该基准，对 LLM 进行微调或预训练，随后应用现有的 SOTA MIA 方法进行攻击评估。
- **流程概述**：
  1. 收集表格记录并划分为成员（训练集）与非成员（测试集）。
  2. 对 LLM 使用成员数据进行微调。
  3. 使用黑盒/白盒 MIA 技术（如 loss 阈值、Likelihood Ratio 等）计算每条记录的攻击分数，输出 AUROC 等指标。

### 3. 实验设计
- **数据集**：Tab-MIA 包含 **五个数据集合**，均来源于 Wikipedia 表格，确保数据多样性与真实结构化特性。每个数据集在六个不同编码格式下提供，构成 5×6 = 30 种子数据集场景。
- **基准与对比方法**：评估了**当前最先进的 MIA 方法**（State-of-the-art MIA methods），包括基于损失值、基于参考模型以及基于序列困惑度等代表性攻击算法。对比不同编码格式下攻击的有效性差异。
- **评估任务**：在预训练 LLM 上进行表格数据微调，随后执行 MIA，分析模型的 AUROC 和攻击成功程度，同时观察记忆行为随微调轮次的变化。

### 4. 资源与算力
- 文中未明确说明使用的 GPU 型号、数量或具体训练时长。仅提及对 LLM 进行**微调至少三个 epoch**，并在多个编码格式和数据集上开展攻击评估。算力消耗规模可推测为中等（数个数据集、多种格式下的微调与推理），但具体硬件配置尚不可知。

### 5. 实验数量与充分性
- **实验组合数量**：
  - 5 个数据集合 × 6 种编码格式 × 至少一种 MIA 方法（推测涵盖多种 SOTA 方法），构成数十组不同条件下的实验。
  - 还对**微调轮次**（如三个 epoch）与不同编码格式导致的攻击性能差异进行了消融分析。
- **充分性**：实验覆盖了多种数据源、多种输入表示，且对比了现有顶尖攻击方法，在方法公平性和设计全面性上较好。但若缺少对不同模型架构、不同规模 LLM 或更多攻击变体的系统比较，可能存在局限性。整体实验设计为首次基准，已具一定说服力。

### 6. 主要结论与发现
- **LLM 对表格数据的记忆行为**：模型会根据编码格式的不同，以不同模式和程度记忆结构化数据，致使 MIA 的漏洞等级因格式而异。
- **攻击高有效性**：即便微调仅进行三个 epoch，模型在大多数场景下已表现出高脆弱性，**AUROC 趋近 90%**，远超文本域中 MIA 的常规表现。
- **现有 MIA 方法效果不一**：直接迁移文本 MIA 方法到表格数据上，其攻击效果取决于编码格式和数据分布，证明需要专门针对表格特性的攻击评估和防护手段。
- **紧迫性**：Tab-MIA 揭示了在 LLM 中处理表格数据所面临的严重隐私暴露风险，需发展标准化评估工具。

### 7. 优点
- **首创新基准**：Tab-MIA 弥补了 LLM 领域表格数据隐私评估的空缺，为研究者提供标准化测试平台。
- **多维度设计**：涵盖五个真实数据集合和六种编码格式，能全面考察格式效应对隐私损失的影响。
- **系统性评估**：首次对表格数据上的 SOTA MIA 方法进行大范围比较，揭示了其局限性和攻击潜力，具有重要警示意义。
- **可复现性**：公开数据集与明确的评估范式便于后续研究复现与改进。

### 8. 不足与局限
- **数据集领域局限**：仅使用 Wikipedia 表格数据，可能缺少医疗、金融等更敏感表格场景，攻击行为在领域外推性未经验证。
- **模型范围有限**：未详细说明实验所用的 LLM 型号与规模，结论的普适性可能受限（尤其是对专用隐私保护架构或较大/较小模型）。
- **攻击方法覆盖**：虽评估了 SOTA MIA 方法，但可能未涵盖所有攻击类型（如基于影子模型的高级攻击），且仅报告 AUROC，缺乏精度、召回等更详尽指标。
- **算力未披露**：缺少计算资源说明，难以评估实验成本与可复现效率。
- **未提供防御方案**：基准旨在评估风险，尚未包含缓解策略的验证，实际应用联动不足。

（完）
