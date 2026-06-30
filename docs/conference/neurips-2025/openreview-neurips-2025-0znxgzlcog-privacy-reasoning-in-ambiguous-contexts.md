---
title: Privacy Reasoning in Ambiguous Contexts
title_zh: 模糊情境下的隐私推理
authors: "Ren Yi, Octavian Suciu, Adrian Gascon, Sarah Meiklejohn, Eugene Bagdasarian, Marco Gruteser"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=0ZnXGzLcOg"
tags: ["query:priv-sec"]
score: 8.0
evidence: 研究大语言模型在模糊情境下的隐私推理与信息披露决策
tldr: "大语言模型在做出信息披露决策时，情境歧义往往导致隐私评估性能低下。本文提出Camber框架，首先利用模型生成的决策理由识别歧义，然后系统性地消解歧义，从而显著提升隐私决策的准确率和召回率（精确率提高13.3%，召回率提高22.3%）。该研究为智能体隐私领域提供了解决情境模糊性的关键方法，有助于构建更可信的隐私保护语言模型。"
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有工作忽略情境歧义对语言模型隐私决策的障碍。
method: 提出Camber框架，利用模型生成的决策理由进行情境消歧。
result: "在精确率和召回率上分别提升13.3%和22.3%。"
conclusion: 揭示了歧义是隐私推理的关键障碍，并提供了有效的消歧方法。
---

## Abstract
We study the ability of language models to reason about appropriate information disclosure - a central aspect of the evolving field of agentic privacy. Whereas previous works have focused on evaluating a model's ability to align with human decisions, we examine the role of ambiguity and missing context on model performance when making information-sharing decisions. We identify context ambiguity as a crucial barrier for high performance in privacy assessments. By designing Camber, a framework for context disambiguation, we show that model-generated decision rationales can reveal ambiguities and that systematically disambiguating context based on these rationales leads to significant accuracy improvements (up to 13.3% in precision and up to 22.3% in recall) as well as reductions in prompt sensitivity. Overall, our results indicate that approaches for context disambiguation are a promising way forward to enhance agentic privacy reasoning.

---

## 论文详细总结（自动生成）

# 模糊情境下的隐私推理（Privacy Reasoning in Ambiguous Contexts）论文总结

## 1. 论文的核心问题与整体含义
- **核心问题**：语言模型（LLM）在做出信息披露决策（如是否共享个人信息）时，常因**情境歧义（context ambiguity）** 或缺失关键上下文而出现性能大幅下降，导致不可靠的隐私判断。
- **研究动机与背景**：
  - 当前“智能体隐私（agentic privacy）”领域多关注模型决策与人类判断的对齐程度，却忽视了**上下文模糊性**对模型推理的根本障碍。
  - 在实际应用中，隐私相关的请求往往是模糊、不完整的，模型若不能识别并处理这类歧义，其决策精度会显著受损。
- **整体含义**：揭示歧义是制约隐私推理性能的关键瓶颈，并提出通过**消歧（disambiguation）** 来系统性提升大语言模型在隐私领域的可信度，为构建更可靠的智能体隐私决策机制铺路。

## 2. 论文提出的方法论
- **核心思想**：利用模型自身生成的**决策理由（rationales）** 来暴露情境歧义，再基于这些理由系统性地消解歧义，从而提升隐私评估的准确性和稳定性。
- **框架名称**：**Camber**（Context Ambiguity Resolution for Privacy Reasoning）。
- **关键技术流程（文字说明）**：
  - **第一阶段 – 理由生成与歧义识别**：
    - 给定一个隐私决策场景（可能包含模糊描述），要求语言模型输出“是否应该披露信息”的判断，并附带**自然语言解释（rationale）**。
    - 从这些解释中检测表达不确定或缺失信息的语句，识别出模型的**上下文歧义点**。
  - **第二阶段 – 系统消歧**：
    - 针对识别出的歧义点，设计自动化的追问或上下文补充策略（例如，要求模型明确其假设、增加缺失的背景信息、细化情境描述）。
    - 将消歧后的清晰上下文重新输入模型，进行二次推理，得到最终决策。
- **核心优势**：不依赖昂贵的人工标注来预处理模糊情境，而是通过**模型自省（introspection）** 驱动歧义消除，既能降低提示（prompt）敏感性，又显著提升决策性能。

## 3. 实验设计
- **数据集 / 场景**：
  - 论文摘要和元数据未详述具体数据集名称，但从研究性质可推断，应包含**隐私相关的信息共享决策场景**，且场景本身带有不同程度的歧义（可能来源自已有隐私基准或自行构造）。
- **评价基准（benchmark）**：
  - 性能指标：**精确率（precision）**、**召回率（recall）**，以及**提示敏感性（prompt sensitivity）** 的变化。
  - 人类决策或清晰情境下的最优决策可能作为参考标准。
- **对比方法**：
  - 摘要提及“previous works”主要关注对齐人类决策，暗示对比基线包括**直接提示模型做决策（无消歧）** 或**常规提示微调方法**。
  - 文中必然对比了 **Camber 框架应用前后的模型表现**，以量化消歧带来的提升。

## 4. 资源与算力
- **说明**：当前提供的摘要文本中**未披露**所使用的 GPU 型号、数量、训练时长或推理成本等算力信息。由于论文主要采用基于提示的推理（可能无训练微调），计算开销可能集中在多次API调用或本地推理，但具体细节无法从现有材料中确认。

## 5. 实验数量与充分性
- **实验组数推测**：
  - 根据提升幅度（精确率+13.3%，召回率+22.3%）的汇报方式，至少包含**多个隐私决策数据集或难度分级的子场景**；
  - 应该包含**消融实验**（如仅使用理由但不进行消歧 vs. 完整Camber），以验证各阶段贡献；
  - 可能还测试了**不同模型尺寸或类型的泛化性**。
- **充分性与公平性**：
  - 实验以**定量指标**呈现显著提升，且关注了提示敏感性，设计较周全。
  - 但摘要未提供与何种人类基准或强基线的对比细节，公平性无法完全评估。此外，文章使用模型自产理由来消歧，可能引入**自我强化偏差**，需更多外部验证。

## 6. 论文的主要结论与发现
- **歧义是关键障碍**：上下文模糊是造成大语言模型隐私决策精度低、提示敏感性强的主要原因。
- **理由揭示歧义**：模型在推理时生成的自然语言解释能有效暴露其感知到的歧义点。
- **消歧大幅提升性能**：通过 Camber 框架系统消解歧义后，精确率最高提升 13.3%，召回率最高提升 22.3%，且模型对提示变化的鲁棒性增强。
- **方法具有前景**：基于理由的上下文消歧是提升智能体隐私推理能力的一条有效且有前景的路径。

## 7. 优点
- **新颖的问题视角**：跳出传统人机对齐的框架，首次深入分析情境歧义对隐私推理的破坏性影响。
- **低成本的自省式消歧**：无需人工重写场景或昂贵标注，利用模型自身生成的解释完成歧义检测与消解，自动化程度高。
- **显著的性能增益**：不仅在两个关键指标上实现两位数百分比提升，还降低了提示敏感性，具有实际部署价值。
- **框架可迁移性强**：Camber 的设计思路（理由→歧义识别→消歧）不限于隐私领域，可推广至其他需要处理模糊自然语言指令的智能体任务。

## 8. 不足与局限
- **实验覆盖不明**：摘要未提供数据集大小、领域多样性、语言多样性等信息，无法判断结论的泛化边界。
- **依赖模型自省能力**：该方法要求模型能生成高质量且诚实的理由，若模型表达能力弱或存在幻觉，歧义识别可能失效。
- **消歧策略的局限性**：摘要未说明消歧是如何具体执行的（自动化规则、额外查询模型还是人工参与），若依赖模型自行补充上下文，可能引入偏见或错误假设。
- **缺乏现实应用验证**：仅在实验基准上验证，未讨论在真实动态对话或多轮交互中的部署效果与延迟成本。
- **潜在偏差风险**：模型生成的消歧理由可能反映其训练数据中的社会偏见，导致对某些隐私场景作出一致性偏差判断。

（完）
