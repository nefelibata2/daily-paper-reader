---
title: "Gandalf the Red: Adaptive Security for LLMs"
title_zh: Gandalf the Red：大语言模型的自适应安全
authors: "Niklas Pfister, Václav Volhejn, Manuel Knott, Santiago Arias, Julia Bazinska, Mykhailo Bichurin, Alan Y. Commike, Janet Darling, Peter Dienes, Matthew Fiedler, David Haber, Matthias Kraft, Marco Lancini, Max Mathys, Damian Pascual-Ortiz, Jakub Podolak, Adrià Romero-López, Kyriacos Shiarlis, Andreas Signer, Zsolt Terek, Athanasios Theocharis, Daniel Timbrell, Samuel Trautwein, Samuel Watts, Yun-Han Wu, Mateo Rojas-Carulla"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Y861SAkeCQ"
tags: ["query:priv-sec"]
score: 9.0
evidence: 解决LLM面临的提示攻击安全威胁，并提出自适应防御评估框架。
tldr: 本文针对现有LLM防御评估忽略动态攻击行为和用户可用性损失的问题，提出D-SEC威胁模型和Gandalf众包红队平台，通过279k条自适应攻击数据集揭示安全-效用的平衡，更真实地评估防御效果。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 当前防御评估未考虑攻击的动态性和防御对正常用户的可用性影响。
method: 提出D-SEC模型和Gandalf平台，收集大量自适应攻击数据，量化安全-效用权衡。
result: 数据集分析表明防御必须兼顾安全性和对良性用户的影响。
conclusion: 为构建更贴近实战的LLM安全评估提供了新框架和基准。
---

## Abstract
Current evaluations of defenses against prompt attacks in large language model (LLM) applications often overlook two critical factors: the dynamic nature of adversarial behavior and the usability penalties imposed on legitimate users by restrictive defenses. We propose D-SEC (Dynamic Security Utility Threat Model), which explicitly separates attackers from legitimate users, models multi-step interactions, and expresses the security-utility in an optimizable form. We further address the shortcomings in existing evaluations by introducing Gandalf, a crowd-sourced, gamified red-teaming platform designed to generate realistic, adaptive attack. Using Gandalf, we collect and release a dataset of 279k prompt attacks. Complemented by benign user data, our analysis reveals the interplay between security and utility, showing that defenses integrated in the LLM (e.g., system prompts) can degrade usability even without blocking requests. We demonstrate that restricted application domains, defense-in-depth, and adaptive defenses are effective strategies for building secure and useful LLM applications.

---

## 论文详细总结（自动生成）

# Gandalf the Red：大语言模型的自适应安全

## 1. 核心问题与研究背景
- **研究动机**：当前大语言模型（LLM）在面对提示攻击（prompt attack）时，其防御评估存在两个严重盲点：
  - **动态攻击行为被忽略**：攻击者会不断调整策略，现有评估多为静态、单步测试，无法反映自适应攻击的真实威胁。
  - **可用性惩罚被低估**：过度保守的防御措施会严重干扰合法用户（benign users）的正常使用，但该影响很少被量化。
- **整体含义**：论文试图建立一个更接近真实攻防场景的评估框架，在安全性与可用性之间寻求可优化的平衡，从而指导构建既安全又好用的 LLM 应用。

## 2. 方法论
### 2.1 D-SEC 威胁模型
- **核心思想**：将攻击者与合法用户显式分离，建模多步交互（multi-step interactions），并将安全-效用权衡表达为可优化的形式（optimizable form）。
- **关键组成**（基于摘要推断）：
  - 动态威胁视图：攻击者可根据防御的反应自适应调整攻击策略。
  - 效用度量：量化防御对合法请求的负面影响，例如响应延迟、内容误拦、信息完整性下降等。
  - 联合优化：在给定攻防约束下，寻求安全与效用的帕累托最优。

### 2.2 Gandalf 众包红队平台
- **设计思路**：通过游戏化（gamified）方式，激励大量参与者不断尝试攻破 LLM 的防御，从而自然产生自适应攻击序列。
- **技术特点**：
  - 面向公众的在线挑战，参与者在不知晓内部防御机制的条件下进行黑盒攻击。
  - 平台记录完整的多轮对话，形成攻击者动态调整策略的数据流。
  - 同时收集合法用户的良性交互数据，为安全-效用分析提供对照。
- **数据产出**：279k 条提示攻击数据，以及配套的良性用户数据。

## 3. 实验设计
### 3.1 数据集与场景
- **攻击数据**：通过 Gandalf 平台收集的 279k 自适应提示攻击，覆盖多种攻击模式（如越狱、注入、角色扮演等）。
- **效应对照数据**：收集的良性用户请求，模拟真实应用环境中的正常交互。
- **应用场景**：论文提到“受限应用域（restricted application domains）”和“纵深防御（defense-in-depth）”可作为安全策略，表明实验覆盖了不同场景设定（如领域限定、多层防御组合）。

### 3.2 评价基准与对比方法
- **主要基准**：自身构建的安全-效用权衡曲线，而非单一安全指标。
- **对比对象**：
  - 不同防御策略（如系统级提示、输入过滤、输出监控等）在安全性与可用性上的表现。
  - 文内提到现有防御集成在 LLM 内部（如 system prompts）即使不直接拒绝请求，也可能降低可用性，暗示与不受限的基准响应质量对比。
- **核心评估指标**：
  - 安全维度：攻击成功率、防御绕过难度。
  - 效用维度：合法用户受到的干扰程度（如响应准确性、相关性下降）。

## 4. 资源与算力
- **论文未明确说明**所使用的 GPU 型号、数量或训练时长。由于工作重点为威胁建模、平台构建与数据分析，而非大规模模型训练，推测算力需求主要来自多次 LLM 推理（用于分类攻击/合法、评估响应质量），但具体硬件资源未公开。

## 5. 实验数量与充分性
- **实验规模**：
  - 基于 279k 条攻击提示的大型数据集，结合良性用户数据进行分析，覆盖大量攻防交互。
  - 文中提及分析揭示了防御策略对可用性的影响，并验证了三种有效策略（受限域、纵深防御、自适应防御），可合理推断进行了多组对比实验。
- **充分性评价**：
  - **充分性**：在安全-效用联合分析层面，拥有大规模、高真实性的自适应攻击数据，能有力支撑主要结论。
  - **客观性与公平性**：采用众包方式收集攻击数据，降低了实验室先验偏差；将防御策略与无防御或不同防御进行横向比较；同时考察安全性和可用性，避免单维度评价的片面性。
  - **潜在局限**：实验范围可能受限于 Gandalf 平台特定的游戏设定，攻击者行为是否完全迁移到真实 LLM 应用尚需外部验证。

## 6. 主要结论与发现
- **安全-效用不可分割**：内置于 LLM 的防御（如精心设计的系统提示）即使不直接拦截请求，也会显著降低合法用户的体验质量。
- **自适应攻击的危害**：静态防御在动态攻击面前更加脆弱，攻击者能逐步绕过防御。
- **有效策略识别**：
  - **受限应用域**：限制 LLM 的功能范围可从根本上缩小攻击面。
  - **纵深防御**：组合多层防御可提高整体安全性，但需注意对效用的叠加影响。
  - **自适应防御**：能根据攻击行为动态调整的防御机制，更有可能同时兼顾安全与效用。
- **平台价值**：Gandalf 平台为生成真实的、规模化的自适应攻击数据提供了可行方法论，填补了当前评估生态的空白。

## 7. 优点与亮点
- **创新的威胁模型**：D-SEC 将攻击动态性和合法用户效用显式纳入同一框架，超越传统单目标安全评估。
- **高真实性数据集**：通过游戏化众包获得 279k 条自适应攻击，具有黑盒、多轮、持续进化的特点，更贴近真实威胁。
- **安全与可用性协同分析**：首次在大规模实验中定量展示内建防御对可用性的损害，指导实践者做出更均衡的设计选择。
- **开放资源**：论文表明会公开数据集和平台细节，有助于社区复现和推进研究。

## 8. 不足与局限
- **算力细节缺失**：未报告计算资源使用情况，在推理成本敏感的应用中，参考价值受限。
- **平台依赖偏差**：攻击数据源于特定游戏化环境，攻击者动机和策略可能与真实恶意对手存在差异，外部效度需进一步验证。
- **效用度量的单一性**：文中主要关注防御对合法用户造成的响应质量下降，其他维度（如延迟、吞吐、用户信任）未充分展开。
- **防御种类有限**：尽管验证了几种策略，但未覆盖所有前沿防御技术（如对抗性训练、可解释性干预等），框架的普适性有待更多方法检验。
- **动态模型的黑盒假设**：论文侧重攻击者无法获知防御细节的场景，对灰盒/白盒攻击的评估可能不足。

（完）
