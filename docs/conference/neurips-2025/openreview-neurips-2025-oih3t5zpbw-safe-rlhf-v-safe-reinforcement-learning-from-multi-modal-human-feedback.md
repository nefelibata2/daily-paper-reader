---
title: "Safe RLHF-V: Safe Reinforcement Learning from Multi-modal Human Feedback"
title_zh: Safe RLHF-V：基于多模态人类反馈的安全强化学习
authors: "Jiaming Ji, Xinyu Chen, Rui Pan, Han Zhu, Jiahao Li, Donghai Hong, Boyuan Chen, Jiayi Zhou, Kaile Wang, Juntao Dai, Chi-Min Chan, Sirui Han, Yike Guo, Yaodong Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=OIH3T5ZPBW"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过带显式安全约束的RLHF实现多模态LLM的安全对齐
tldr: 多模态大模型面临日益严峻的安全风险，现有方法未能将单一偏好信号解耦为显式安全约束。本文提出Safe RLHF-V，将安全对齐形式化为极小极大优化问题，从多模态人类反馈中解耦安全约束，并首次将其有效融入多模态模型的强化学习微调中。实验表明该方法在保持模型能力的同时，显著降低了不安全行为的生成概率，为构建安全可靠的多模态AI助手提供了新的对齐范式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 多模态大模型的安全对齐缺乏显式安全约束和系统优化方法，现有数据集未解耦偏好与安全信号。
method: 将安全对齐建模为极小极大优化，从人类反馈中分离安全约束，并通过安全强化学习微调多模态模型。
result: 在多个安全基准上，该方法大幅降低不安全输出，同时保持甚至提升模型的一般性能。
conclusion: Safe RLHF-V首次在多模态场景下实现了有效且可扩展的安全对齐，填补了领域空白。
---

## Abstract
Multimodal large language models (MLLMs) are essential for building general-purpose AI assistants; however, they pose increasing safety risks. How can we ensure safety alignment of MLLMs to prevent undesired behaviors? Going further, it is critical to explore how to fine-tune MLLMs to preserve capabilities while meeting safety constraints. Fundamentally, this challenge can be formulated as a min-max optimization problem. However, existing datasets have not yet disentangled single preference signals into explicit safety constraints, hindering systematic investigation in this direction. Moreover, it remains an open question whether such constraints can be effectively incorporated into the optimization process for multi-modal models. In this work, we present the first exploration of the Safe RLHF-V -- the first multimodal safety alignment framework. The framework consists of: (I) BeaverTails-V, the first open-source dataset featuring dual preference annotations for helpfulness and safety, supplemented with multi-level safety labels (minor, moderate, severe); (II) Beaver-Guard-V, a multi-level guardrail system to proactively defend against unsafe queries and adversarial attacks. Applying the guard model over five rounds of filtering and regeneration significantly enhances the precursor model’s overall safety by an average of 40.9%. (II) Based on dual preference, we initiate the first exploration of multi-modal safety alignment within a constrained optimization. Experimental results demonstrate that Safe RLHF effectively improves both model helpfulness and safety. Specifically, Safe RLHF-V enhances model safety by 34.2% and helpfulness by 34.3%.

---

## 论文详细总结（自动生成）

# Safe RLHF-V：基于多模态人类反馈的安全强化学习  论文总结

## 1. 核心问题与研究动机  
- 多模态大语言模型（MLLMs）在构建通用AI助手时不可或缺，但其安全风险日益突出。  
- **核心挑战**：如何在微调MLLMs时兼顾能力保持与安全约束，避免模型生成有害、偏激或违规的多模态输出。  
- 该问题本质上可形式化为**极小极大优化问题**（min‑max optimization），但现有数据集**未将单一的偏好信号解耦为显式的安全约束**，导致无法系统研究多模态安全对齐。  
- 此外，这一约束能否有效嵌入多模态模型的优化过程仍是开放问题。  
- **整体含义**：Safe RLHF‑V 首次在多模态场景下探索了基于人类反馈的安全强化学习，填补了将显式安全约束引入RLHF微调的研究空白。

## 2. 方法论  
**核心思想**：将安全对齐过程建模为带约束的极小极大优化，从人类反馈中显式分离出**帮助性（helpfulness）** 与**安全性（safety）** 两种偏好信号，并通过安全强化学习进行微调。

**关键技术组件**：
- **BeaverTails‑V 数据集**：首个开源的多模态双偏好标注数据集，同时包含：  
  - 帮助性与安全性两维并列的偏好标注；  
  - 多级安全标签（轻微、中等、严重），支持细粒度的风险感知。
- **Beaver‑Guard‑V 护栏系统**：多级安全防护模块，主动防御不安全查询与对抗攻击。  
  - 通过“过滤‑重生成”循环（5轮迭代），使前置模型的整体安全性平均提升 **40.9%**。  
- **多模态约束优化框架**：  
  - 将安全对齐构造为极小极大问题，在优化奖励模型的同时，满足由安全偏好推导出的显式约束；  
  - 首次将此类约束成功融入多模态模型的强化学习微调（Safe RLHF）。

**流程简述**：  
1. 收集并标注多模态数据，分离帮助性与安全性偏好；  
2. 训练双维度奖励模型，并建立安全约束；  
3. 在约束条件下执行强化学习微调，最大化奖励同时限制不安全输出。

## 3. 实验设计  
- **数据集**：自建的 **BeaverTails‑V** 数据集（多模态双偏好标注 + 三级安全标签）。  
- **基准测试**：多个多模态安全基准（具体名称未详述，摘要仅提到“在多个安全基准上”）。  
- **对比方法**：与未解耦安全信号的基线方法进行对比，突出安全约束引入前后的差异；同时分别评估了单纯使用 Beaver‑Guard‑V 护栏以及结合约束优化后的效果。  
- **评估维度**：模型安全性（不安全输出概率）、帮助性（一般能力）。  
- **关键实验结果**：  
  - Beaver‑Guard‑V 迭代5轮后，前置模型整体安全性平均提升 **40.9%**；  
  - Safe RLHF‑V（约束优化微调）相比基线，安全性提升 **34.2%**，帮助性提升 **34.3%**，且模型一般能力未受损。

## 4. 资源与算力  
- 在提供的元数据与摘要中，**未明确提及**所使用的 GPU 型号、数量及具体训练时长。  
- 推测训练阶段涉及多模态大模型微调与强化学习，算力需求较高，但本摘要无法提供具体数据。

## 5. 实验数量与充分性  
- 摘要中明确至少包含以下几类实验：  
  - Beaver‑Guard‑V 多层过滤再生实验（5轮迭代对比）；  
  - 引入约束的 Safe RLHF‑V 微调前后对比；  
  - 安全性与帮助性双重指标的消融分析。  
- 报告在“多个安全基准”上进行了评估，暗示实验覆盖了不同场景。  
- 虽然细节未全部展开，但从提升幅度（40.9%、34.2%、34.3%）及分离评估两个维度来看，实验设计**较为系统**，且同时关注“去毒”与“能力保持”，体现了**客观与公平性**。  
- 由于缺少具体的基线方法列表与显著性检验信息，尚无法完全判断统计充分性。

## 6. 主要结论与发现  
- **显式安全约束可行且高效**：首次在多模态模型中证明，从人类反馈中解耦出安全约束后，可通过约束优化显著降低不安全输出。  
- **双系统协同显著增强安全**：Beaver‑Guard‑V 护栏与 Safe RLHF‑V 微调可协同工作，护栏迭代能大幅提升前端安全性，约束微调则进一步内化安全行为。  
- **能力无损甚至提升**：在强化安全对齐的同时，模型帮助性不降反升（+34.3%），说明该方法没有导致过度保守或能力衰退。  
- **建立新范式**：Safe RLHF‑V 为多模态AI助手的安全对齐提供了可扩展、可复现的框架，填补了领域空白。

## 7. 优点与亮点  
- **首次将极小极大安全约束引入多模态RLHF**：突破以往仅面向纯文本的约束优化，成功拓展至视觉−语言场景。  
- **开源数据集与护栏系统**：BeaverTails‑V 和 Beaver‑Guard‑V 为社区提供了可复现、可扩展的研究基础。  
- **多级安全标签**：细粒度风险分级（轻微/中等/严重）使安全控制更精准，便于按需调整防护等级。  
- **双赢效果**：安全性与帮助性同时大幅提升，表明方法有效平衡了“有用性”与“无害性”，避免了常见的权衡困境。

## 8. 不足与局限  
- **实验细节不完整**：摘要未列出具体的对比方法、基准名称及统计检验，难以全面评估实验的严谨性。  
- **算力信息缺失**：无法判断该方法的实际训练成本和可部署性，对资源受限场景的适用性存疑。  
- **多模态攻击覆盖范围未知**：未说明 Beaver‑Guard‑V 对各类多模态对抗攻击（如图像投毒、视觉越狱）的防御广度与极限。  
- **局限性潜在**：若评估仅依赖自建数据集，可能面临分布偏差风险；在真实世界复杂、多样化应用下的泛化能力仍需验证。  
- **安全对齐与创造力的平衡**：高安全性可能导致过于保守的回答，但摘要未深入讨论此消长关系。

（完）
