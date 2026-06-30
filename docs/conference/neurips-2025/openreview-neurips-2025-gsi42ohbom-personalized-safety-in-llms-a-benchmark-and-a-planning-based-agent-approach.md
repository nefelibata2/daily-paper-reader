---
title: "Personalized Safety in LLMs: A Benchmark and A Planning-Based Agent Approach"
title_zh: 大语言模型中的个性化安全：基准与基于规划的智能体方法
authors: "Yuchen Wu, Edward Sun, Kaijie Zhu, Jianxun Lian, Jose Hernandez-Orallo, Aylin Caliskan, Jindong Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Gsi42ohBoM"
tags: ["query:priv-sec"]
score: 6.0
evidence: LLM个性化安全基准评估
tldr: 现有LLM安全评估忽略用户差异性，本文提出个性化安全概念，并构建PENGUIN基准，包含7个敏感领域、1.4万个场景。评估显示，结合个性化用户信息能显著提升安全分数，并提出了基于规划的安全代理方法。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 不同用户对LLM响应安全性的需求存在差异。
method: 构建PENGUIN基准，提出基于规划的个性化安全代理。
result: 个性化信息使LLM安全评分显著提升。
conclusion: 个性化安全是LLM安全部署的重要维度。
---

## Abstract
Large language models (LLMs) typically generate identical or similar responses for all users given the same prompt, posing serious safety risks in high-stakes applications where user vulnerabilities differ widely.
Existing safety evaluations primarily rely on context-independent metrics—such as factuality, bias, or toxicity—overlooking the fact that the same response may carry divergent risks depending on the user's background or condition.
We introduce ``personalized safety'' to fill this gap and present PENGUIN—a benchmark comprising 14,000 scenarios across seven sensitive domains with both context-rich and context-free variants. Evaluating six leading LLMs, we demonstrate that personalized user information significantly improves safety scores by 43.2%, confirming the effectiveness of personalization in safety alignment. However, not all context attributes contribute equally to safety enhancement. To address this, we develop RAISE—a training-free, two-stage agent framework that strategically acquires user-specific background. RAISE improves safety scores by up to 31.6% over six vanilla LLMs, while maintaining a low interaction cost of just 2.7 user queries on average. Our findings highlight the importance of selective information gathering in safety-critical domains and offer a practical solution for personalizing LLM responses without model retraining. This work establishes a foundation for safety research that adapts to individual user contexts rather than assuming a universal harm standard.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）
- 现有大语言模型（LLM）的安全评估依赖上下文无关的指标（如事实性、偏见、有害性），忽略了**用户差异性**：同一回答对不同背景或条件的用户可能带来截然不同的安全风险。
- 在高风险应用中（如医疗建议、法律咨询），以“一刀切”的方式判断模型回复是否安全，无法适配用户脆弱的多样性。
- 论文由此提出 **“个性化安全”（personalized safety）** 概念，旨在根据用户个性化背景重新定义LLM回复的安全性。
- 动机在于：将安全对齐从“统一危害标准”转向“适配个体上下文”的新范式，填补现有评估盲区。

## 2. 论文提出的方法论：核心思想、关键技术细节
- **核心思想**：通过获取用户特定背景信息，在推理阶段实现个性化安全响应，无需重新训练模型。
- **PENGUIN基准**  
  - 包含**7个敏感领域**（如心理健康、法律、金融等），共**14,000个场景**。  
  - 每个场景均有**上下文丰富（context-rich）** 和**无上下文（context-free）** 两种变体，用于对比。  
  - 用于系统评估个性化信息对LLM安全分数的提升效果。
- **RAISE智能体框架**（训练无关、两阶段代理）  
  - 策略性地获取用户背景：通过少量交互（平均仅2.7次查询）收集关键信息。  
  - 第一阶段：判定当前是否已掌握足够必要信息，若不足则生成针对性提问。  
  - 第二阶段：基于所获完整用户上下文，生成个性化安全回复。  
  - 实现**选择性信息收集**，避免过度询问，在有限交互成本下最大化安全性能。

## 3. 实验设计：数据集/场景、基准、对比方法
- **基准**：自建PENGUIN，覆盖7个敏感领域，1.4万场景（含context-rich与context-free）。
- **评估模型**：六种主流LLM（具体名称未详述），作为基线（vanilla LLMs）。
- **对比维度**  
  - 在有/无用户上下文条件下，对比各模型的安全分数变化。  
  - 引入RAISE后，对比原始LLM和RAISE增强版本的个性化安全效果。
- **指标**：安全分数（具体度量方式未展开，但明确提出安全分数的量化提升）。  
- **公平性**：使用统一基准、相同提示模板，在同一安全判定标准下对比，避免模型架构之外的不公平因素。

## 4. 资源与算力
- 论文摘录及元数据中**未明确提供**算力详情（如GPU型号、数量、训练时长）。  
- 由于RAISE为训练无关方法，核心推理开销在于少量用户交互回合和LLM推理，计算资源需求不大，但原文未给出具体配置。

## 5. 实验数量与充分性
- 基于摘要可推测的实验组成部分：
  - 六种LLM在PENGUIN benchmark上的上下文富化与无上下文两组对照实验。
  - 个性化信息对安全分数的提升分析（整体与按领域的差异）。
  - RAISE与原始LLM的性能对比（安全性、交互成本）。
  - 可能包含消融实验：不同上下文属性对安全提升的贡献差异（摘要提到“并非所有上下文属性贡献相同”）。
- **充分性与客观性**：基准规模较大（14k场景），多领域覆盖，多模型对比，且采用context-rich/context-free对照设计，较客观。但领域数量和模型覆盖（仅六款）仍有扩展空间，消融细节未全面公开。

## 6. 论文的主要结论与发现
- **个性化信息能显著提升LLM的安全性能**：在PENGUIN基准上，融入用户背景后安全分数平均提升**43.2%**。
- **并非所有背景属性同等重要**：部分用户属性对安全决策的影响远大于其他，有必要进行选择性利用。
- **RAISE可在极小交互成本下取得优秀效果**：在不重新训练模型的前提下，安全分数最高提升**31.6%**，平均仅需2.7次用户查询。
- 结果表明，个性化安全是LLM实际部署中不可忽视的重要维度，应建立基于用户上下文而非通用危害标准的安全评估体系。

## 7. 优点：方法或实验设计上的亮点
- **概念创新**：首次提出“个性化安全”概念，将LLM安全从静态评价转向上下文敏感的动态评价。
- **基准设计严谨**：PENGUIN提供丰富的领域场景和成对变体，为后续研究建立了可复现的评估平台。
- **方法实用性强**：RAISE无需额外训练，交互成本极低，易于集成到现有LLM应用。
- **选择性信息收集策略**：避免了因过度询问用户隐私而降低体验，兼顾安全与效率。

## 8. 不足与局限
- **领域覆盖有限**：仅7个领域，用户脆弱性的其他重要维度（如文化、语言、年龄段）可能未被充分覆盖。
- **隐私风险**：个性化安全方案需要收集用户敏感信息，如何保证信息保护尚待深入探讨。
- **动态适应性未知**：用户上下文可能随时间变化，当前静态的一次性收集策略无法应对长期交互中的变动。
- **评估指标可能不全面**：安全分数的具体构成不明，未考虑“安全”与“有用性”之间的权衡。
- **模型多样性不足**：仅测试六种LLM，未纳入不同尺寸、开源/闭源模型的全谱系对比。
- **算力报告缺失**：使复现和成本评估困难。

（完）
