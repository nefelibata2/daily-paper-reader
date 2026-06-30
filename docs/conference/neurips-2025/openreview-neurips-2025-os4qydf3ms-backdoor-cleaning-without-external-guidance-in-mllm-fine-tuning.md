---
title: Backdoor Cleaning without External Guidance in MLLM Fine-tuning
title_zh: 无须外部指导的后门清洗：面向多模态大语言模型微调
authors: "Xuankun Rong, Wenke Huang, Jian Liang, Jinhe Bi, Xun Xiao, Yiming Li, Bo Du, Mang Ye"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=os4QYDf3Ms"
tags: ["query:priv-sec"]
score: 10.0
evidence: 通过注意力坍缩识别后门样本，无需外部监督进行过滤
tldr: 多模态大语言模型在微调即服务场景中面临后门攻击风险。本文发现后门触发会导致注意力异常集中，即注意力坍缩现象。基于此提出BYE（相信你的眼睛）框架，利用注意力熵模式作为自监督信号，自动识别并过滤后门样本，无需外部指导。实验表明BYE能有效清洗后门数据，抵御微调攻击，为MLLM的安全部署提供了一种轻量高效的防御方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 微调即服务中的后门攻击隐蔽且防御依赖外部指导。
method: 发现注意力坍缩现象，利用注意力熵自监督识别后门样本并过滤。
result: 无需外部指导，有效清洗后门数据，防御攻击。
conclusion: 为MLLM安全微调提供了基于注意力异常的自监督防御机制。
---

## Abstract
Multimodal Large Language Models (MLLMs) are increasingly deployed in fine-tuning-as-a-service (FTaaS) settings, where user-submitted datasets adapt general-purpose models to downstream tasks. This flexibility, however, introduces serious security risks, as malicious fine-tuning can implant backdoors into MLLMs with minimal effort. In this paper, we observe that backdoor triggers systematically disrupt cross-modal processing by causing abnormal attention concentration on non-semantic regions—a phenomenon we term **attention collapse**. Based on this insight, we propose **Believe Your Eyes (BYE)**, a data filtering framework that leverages attention entropy patterns as self-supervised signals to identify and filter backdoor samples. BYE operates via a three-stage pipeline: (1) extracting attention maps using the fine-tuned model, (2) computing entropy scores and profiling sensitive layers via bimodal separation, and (3) performing unsupervised clustering to remove suspicious samples. Unlike prior defenses, BYE equires no clean supervision, auxiliary labels, or model modifications. Extensive experiments across various datasets, models, and diverse trigger types validate BYE's effectiveness: it achieves near-zero attack success rates while maintaining clean-task performance, offering a robust and generalizable solution against backdoor threats in MLLMs.

---

## 论文详细总结（自动生成）

由于提供的材料仅为论文元数据和摘要（不包含全文），以下总结将基于这些有限信息展开。对于部分需要全文细节才能回答的问题（如具体数据集、算力等），我将指出信息缺失。

## 1. 研究动机与背景
- **核心问题**：多模态大语言模型（MLLM）在“微调即服务”（FTaaS）场景中被广泛使用，但用户上传的数据集可能被恶意注入后门。攻击者只需通过微调就能植入后门，而这在现实部署中极难防范。
- **主要挑战**：现有后门防御方案通常依赖外部指导——如使用干净样本的监督、辅助标签或修改模型结构——这在“服务提供方只能拿到用户提交的混合数据”的实际场景中往往不具备可行性。
- **整体含义**：本文旨在提出一种完全无须外部指导、仅依靠模型内部信号的后门清洗方法，使MLLM的安全微调更加自主和实用。

## 2. 方法论：BYE（相信你的眼睛）框架
- **核心思想**：作者首次观察到后门触发会系统性地破坏跨模态处理，导致模型注意力异常地集中于非语义区域，将这一现象命名为 **“注意力坍缩”（attention collapse）**。 
- **技术路线**：利用注意力熵作为自监督信号，自动识别并过滤含有后门触发器的样本，整个框架命名为 **Believe Your Eyes (BYE)**。
- **三阶段流程**（用自然语言概括）：
    1. **注意力图提取**：使用已微调的MLLM对每个样本提取跨模态注意力图。
    2. **熵分数计算与敏感层定位**：基于注意力图计算注意力熵，并通过双模态分离（bimodal separation）找出对后门最敏感的那些层。
    3. **无监督聚类与清洗**：在敏感层的熵分数上进行无监督聚类，将离群的、熵值异常低的样本（即呈现注意力坍缩的样本）判定为后门样本并移除。
- **关键差异**：整个过程不需要任何干净标签、辅助模型、外部参考数据，也不对原模型做任何修改，完全利用模型自身的注意力模式作为自监督线索。

## 3. 实验设计
由于只有摘要和元数据，以下信息为摘要中的概括性描述：
- **数据集与场景**：摘要中提到“在各种数据集、模型和多样的触发器类型上进行了广泛实验”，但并未列出具体的数据集名称（如COCO、VQA等）或攻击类型。
- **评估指标（Benchmark）**：主要衡量指标为**攻击成功率（ASR）** 和**干净任务性能**。目标是ASR降到接近零，同时保持原有的下游任务准确率。
- **对比方法**：文中提及“与之前需要外部指导的防御不同”，暗示可能对比了使用干净样本监督或辅助标签的防御方案，但具体对比的方法名称在摘要及元数据中未出现。

## 4. 资源与算力
- **信息缺失**：在提供的材料中，**完全没有提及** GPU型号、数量、训练时长等任何算力相关信息。这一部分无法评估。

## 5. 实验数量与充分性
- **实验数量**：无法得知具体组数。摘要强调“广泛实验”（Extensive experiments），暗示可能涵盖了多种数据集、模型架构和触发器变种，也可能包含消融实验（如分析不同层的作用、聚类算法的选择等）。
- **充分性与公平性**：从宣称的结果（近零ASR且维持干净性能）来看，作者认为防御是全面且鲁棒的。但缺少具体数据集数量和类型，难以独立判断覆盖度是否足够。若没有具体对比方法名称和设定，公平性也无法具体评价。

## 6. 主要结论与发现
- **现象发现**：首次揭示并利用了MLLM后门攻击中的“注意力坍缩”现象。
- **防御效果**：BYE框架在不需要任何外部指导的情况下，能够将攻击成功率降至接近零，同时不影响模型在原始任务上的正常表现。
- **整体意义**：为微调即服务场景下的MLLM安全提供了一种通用、轻量、自监督的后门清洗方案。

## 7. 优点
- **完全自监督**：不依赖干净样本、辅助标签或任何外部知识，极大简化了部署条件。
- **无侵入性**：无需修改模型结构或重新训练，仅通过数据过滤实现防御。
- **物理发现驱动**：将安全机制建立在可解释的“注意力坍缩”现象之上，技术路线具有新意。
- **通用性强**：声言在多种模型、数据集和触发器上均有效。

## 8. 不足与局限（基于现有信息推测）
- **实验细节未公开**：摘要和元数据未提供数据集、触发器类型、对比基线等关键信息，无法评估实验的全面性和结论的适用范围。
- **注意力坍缩的普适性存疑**：是否所有类型的后门触发器都会引起显著的注意力坍缩？对于与语义高度融合的隐蔽触发器，该现象可能减弱，但本文未讨论。
- **算力成本未知**：需要在每个样本上提取全模型注意力图进行聚类，当样本量极大时计算开销可能成为瓶颈，但文中未提供复杂度分析。
- **实际部署门槛**：该方法仍然要求防御方能够完全访问微调后的模型内部注意力加权结果，这在某些服务契约下可能无法满足。

（完）
