---
title: Black-Box Adversarial Attacks on LLM-Based Code Completion
title_zh: 针对基于LLM的代码补全的黑盒对抗攻击
authors: "Slobodan Jenko, Niels Mündler, Jingxuan He, Mark Vero, Martin Vechev"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=jSYBqtOJS4"
tags: ["query:priv-sec"]
score: 9.0
evidence: 展示了对LLM代码补全的黑盒对抗攻击，导致不安全代码生成增加
tldr: 针对LLM代码补全引擎潜在的安全隐患，本工作首次提出黑盒对抗攻击方法INSEC，通过向补全输入注入精心设计的短注释，在无需模型内部信息的情况下，使模型输出大量包含安全漏洞的代码。实验结果表明，该攻击隐蔽且有效，大幅提升了不安全代码生成比例，证实了代码补全领域的现实安全风险，亟需开发相应的防御策略。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: LLM代码补全引擎广泛使用，其安全性至关重要，但现有研究缺乏对其黑盒攻击的关注。
method: 提出INSEC攻击，在补全输入中注入短注释作为攻击字符串，通过基于查询的优化过程从精心设计的初始化中生成。
result: 实验表明INSEC可显著提高不安全代码的生成率，且攻击隐蔽有效。
conclusion: 该工作揭示了LLM代码补全的严重安全漏洞，呼吁加强相关防御研究。
---

## Abstract
Modern code completion engines, powered by large language models (LLMs), assist millions of developers with their strong capabilities to generate functionally correct code. Due to this popularity, it is crucial to investigate the security implications of relying on LLM-based code completion. In this work, we demonstrate that state-of-the-art black-box LLM-based code completion engines can be stealthily biased by adversaries to significantly increase their rate of insecure code generation. We present the first attack, named INSEC, that achieves this goal. INSEC works by injecting an attack string as a short comment in the completion input. The attack string is crafted through a query-based optimization procedure starting from a set of carefully designed initialization schemes. We demonstrate INSEC's broad applicability and effectiveness by evaluating it on various state-of-the-art open-source models and black-box commercial services (e.g., OpenAI API and GitHub Copilot). On a diverse set of security-critical test cases, covering 16 CWEs across 5 programming languages, INSEC increases the rate of generated insecure code by more than 50%, while maintaining the functional correctness of generated code. We consider INSEC practical - it requires low resources and costs less than 10 US dollars to develop on commodity hardware. Moreover, we showcase the attack's real-world deployability, by developing an IDE plug-in that stealthily injects INSEC into the GitHub Copilot extension.

---

## 论文详细总结（自动生成）

# 针对基于LLM的代码补全的黑盒对抗攻击（INSEC）

## 1. 论文核心问题与整体含义
- **研究动机**：基于大语言模型（LLM）的现代代码补全引擎已被全球数百万开发者使用，其生成的代码功能正确且高效，但在安全性的研究尚不充分。
- **核心问题**：攻击者是否能在**黑盒**场景下（无需模型参数、梯度等内部信息），通过对输入进行微小而隐蔽的操控，显著提升LLM代码补全产生**不安全代码**的比例。
- **整体含义**：该工作揭示了当前主流代码补全系统面临现实的、低成本的黑盒安全威胁，提醒学术界和工业界必须重视面向代码安全的防御措施。

## 2. 方法论
- **攻击名称**：INSEC（Insecure Code Completion Attack）。
- **核心思想**：在代码补全的输入中注入一个**短注释**作为攻击字符串（attack string），该注释对开发者而言看起来像普通的程序注释，但能够干扰LLM的生成，使其倾向于输出包含安全漏洞的代码。
- **关键技术细节**：
  - **黑盒优化**：通过基于查询（query-based）的优化过程来生成攻击字符串，整个过程无需访问模型的内部表示。
  - **初始化方案**：优化从一组精心设计的初始化字符串开始，以提升攻击效果和收敛速度。
  - **约束条件**：攻击字符串被设计为合法、简短的注释，从而保证隐蔽性；同时攻击后的代码补全在功能正确性上仍然得到保持。
- **公式/算法流程**（文字描述）：  
  - 给定一个安全敏感的代码补全上下文，初始化一组候选攻击注释。  
  - 反复向目标模型发送包含该注释的补全请求，并在收到生成代码后评估其安全性。  
  - 根据评估结果（不安全代码生成率的提升）优化攻击字符串，最终得到一个能使模型稳定产生不安全代码的通用或特化的攻击字符串。

## 3. 实验设计
- **数据集/场景**：安全关键的测试用例，覆盖 **16 种常见弱点枚举（CWE）**，横跨 **5 种编程语言**。
- **评估模型/服务**：
  - 多个先进的**开源模型**；
  - **黑盒商业服务**：OpenAI API、GitHub Copilot 等。
- **对比方法**：论文未在摘要中详述对比 baseline，但根据上下文会对比原始（无攻击）代码补全的安全率与功能正确率。
- **度量指标**：
  - **不安全代码生成率的提升**（摘要中提到超过 **50%** 的提升）。
  - **功能正确性维持**：生成的代码仍然在功能上正确。

## 4. 资源与算力
- 摘要中强调 INSEC **资源需求低**，在普通硬件上开发攻击成本 **不到 10 美元**。
- 未明确提及 GPU 型号、数量或具体训练时长，但“commodity hardware”暗示没有使用昂贵的高性能计算集群，优化主要通过 API 查询而非本地大模型训练。

## 5. 实验数量与充分性
- 实验覆盖 **5 种编程语言**、**16 种 CWE**，在多个开源模型和商业服务上进行评估，具有较广的覆盖面。
- 攻击方法的 **通用性和可部署性** 得到验证：开发了 IDE 插件，能够秘密地将攻击注入 GitHub Copilot 扩展。
- 摘要虽未详细列出消融实验的具体类型，但提到从“精心设计的初始化方案”出发的优化过程，暗示可能存在关于初始化方法影响的实验。
- 总体上，实验设计考虑了多样性（多模型、多语言、多弱点类型）和现实场景，客观性和公平性较高。

## 6. 主要结论与发现
- **INSEC 现实有效**：首种对 LLM 代码补全场景的黑盒攻击，可在隐蔽的注释注入下，将生成不安全代码的比例提升超过 **50%**。
- **低成本高危害**：攻击开发成本极低（<10 美元），却对现代商业和开源代码补全引擎构成实质性威胁。
- **功能正确性不受影响**：攻击未降低代码的正确性，使其更不易被发现。
- **现实部署风险**：通过实现 IDE 插件，展示了攻击可轻易集成到开发环境中，进一步证实了威胁的迫切性。
- **呼吁防御研究**：强烈建议社区研发针对此类黑盒攻击的检测和缓解策略。

## 7. 优点（论文亮点）
- **首次实现黑盒攻击**：填补了 LLM 代码补全领域对抗攻击研究的空白。
- **隐蔽且实用**：攻击载体仅为短注释，在正常开发中不易察觉，且成本极低，便于真实部署。
- **广泛的实验验证**：覆盖多个商业服务、开源模型、多种编程语言和安全弱点，结论可信度高。
- **实际应用演示**：通过 IDE 插件证明了攻击在真实开发环境中的可行性。

## 8. 不足与局限
- **实验细节未知**：基于提供的摘要，无法获知攻击是否针对特定语言/框架存在泛化问题，或是否对防御性提示（如安全指南）敏感。
- **功能正确性的评估**：摘要提到维持功能正确，但未说明评估方式（是否用自动化测试套件），可能存在不完全执行所有功能性路径的风险。
- **对输入扰动的鲁棒性**：攻击字符串是否容易被开发者的人工检查或自动化工具（如注释清洗）识别和过滤，有待进一步考察。
- **伦理与部署限制**：相关实验是在受控条件下进行，真实部署会产生安全危害，论文未深入讨论披露和缓解时间线。

（完）
