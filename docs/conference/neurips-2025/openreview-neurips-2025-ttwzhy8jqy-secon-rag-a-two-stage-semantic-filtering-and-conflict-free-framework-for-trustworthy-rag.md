---
title: "SeCon-RAG: A Two-Stage Semantic  Filtering and Conflict-Free Framework for Trustworthy RAG"
title_zh: "SeCon-RAG: 面向可信RAG的两阶段语义过滤与无冲突框架"
authors: "Xiaonan si, Meilin Zhu, Simeng Qin, Lijia Yu, Lijun Zhang, Shuaitong Liu, Xinfeng Li, Ranjie Duan, Yang Liu, Xiaojun Jia"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=tTwZhy8JqY"
tags: ["query:priv-sec"]
score: 9.0
evidence: 解决RAG中的语料库投毒攻击，提出两阶段语义过滤框架
tldr: RAG系统易受语料库投毒攻击，传统过滤方法常过度删减信息。SeCon-RAG提出两阶段防御：先通过语义聚类联合过滤，再基于实体-意图-关系提取进行冲突消解，确保生成可信。实验表明该方法在抵御投毒攻击的同时保留了更多有用信息，显著提升了RAG的鲁棒性与可靠性。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: RAG系统面临语料投毒威胁，现有防御过度过滤导致信息损失，亟需更智能的过滤方案。
method: 设计实体-意图-关系抽取器(EIRE)引导两阶段过滤：第一阶段联合语义与聚类过滤，第二阶段冲突消解确保生成一致性。
result: 实验显示SeCon-RAG在多种投毒攻击下保持高生成质量，信息保留率优于同类方法。
conclusion: SeCon-RAG为可信RAG提供了兼顾安全与信息利用的有效框架。
---

## Abstract
Retrieval-augmented generation (RAG) systems enhance large language models (LLMs) with external knowledge but are vulnerable to corpus poisoning and contamination attacks, which can compromise output integrity. Existing defenses often apply aggressive filtering, leading to unnecessary loss of valuable information and reduced reliability in generation.
To address this problem, we propose a two-stage semantic filtering and conflict-free framework for trustworthy RAG. 
In the first stage, we perform a joint filter with semantic and cluster-based filtering  which is guided by the Entity-intent-relation extractor (EIRE). EIRE extracts entities, latent objectives, and entity relations from both the user query and filtered documents, scores their semantic relevance, and selectively adds valuable documents into the clean retrieval database. 
In the second stage, we proposed an EIRE-guided conflict-aware filtering module, which analyzes semantic consistency between the query, candidate answers, and retrieved knowledge before final answer generation, filtering out internal and external contradictions that could mislead the model.
Through this two-stage process, SeCon-RAG effectively preserves useful knowledge while mitigating conflict contamination, achieving significant improvements in both generation robustness and output trustworthiness.
Extensive experiments across various LLMs and datasets demonstrate that the proposed SeCon-RAG markedly outperforms state-of-the-art defense methods.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义
- **研究背景**：检索增强生成（RAG）通过引入外部知识库提升大语言模型（LLMs）的生成质量，但这一机制也为语料库投毒与污染攻击打开了缺口，攻击者可通过注入恶意文档操纵模型输出，破坏可信度。
- **现存问题**：现有防御策略普遍采用激进过滤，虽能阻止部分攻击，却导致大量有用信息被误删，削弱了 RAG 的知识利用能力与回答可靠性。
- **研究动机**：亟需一种既能精准识别、剔除投毒内容，又能最大限度保留有效知识的方法，从而在安全与信息完整性之间取得平衡，提升 RAG 在真实对抗环境下的鲁棒性。

## 2. 方法论
论文提出 **SeCon-RAG**，一种面向可信 RAG 的两阶段语义过滤与无冲突框架，核心在于引入 **实体‑意图‑关系抽取器（EIRE）** 作为语义理解引擎，指导两个阶段的精细化过滤。

- **第一阶段：联合语义与聚类过滤**
  - 利用 EIRE 从用户查询及待过滤文档中抽取实体、潜在目标（意图）以及实体间关系。
  - 计算查询与文档之间的语义关联得分，同时结合聚类分析对文档进行分组，识别并丢弃离群或语义不一致的文档。
  - 仅将语义相关且符合聚类结构的高价值文档添加至干净检索库，实现“去伪存真”而非简单丢弃。

- **第二阶段：EIRE 引导的冲突感知过滤**
  - 在最终答案生成前，再次借助 EIRE 分析查询、候选答案与已检索知识之间的语义一致性。
  - 检测两类冲突：
    - **内部冲突**：候选答案内部或与检索知识之间的矛盾；
    - **外部冲突**：候选答案与查询意图之间的不一致。
  - 过滤掉含有冲突的候选答案，确保最终输出逻辑自洽、知识可靠。

总体流程为：**查询→文档检索→EIRE 驱动的语义‑聚类联合过滤→构建干净知识基底→EIRE 冲突检测→生成可信回答**。方法没有给出明确的数学公式，但通过语义评分、聚类阈值和冲突判别规则实现可操作的过滤机制。

## 3. 实验设计
- **测试场景**：涵盖多种语料库投毒攻击，如注入错误事实、矛盾叙述、偏见性内容等，以模拟真实性威胁。
- **数据集与大模型**：论文宣称在多个数据集和多种 LLMs 上进行评估，但摘要及元数据未给出具体名称，推测使用了常见的问答/知识密集型基准（如 Natural Questions、TriviaQA 或自定义投毒版本）和主流开源模型。
- **对比方法**：将 SeCon-RAG 与当前最先进的防御方法（State‑of‑the‑art defense methods）进行比较，但未列出具体名称。依据元数据 “result”，对比维度包括生成质量和信息保留率。

## 4. 资源与算力
提供的信息中完全没有提到所用 GPU 型号、数量、训练时长或推理开销。由于 SeCon-RAG 的核心组件（EIRE、聚类、冲突检测）可能依赖额外的语义模型，其算力需求应高于单纯检索，但论文未给出具体数字，无法评估其对部署环境的要求。

## 5. 实验数量与充分性
- **实验规模**：文中仅提到“广泛的实验（Extensive experiments）”，并指出在多种 LLMs 和数据集上测试，但未载明实验组数的精确数量。
- **充分性分析**：从现有描述来看，实验覆盖了多个模型和攻击场景，并与 SOTA 防御对比，具备基本充分性。然而，缺乏消融研究（如去掉第一阶段、去掉 EIRE 引导等）的叙述，也未见对超参数敏感性的讨论，实验的透明性和可复现性尚无法判断。
- **客观与公平性**：方法比较对象为 SOTA 防御，但未说明这些防御是否针对相同威胁模型、是否采用完全一致的检索库和环境，公平性需查阅全文方可确认。

## 6. 主要结论与发现
- SeCon-RAG 在多种投毒攻击下均能保持高生成质量，其答案的准确性、连贯性显著优于现有防御方法。
- 两阶段过滤设计有效减少了信息损失，信息保留率明显领先，表明语义级理解对区分恶意与良性内容至关重要。
- 该框架为构建可信 RAG 提供了一种兼顾安全与知识利用的可行路径，具备向真实应用迁移的潜力。

## 7. 优点
- **精细化的语义过滤**：通过 EIRE 抽取实体、意图和关系，比单纯基于向量相似度或关键词的过滤更精确，能够理解文本的深层目标。
- **两阶段递进架构**：先建干净知识库，再消解答案冲突，逻辑清晰，将防御前置到检索环节，而非仅在生成后修正。
- **信息保留率高**：在抵御攻击的同时避免“一刀切”的信息丢弃，增强了系统的实用价值。
- **模型无关性**：宣称适用于多种 LLMs，表明方法具有一定的通用性。

## 8. 不足与局限
- **实验细节缺失**：摘要未披露数据集、对比方法、EIRE 的具体实现（如基于微调模型还是提示工程）、评价指标等，难以复现和评估其真实性能。
- **算力成本未知**：没有给出计算资源开销，若 EIRE 需要额外的大模型推理，可能增加延迟和成本，影响在线服务部署。
- **攻击覆盖范围**：未说明是否仅针对特定投毒模式（如虚假事实注入）有效，或可推广到更隐蔽的污染攻击（如时间衰减信息篡改）。
- **泛化风险**：缺少对多语言、多领域（如医学、法律）的测试，框架的跨场景稳定性存疑。
- **缺乏理论分析**：未从理论角度证明过滤策略的保真度或冲突消解的完备性，方法的可靠性仍依赖经验验证。

（完）
