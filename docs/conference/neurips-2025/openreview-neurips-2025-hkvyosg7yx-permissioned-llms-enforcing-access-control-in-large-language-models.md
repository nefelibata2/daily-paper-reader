---
title: "Permissioned LLMs: Enforcing Access Control in Large Language Models"
title_zh: 权限化大语言模型：在大语言模型中强制执行访问控制
authors: "Bargav Jayaraman, Virendra Marathe, Hamid Mozaffari, William F. Shen, Krishnaram Kenthapadi"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Hkvyosg7Yx"
tags: ["query:priv-sec"]
score: 9.0
evidence: 在LLM响应中强制执行访问控制
tldr: 针对企业环境中LLM访问控制缺失问题，提出权限化大语言模型PermLLM，将组织数据访问控制结构叠加到查询响应中。通过形式化定义相关响应及其正确性判定，为LLM的访问控制实施提供了理论基础和实现方法。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 企业数据访问控制在LLM应用中被破坏。
method: 提出PermLLM，将访问控制规则融入LLM生成过程。
result: 形式化证明了访问控制实施正确性并可检测。
conclusion: PermLLM为LLM安全访问企业数据提供了可行方案。
---

## Abstract
In enterprise settings, organizational data is segregated, siloed and carefully protected by elaborate access control frameworks. These access control structures can completely break down if an LLM fine-tuned on the siloed data serves requests, for downstream tasks, from individuals with disparate access privileges. We propose Permissioned LLMs (PermLLM), a new class of LLMs that superimpose the organizational data access control structures on query responses they generate. We formalize abstractions underpinning the means to determine whether access control enforcement happens correctly over LLM query responses. Our formalism introduces the notion of a relevant response that can be used to prove whether a PermLLM mechanism has been implemented correctly. We also introduce a novel
metric, called access advantage, to empirically evaluate the efficacy of a PermLLM mechanism. We introduce three novel PermLLM mechanisms that build on Parameter Efficient Fine-Tuning to achieve the desired access control. We furthermore present two instantiations of access advantage–(i) Domain Distinguishability Index (DDI) based on Membership Inference Attacks, and (ii) Utility Gap Index (UGI)
based on LLM utility evaluation. We demonstrate the efficacy of our PermLLM mechanisms through extensive experiments on five public datasets (GPQA, RCV1, SimpleQA, WMDP, and PubMedQA), in addition to evaluating the validity of DDI and UGI metrics themselves for quantifying access control in LLMs.

---

## 论文详细总结（自动生成）

# 权限化大语言模型（PermLLM）论文深入总结

## 1. 论文的核心问题与整体含义

- **研究背景**：企业环境中，组织数据被严格隔离、分类并受到复杂的访问控制框架保护。然而，当基于这些隔离数据微调的大语言模型（LLM）为拥有不同访问权限的用户提供服务时，原有的访问控制结构可能完全失效。
- **核心问题**：传统LLM在生成响应时，无法感知或执行企业数据访问控制的细粒度规则，导致信息泄露风险（如低权限用户获取高敏感数据信息）。
- **整体含义**：提出权限化LLM（Permissioned LLMs，简称PermLLM），将组织的访问控制结构强制叠加到LLM的生成响应上，实现LLM层面的访问控制实施，从而安全地支持企业数据服务。

## 2. 论文提出的方法论

- **核心思想**：PermLLM不是将访问控制放在应用层，而是内嵌到LLM的响应生成过程中，确保模型输出仅包含请求者有权访问的数据内容。
- **形式化抽象**：
  - 引入“相关响应”（relevant response）概念，用于判定LLM的响应是否符合访问控制规则。
  - 定义访问控制正确性判定机制，以证明PermLLM机制实现正确。
- **关键创新指标**：
  - **访问优势（Access Advantage）**：用于实证评估PermLLM机制有效性的新度量指标。
- **三种PermLLM机制**：基于参数高效微调（Parameter Efficient Fine-Tuning, PEFT）构建，具体包括：
  - 机制一（文中未详述）：利用PEFT适配访问权限。
  - 机制二（文中未详述）：进一步细化控制粒度。
  - 机制三（文中未详述）：可能的集成或增强方法。
- **访问优势的两种实例化**：
  - **领域可区分性指数（Domain Distinguishability Index, DDI）**：基于成员推理攻击（Membership Inference Attacks）衡量模型在不同访问域下的区分能力。
  - **效用差距指数（Utility Gap Index, UGI）**：基于LLM效用评估，测量权限控制对模型有用性的影响。

## 3. 实验设计

- **数据集**：使用五个公开数据集进行实验，覆盖不同领域和复杂度：
  - **GPQA**（General Physics Questions Answering）：通用物理问答。
  - **RCV1**（Reuters Corpus Volume 1）：新闻文本分类。
  - **SimpleQA**：可能为简单问答数据集。
  - **WMDP**（Weapons of Mass Destruction Proxy）：敏感知识基准测试。
  - **PubMedQA**：生物医学问答。
- **Benchmark/场景**：测试各数据集中不同访问权限划分（如组织内部不同部门、不同安全级别）下的模型表现，验证PermLLM在防泄露与保持效用之间的平衡。
- **对比方法**：论文未在摘要中明确列出具体对比基线，但可推测对比了未加权限控制的普通微调LLM，以及可能的其他访问控制方法（如基于提示、输出过滤等）。

## 4. 资源与算力

- **算力信息**：在提供的摘要和元数据中**未明确说明**所使用的GPU型号、数量及训练时长。由于是NeurIPS 2025录用论文，通常会在正文中描述计算资源（如A100 80GB等），但本次提取文本未包含此细节。需阅读全文方可知晓。

## 5. 实验数量与充分性

- **实验覆盖**：涉及**五个数据集**，涵盖问答题、文本分类、知识基准等不同类型，具有一定的领域广度。
- **评估指标**：不仅测试了权限控制的防泄露能力（DDI），还评估了对模型效用折损（UGI），并且验证了DDI和UGI本身作为量化LLM访问控制的有效性，实验设计考虑较为全面。
- **消融与分析**：摘要提到“广泛实验”以及评估“DDI和UGI指标本身的有效性”，暗示可能包含消融实验或参数分析，但细节不详。
- **客观性与公平性**：使用公开数据集和标准推理攻击（成员推理攻击）来构建DDI，提升了评估的客观性。通过效用差距评估，避免了片面追求安全性而牺牲模型实用性，较为公平。

## 6. 论文的主要结论与发现

- PermLLM能够有效将组织数据访问控制规则叠加到LLM响应中。
- 提出的形式化框架可证明PermLLM机制是否正确实施。
- 新指标“访问优势”能成功量化和评估LLM中访问控制的效果。
- 基于PEFT的三种PermLLM机制在多个数据集上展示出良好的效能。
- DDI和UGI作为实例化指标，能够区分不同权限级别下的模型保护能力与效用损失，验证了其作为评价标准的可行性。

## 7. 优点

- **形式化基础扎实**：引入相关响应和正确性证明概念，为访问控制的LLM内嵌提供了理论保障。
- **指标创新**：提出访问优势及其两种具体指标（DDI和UGI），将安全性评估和效用评估统一，解决了仅看泄露的片面问题。
- **机制轻量**：采用参数高效微调（PEFT）而非全参数微调，利于实际部署与多权限快速适配。
- **实验多样性强**：覆盖常识问答、专业知识、安全敏感内容等多种数据集，验证方法的泛化能力。

## 8. 不足与局限

- **细节缺失**：摘要未描述三种PermLLM机制的具体技术实现，无法深入评估其复杂性与局限性。
- **实验对比基线不明**：未提及与传统访问控制方法（如输入过滤、输出审查、基于prompt的限制）的对比，难以判断性能提升的幅度是否显著。
- **应用限制讨论不足**：实际企业应用中，访问控制策略可能动态变化、涉及组合权限等复杂情形，摘要未涉及此类场景。
- **算力信息披露不足**：无法评估方法的资源消耗和可复现门槛。
- **偏差风险**：基于成员推理攻击构建的DDI指标本身可能受数据分布影响，需警惕评估结果的可靠性。

（完）
