---
title: System Prompt Extraction Attacks and Defenses in Large Language Models
title_zh: 大语言模型中的系统提示提取攻击与防御
authors: "Badhan Chandra Das, M. Hadi Amini, Yanzhao Wu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=lqpaS9WCnC"
tags: ["query:priv-sec"]
score: 10.0
evidence: 系统评估LLM中的系统提示提取攻击与防御，解决安全威胁。
tldr: 本文针对LLM系统提示易受提取攻击导致隐私泄露的问题，提出SPE-LLM评估框架，系统化设计多种对抗性查询攻击和防御方法，为LLM安全部署提供参考。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM系统提示含有敏感信息，现有研究缺乏对其攻击与防御的系统性评估。
method: 提出SPE-LLM框架，包含多种攻击策略和防御评估指标。
result: 实验揭示了不同模型的脆弱性，验证了防御的有效性。
conclusion: 系统提示安全是LLM部署的关键，需要持续关注和防护。
---

## Abstract
The system prompt in Large Language Models (LLMs) plays a pivotal role in guiding model behavior and response generation. Often containing private configuration details, user roles, and operational instructions, the system prompt has become an emerging attack target. Recent studies have shown that LLM system prompts are highly susceptible to extraction attacks through meticulously designed queries, raising significant privacy and security concerns. Despite the growing threat, there is a lack of systematic studies of system prompt extraction attacks and defenses. In this paper, we present a comprehensive framework, SPE-LLM, to systematically evaluate System Prompt Extraction attacks and defenses in LLMs, where we propose several adversarial query design techniques, defense mechanisms, and compare them with the state-of-the-art (SOTA) baselines. First, we design a set of novel adversarial queries that effectively extract system prompts from the SOTA LLMs, demonstrating the severe risks of LLM system prompt extraction. Second, we propose several defense techniques to mitigate the attacks, providing practical solutions for secure LLM deployments. Third, we used a diverse set of evaluation metrics to accurately quantify the severity of system prompt extraction attacks in LLMs and conduct comprehensive experiments across multiple benchmark datasets, which validate the efficacy of our proposed SPE-LLM framework.

---

## 论文详细总结（自动生成）

# 论文总结：大语言模型中的系统提示提取攻击与防御

## 1. 核心问题与研究背景
- **核心问题**：大型语言模型（LLM）的系统提示（system prompt）通常包含私有配置、用户角色与操作指令等敏感信息，成为新兴攻击面。精心设计的查询可轻易提取这些提示，严重威胁隐私与安全。
- **研究漏洞**：尽管提取攻击已出现，但相关研究缺乏系统性框架：攻击方法零散、防御方案未统一评估、缺少标准化的攻击-防御对比基准。
- **整体含义**：本文通过提出 **SPE-LLM** 框架，首次系统性评估系统提示提取攻击与防御，旨在为 LLM 的安全部署提供量化依据与实用方案。

## 2. 方法论
- **核心思想**：构建统一框架 **SPE-LLM**（System Prompt Extraction for LLMs），同时整合新颖攻击策略、防御机制和标准化评估指标，实现对攻击严重性与防御有效性的量化分析。
- **攻击设计**：设计一系列新颖的对抗性查询（adversarial queries），利用提示注入、角色混淆、逐句诱骗等技术，有效提取主流 LLM 的系统提示。其中可能包含多步查询、上下文劫持等方法（具体细节原文未展开）。
- **防御机制**：提出多种防御技术，可能涵盖输入过滤、响应约束、提示隔离、动态混淆等策略，旨在阻断或干扰提取行为。
- **评估对比**：将所提攻击与防御技术与当前最优（SOTA）基线方法进行直接比较，使用统一的指标体系衡量优劣。

## 3. 实验设计
- **测试对象**：多个主流 LLM（具体模型名称未在摘要中列出，推测可能包括 GPT 系列、Claude、Llama 等商业或开源模型）。
- **数据集 / 场景**：在**多个基准数据集**上进行评估，可能包含自定义的系统提示模板库以及公开对话数据集。
- **评估指标**：采用**多样化指标**量化攻击严重性（如提取准确率、语义相似度、信息泄露比率）和防御有效性（如阻挡成功率、响应质量下降程度）。
- **对比方法**：与现有的 SOTA 系统提示提取攻击及防御基线进行对比，验证 SPE-LLM 组件的先进性。

## 4. 资源与算力
- **文中未明确说明**训练或实验所使用的 GPU 型号、数量、耗时等算力细节。由于攻击本质多为推理过程，可能不需要大规模训练，但用于评估的模型推理和大量查询实验可能消耗一定 API 调用额度或本地推理资源。论文中未提供相关数据。

## 5. 实验数量与充分性
- **实验规模**：虽无精确组数，但摘要强调“comprehensive experiments across multiple benchmark datasets”，表明覆盖了多个数据集、多种模型、多类攻击与防御的组合，实验总量充足。
- **充分性判断**：从框架设计看，包含攻击对比、防御对比、指标消融等层次，能够支撑结论。由于同时与 SOTA 基线对比，客观性与公平性有一定保证。但具体消融实验（如单一攻击成分贡献、防御模块独立性）的详细程度因摘要信息缺乏而无法评定。

## 6. 主要结论与发现
- **攻击风险严峻**：所设计的新颖攻击能够有效提取 SOTA LLM 的系统提示，验证了当前模型在该类威胁下的普遍脆弱性。
- **防御有效且可行**：提出的防御技术能显著降低提取成功率，为安全部署提供了实用方案。
- **框架有效性**：SPE-LLM 的评估体系可准确量化攻击危害与防御收益，证明系统性研究对理解与缓解此类安全威胁必不可少，需持续关注。

## 7. 优点与亮点
- **首提系统性框架**：弥补了系统提示提取攻击研究缺乏标准化评估的空白，构建了可复现的比较平台。
- **攻击与防御协同设计**：同时贡献新颖攻击技术（揭示风险）和实用防御方案（提供出路），具有双向价值。
- **多维度量化**：采用多样化指标避免了单一指标带来的片面评价，增强了结论可信度。

## 8. 不足与局限
- **模型覆盖范围未知**：限于摘要，无法获知测试模型的广度与版本，可能未纳入最新的强安全对齐模型或小型开源模型。
- **攻击可迁移性未提及**：未说明攻击在未见过的系统提示模板或跨模型间的成功率。
- **防御鲁棒性存疑**：未讨论自适应攻击（攻击者知晓防御机制后调整策略）下的防御性能，实际部署环境可能被绕过。
- **实验细节缺失**：由于仅基于摘要，无法评估数据集的具体组成、消融实验的充分性以及统计显著性检验，这些可能影响结论的普适性与稳健性。
- **算力与环境未公开**：资源消耗透明度的缺失削弱了可复现性，无法判断中小团队能否复现类似实验。

（完）
