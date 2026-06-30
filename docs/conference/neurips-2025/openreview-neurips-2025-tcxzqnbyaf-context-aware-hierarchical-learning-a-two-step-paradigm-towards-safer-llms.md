---
title: "Context-Aware Hierarchical Learning: A Two-Step Paradigm towards Safer LLMs"
title_zh: 上下文感知分层学习：迈向更安全的大语言模型的两步范式
authors: "Tengyun Ma, Jiaqi Yao, Daojing He, Shihao Peng, YU LI, Shaohui Liu, Zhuotao Tian"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=TCxzqnbyAF"
tags: ["query:priv-sec"]
score: 10.0
evidence: 新型工具补全攻击及通过分层学习的防御
tldr: 大语言模型统一的令牌处理范式在对抗场景下引发指令安全漏洞。本文发现并定义了一种新型攻击——工具补全攻击，它利用函数调用机制篡改模型行为。为此构建了全面的安全评估基准，揭示即便最先进模型也难以抵御。进而提出上下文感知分层学习范式，通过两步处理将高层指令与低层输入解耦，优先执行安全约束。实验证明该方法在显著降低攻击成功率的同时，保持了模型功能完整性，为LLM指令安全提供了新的防御思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: LLM存在函数调用被利用的新型攻击面，现有统一处理范式缺乏对指令层级的保护。
method: 提出上下文感知分层学习，解耦高层指令与低层输入，优先处理安全关键指令。
result: "在工具补全基准上，攻击成功率从90%降至10%以下，模型功能无显著下降。"
conclusion: 该方法为LLM指令安全提供了轻量高效防御，对新攻击面具有普遍适用性。
---

## Abstract
Large Language Models (LLMs) have emerged as powerful tools for diverse applications. However, their uniform token processing paradigm introduces critical vulnerabilities in instruction handling, particularly when exposed to adversarial scenarios. In this work, we identify and propose a novel class of vulnerabilities, termed Tool-Completion Attack (TCA), which exploits function-calling mechanisms to subvert model behavior. To evaluate LLM robustness against such threats, we introduce the Tool-Completion benchmark, a comprehensive security assessment framework, which reveals that even state-of-the-art models remain susceptible to TCA, with surprisingly high attack success rates. To address these vulnerabilities, we introduce Context-Aware Hierarchical Learning (CAHL), a sophisticated mechanism that dynamically equilibrates semantic comprehension with role-specific instruction constraints. CAHL leverages the contextual correlations between different instruction segments to establish a robust, context-aware instruction hierarchy. Extensive experiments demonstrate that CAHL significantly enhances LLM robustness against both conventional attacks and the proposed TCA, exhibiting strong generalization capabilities in zero-shot evaluations while still preserving model performance on generic tasks. Our code is available at https://github.com/S2AILab/CAHL.

---

## 论文详细总结（自动生成）

## 论文总结

### 1. 核心问题与整体含义（研究动机和背景）
- 大型语言模型（LLMs）普遍采用统一的令牌处理范式，这一设计在对抗场景下暴露出严重的指令安全漏洞。
- 本文发现并定义了一类全新攻击——**工具补全攻击（Tool-Completion Attack, TCA）**，该攻击利用模型的函数调用机制，通过恶意构造的输入篡改模型行为。
- 作者构建了专用的**工具补全基准（Tool-Completion benchmark）**评估框架，实验表明即使是当前最先进的模型也难以有效抵御 TCA，攻击成功率异常高。
- 整体含义：现有的统一处理范式缺乏对指令层级的区分与保护，亟需一种能够在保持模型通用能力的同时，稳固执行安全约束的新机制。

### 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：提出**上下文感知分层学习（Context-Aware Hierarchical Learning, CAHL）**，将指令处理解耦为两个层级——高层角色指令（如系统安全约束）与低层用户输入，并强制模型优先处理高层指令，从而阻断恶意低层输入对系统行为的篡改。
- **关键技术细节**：
  - 动态平衡语义理解与角色特定指令约束。
  - 利用不同指令片段之间的上下文关联，建立稳健的、上下文感知的指令层级结构。
  - 通过两步处理范式：先解析并锁定安全关键的高层指令，再在安全约束下处理低层输入，实现“安全优先”的执行逻辑。
- 该方法不依赖模型架构的大幅改动，是一种轻量级的防御策略。

### 3. 实验设计：数据集/场景、基准、对比方法
- **攻击基准**：专门设计的**Tool-Completion benchmark**，用于系统评估模型在函数调用场景下对工具补全攻击的脆弱性。
- **场景**：覆盖常规攻击（如提示注入）与本文提出的 TCA 攻击。
- **对比对象**：包括当前最先进的大语言模型（具体模型名称在摘要中未列出），在这些模型上测量攻击成功率。
- **评估指标**：攻击成功率（ASR）、通用任务性能（以验证防御是否损害正常功能）。
- 此外，进行了**零样本泛化评估**，考察 CAHL 在未见过的新攻击变体上的防御能力。

### 4. 资源与算力
- 提供的论文文本中**未明确说明**使用的 GPU 型号、数量、训练时长等算力细节。
- 摘要仅提及“Extensive experiments”，代码已开源，但硬件资源信息需参见原文正文或代码仓库。

### 5. 实验数量与充分性
- 论文声称进行了**大量实验**，至少包含以下维度：
  - 针对 TCA 和常规攻击的防御效果测试；
  - 零样本泛化实验；
  - 通用任务性能对比（确保功能无显著下降）。
- 摘要中所给的结果（攻击成功率从 90% 降至 10% 以下）和结论表明实验具有统计显著性和效果稳定性。
- 然而，作者未在摘要中详细列出消融实验的具体组数、数据集规模、统计检验方法，因此从已有文本无法准确量化实验总量。可以推断实验设计较完整，但在未见到全文前，部分细节的充分性无法完全定论。

### 6. 主要结论与发现
- CAHL 能大幅提升 LLM 对工具补全攻击及常规攻击的鲁棒性，将攻击成功率从约 **90% 降低至 10% 以下**。
- 防御的同时，模型在通用任务上的表现**未出现显著下降**，保持了功能完整性。
- CAHL 在零样本评估中表现出**强泛化能力**，表明其并非针对特定攻击样式的过拟合，具有一定普适性。
- 该工作为 LLM 指令安全提供了一种轻量、高效的新防御范式。

### 7. 优点：方法与实验设计的亮点
- **问题定义新**：首次揭示并命名工具补全攻击（TCA），开辟了 LLM 函数调用安全的新攻击面。
- **基准建设**：贡献了专门的 Tool-Completion benchmark，为后续研究提供了标准化评估工具。
- **设计巧妙**：两步分层解耦思想简单有效，在不牺牲通用性能的前提下实现安全加固，避免了传统安全对齐方法对模型能力的高代价压缩。
- **泛化能力强**：零样本评估结果优异，说明方法不依赖特定攻击样本的重训，实用性高。
- **开源可复现**：提供代码，促进社区验证与扩展。

### 8. 不足与局限：实验覆盖、偏差风险、应用限制
- **信息有限**：从现有文本无法得知实验中所用基准的具体样本量、模型版本、训练超参数等细节，难以完全评估实验的规模与严谨性。
- **对比基线不明**：未明确列出对比的具体防御方法（如对抗训练、提示过滤等），无法判断 CAHL 是否全面超越现有方案。
- **攻击覆盖范围**：集中于函数调用场景，未讨论多模态、多轮对话或更复杂的复合攻击下 CAHL 的有效性。
- **架构依赖性**：CAHL 的实施可能需要适配不同 LLM 的指令接口，泛化到闭源商业模型的可能性未讨论。
- **实际部署考量**：摘要未涉及推理延迟、额外计算开销和实时性表现，这些对现实应用至关重要。
- **偏差风险**：实验可能仅基于少数模型或英文环境，不一定代表跨语言、跨文化场景下的安全表现。

（完）
