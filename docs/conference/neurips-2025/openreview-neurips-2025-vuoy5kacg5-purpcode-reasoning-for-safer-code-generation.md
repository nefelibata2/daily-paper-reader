---
title: "PurpCode: Reasoning for Safer Code Generation"
title_zh: PurpCode：面向更安全代码生成的推理训练
authors: "Jiawei Liu, Nirav Diwan, Zhe Wang, Haoyu Zhai, Xiaona Zhou, Kiet A. Nguyen, Tianjiao Yu, Muntasir Wahed, Yinlin Deng, hadjer Benkraouda, Yuxiang Wei, LINGMING ZHANG, Ismini Lourentzou, Gang Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=VUoY5kacG5"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过推理和强化学习训练安全代码生成
tldr: 现有代码大模型缺乏生成安全代码和抵御恶意利用的内在能力。PurpCode提出首个后训练方案，通过规则学习阶段显式注入网络安规规则，再经强化学习阶段利用多目标奖励机制优化安全性与实用性。基于真实世界任务进行内部红队测试，合成了高覆盖度的诱导不安全代码的提示。实验表明，该方法在不牺牲代码功能的前提下，显著降低了漏洞产生和恶意协助行为，为代码生成模型的安全性对齐提供了有效路径。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 代码大模型易生成漏洞代码或被恶意利用，缺乏系统的安全训练方法。
method: 分两阶段后训练：规则学习注入安全知识，多目标强化学习平衡安全与功能。
result: 在多种基准上，生成代码的漏洞率大幅降低，且抵御恶意提示的能力显著增强。
conclusion: PurpCode首次实现了代码生成模型的安全对齐，对安全关键领域应用意义重大。
---

## Abstract
We introduce PurpCode, the first post-training recipe for training safe code reasoning models towards generating secure code and defending against malicious cyberactivities. PurpCode trains a reasoning model in two stages: (i) Rule Learning, which
explicitly teaches the model to reference cybersafety rules to generate vulnerability-free code and to avoid facilitating malicious cyberactivities; and (ii) Reinforcement Learning, which optimizes model safety and preserves model utility through diverse, multi-objective reward mechanisms. To empower the training pipelines with comprehensive cybersafety data, we conduct internal red-teaming to synthesize comprehensive and high-coverage prompts based on real-world tasks for inducing unsafe cyberactivities in the model. Based on PurpCode, we develop a reasoning-based coding model, namely PurpCode-32B, which demonstrates state-of-the-art cybersafety,
outperforming various frontier models. Moreover, our alignment method decreases the model overrefusal rates in both general and cybersafety-specific scenarios, while preserving model utility in both code generation and common security knowledge.

---

## 论文详细总结（自动生成）

# PurpCode：面向更安全代码生成的推理训练

## 1. 核心问题与研究动机
- 现有大型代码生成模型（如代码 LLM）在生成功能代码的同时，容易产生安全漏洞（如注入、缓冲区溢出等），甚至可能在恶意提示下主动协助网络攻击。
- 缺乏系统性的训练方法，使模型能**内生地**遵循网络安全规则、抵御恶意滥用，而不牺牲常规代码生成能力和一般安全常识。
- PurpCode 正是为此提出首个后训练方案，旨在对齐代码推理模型与安全目标，实现“生成安全代码”与“拒绝恶意请求”的双重约束。

## 2. 方法论：两阶段后训练对齐
### 2.1 整体思路
- 以预训练代码模型为基础，通过两阶段训练，显式注入安全知识并利用强化学习平衡安全性与实用性。
- 关键设计：内部红队合成高覆盖度的**诱导不安全行为**的提示，为训练提供全面网络安全数据。

### 2.2 阶段一：规则学习 (Rule Learning)
- 显式教授模型**引用网络安全规则**（如 OWASP 准则、CWE 分类等），指导模型在代码生成时主动规避漏洞。
- 同时训练模型识别并拒绝辅助恶意网络活动（如生成恶意软件、社会工程攻击代码等）。
- 目标：让模型形成“规则→安全代码”的推理路径，降低基本漏洞生成率。

### 2.3 阶段二：强化学习 (Reinforcement Learning)
- 构建**多目标奖励机制**：  
  - 安全性奖励：衡量生成代码是否含漏洞、是否拒绝危险请求。  
  - 实用性奖励：保生成代码的功能正确性、与 prompt 的相关性。  
  - 过拒绝惩罚：防止模型因过度敏感而拒绝无害请求（安全与一般场景均考虑）。  
- 通过 RL 优化，在保持甚至提升代码生成能力的同时，将安全策略内化到推理过程中。

### 2.4 数据合成：内部红队测试
- 基于真实世界开发任务与网络安全场景，人工设计（或半自动生成）大量**诱导不安全输出**的 prompt。
- 覆盖多种攻击面：代码漏洞注入、恶意工具生成、绕过安全限制等，确保训练数据的高危害覆盖。
- 该数据同时支持规则学习与强化学习两阶段。

## 3. 实验设计与对比
- **基准测试**：文中构建或使用了多个评估维度：  
  - 代码漏洞率基准（如针对 C/C++、Python 等常见语言的安全性测试）。  
  - 恶意请求拒绝率基准（捕捉模型是否协助网络攻击）。  
  - 过拒绝率评估（一般编码任务和网络安全常识问答中的错误拒绝）。  
  - 代码生成能力基准（如 HumanEval、MBPP 等标准代码任务）。  
  - 安全知识保持（验证模型是否遗忘一般安全常识）。
- **对比方法**：包括多种前沿模型（未详细列出，但从摘要推断可能包含 GPT-4、Claude、开源模型等）以及未对齐的基准模型。
- 最终基于 PurpCode 训练的 **PurpCode-32B** 模型被评测并取得 state-of-the-art 的网络安全性能。

## 4. 资源与算力
- 提供的摘要及元数据中**未明确提及 GPU 型号、数量、训练时长**等算力细节。
- 从模型名称“PurpCode-32B”推断基础模型规模为 32B 参数，后训练所需算力应至少为数块高端 GPU（如 A100）的多日训练，但具体数字无法得出。

## 5. 实验数量与充分性
- 基于摘要，实验覆盖了多个独立维度：
  - 安全漏洞生成率（针对多种语言/场景）。
  - 恶意活动协助率。
  - 过拒绝率（一般任务 vs 安全特定任务）。
  - 代码生成质量（功能正确性）。
  - 安全常识保持。
- 多维度对比表明实验**较为充分**，能同时验证安全性对齐的正面效果与负面代价。  
- 对比对象包含多种前沿模型，增强了结论的说服力。消融实验（如单阶段 vs 两阶段、有无 RL 等）未在摘要中提及，但常见于此类工作的完整论文中，暂无法判断是否存在。

## 6. 主要结论与发现
- PurpCode 是首个通过后训练实现代码生成模型**安全对齐**的工作，显著降低了生成代码的漏洞率。
- 能有效抵御恶意提示，大幅减少模型输出恶意协助内容的概率。
- 同时缓解了安全训练中常见的**过拒绝**问题，模型在正常编码及安全知识问答中拒绝率低于以往对齐方法。
- 保持了原代码模型的生成能力，未因安全训练而退化功能，并保留了通用安全知识。
- PurpCode-32B 在网络安全综合指标上达到领先水平，超越多种前沿模型。

## 7. 优点与亮点
- **首次性**：为代码推理模型设计了专门的安全后训练流程，填补了系统性安全对齐的空白。
- **两阶段设计**：规则学习提供显式安全知识基础，RL 则灵活平衡安全与功能，避免刻板规则导致的过度拒绝。
- **红队数据合成**：基于真实任务内部红队构建的全面安全数据，覆盖度高，针对性强。
- **多目标奖励**：同时优化安全性、实用性和拒绝率，使得实用性和安全性协同提升而非此消彼长。
- **实用性保留**：明确证明安全对齐不牺牲代码生成质量，这对工业落地至关重要。

## 8. 不足与局限
- **算力与细节缺失**：摘要未提供训练资源、超参数、数据集规模等信息，无法评估复现成本与可扩展性。
- **语言与任务覆盖**：代码安全可能侧重于某些语言（如 C/C++）；对其他语言、脚本、领域特定语言的泛化性未说明。
- **规则依赖风险**：规则学习阶段依赖的网络安全规则库可能局限已有知识，对新类型的零日漏洞可能预防有限。
- **对抗鲁棒性未知**：红队提示为内部合成，未经外部实时攻击迭代测试，可能存在过拟合到训练分布的安全表现。
- **过拒绝定义**：过拒绝的具体衡量标准未展开，不同应用场景下容忍度差异可能影响实际效用。
- **缺乏长期安全性维持**：未讨论模型在持续微调或更新后的安全退化问题。

（完）
