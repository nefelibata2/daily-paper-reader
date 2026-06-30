---
title: "VeriGuard: Enhancing LLM Agent Safety via Verified Code Generation"
title_zh: VeriGuard：通过验证代码生成增强LLM代理安全
authors: "Lesly Miculicich, Mihir Parmar, Hamid Palangi, Krishnamurthy Dj Dvijotham, Mirko Montanari, Tomas Pfister, Long Le"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=SnEywLKodN"
tags: ["query:priv-sec"]
score: 9.0
evidence: 为医疗保健领域的LLM代理提供形式化安全保证，应对安全与隐私风险。
tldr: 自主AI代理在医疗等敏感领域部署面临安全与隐私风险。本文提出VeriGuard框架，通过离线验证和运行时约束的双阶段架构，为LLM代理的行为提供形式化安全保障，确保其遵守数据隐私政策。实验证明该方法能有效防止代理越权，为医疗AI安全提供可靠保障。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 医疗领域AI代理缺乏形式化安全保证，易引发隐私和安全问题。
method: 采用双阶段架构：离线意图澄清与安全约束制定，运行时强制执行验证。
result: 框架能有效防止代理违规行为，保障医疗数据隐私与安全。
conclusion: 形式化验证为敏感领域的LLM代理部署提供了可靠的安全机制。
---

## Abstract
The deployment of autonomous AI agents in sensitive domains, such as healthcare, introduces critical risks to safety, security, and privacy. These agents may deviate from user objectives, violate data handling policies, or be compromised by adversarial attacks. Mitigating these dangers necessitates a mechanism to formally guarantee that an agent's actions adhere to predefined safety constraints, a challenge that existing systems do not fully address.
We introduce \ours{}, a novel framework that provides formal safety guarantees for LLM-based agents through a dual-stage architecture designed for robust and verifiable correctness. The initial offline stage involves a comprehensive validation process. 
It begins by clarifying user intent to establish precise safety specifications. \ours{} then synthesizes a behavioral policy and subjects it to both extensive testing in simulated environments and rigorous formal verification to mathematically prove its compliance with these specifications. 
This iterative process refines the policy until it is deemed correct. Subsequently, the second stage provides online action monitoring, where \ours{} operates as a runtime monitor to validate each proposed agent action against the pre-verified policy before execution. This separation of the exhaustive offline validation from the lightweight online monitoring allows formal guarantees to be practically applied, providing a robust safeguard that substantially improves the trustworthiness of LLM agents in complex, real-world environments.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：自主AI代理（特别是基于大语言模型的代理）在医疗等敏感领域部署时，可能偏离用户意图、违反数据处理政策或遭受对抗攻击，引发安全、隐私和安保风险。现有系统缺乏**形式化安全保障**机制，无法在数学上证明代理的行为符合预定义的安全约束。
- **整体含义**：论文提出一种名为 **VeriGuard** 的框架，通过**离线验证+在线监控**的双阶段架构，为LLM代理提供**可验证的正确性**，从而实现可信赖的自主决策，尤其适用于医疗等高风险场景。

### 2. 论文提出的方法论

- **核心思想**：将严格的形式化验证与轻量级运行时监控解耦，使安全保证能够切实落地。离线阶段完成繁重的策略合成与证明，在线阶段仅需快速合规检查。
- **双阶段架构细节**：
  - **离线阶段（策略合成与验证）**
    1. **意图澄清与安全规范制定**：首先澄清用户真实意图，据此提炼出精确的**安全规范**（例如数据隐私政策的形式化描述）。
    2. **行为策略合成**：基于安全规范生成代理的行为策略。
    3. **测试与形式化验证**：在模拟环境中对策略进行大量测试，并采用**严格的形式化验证**方法，数学证明该策略是否完全符合安全规范。若未通过验证，则进行迭代优化，直到策略达到可证明的正确性。
  - **在线阶段（运行时监控）**
    - 将验证通过的策略部署为**运行时监控器**。
    - 在实际执行中，每当代理产生一个候选动作，VeriGuard 即对照已验证的策略进行合规性检查，仅允许满足约束的动作执行。
- **关键特性**：通过离线繁重、在线轻量的分工，使得形式化保证在现实复杂环境中具备实用价值。

### 3. 实验设计

- **应用场景**：摘要中特别强调医疗保健领域，实验很可能围绕医疗数据处理、患者隐私保护等任务展开。
- **Benchmark与对比方法**：
  - 由于原文仅提供摘要，未给出具体数据集和对比基准名称。但可推测实验会构建包含安全违规模拟的场景，评估代理在有无VeriGuard保护下的违规率，并可能对比仅靠提示工程、规则过滤等基线方法。
  - 对比维度可能包括：安全违规次数、策略执行成功率、运行时开销等。
  
### 4. 资源与算力

- **文中提及情况**：摘要及提供的元数据中**未明确说明**所使用的GPU型号、数量或训练时长。但离线阶段涉及形式化验证和模拟测试，通常需要一定算力支持；在线监控则设计为轻量级，对算力要求低。
- **补充说明**：具体算力信息需查阅论文正文，目前无法从已有信息中获取。

### 5. 实验数量与充分性

- **实验数量估计**：仅从摘要难以判断实验总量。但VeriGuard的设计包含多轮“迭代优化”，实验可能至少包含：
  - 不同安全规范下的策略验证成功率；
  - 多组违规场景测试（如不同攻击类型、策略违反方式）；
  - 消融实验（如移除形式化验证仅保留测试，或移除在线监控）。
- **充分性与客观性**：
  - 形式化验证本身提供数学保证，具有很强的客观性。
  - 如果实验覆盖了多种复杂场景并与多个基线对比，将能较好地支撑结论。但由于无法获取全文，实验的统计显著性、偏差控制等细节暂不可知。

### 6. 论文的主要结论与发现

- VeriGuard 能够通过双阶段架构**有效防止LLM代理的违规行为**，保障医疗数据隐私与整体系统安全。
- 将离线形式化验证与在线轻量级监控分离，使形式化安全保证在实际应用中成为可能，显著**提升了LLM代理在复杂、真实环境中的可信度**。
- 该方法为敏感领域（尤其是医疗）的自主代理部署提供了**可靠的安全机制**。

### 7. 优点

- **形式化保证**：不仅仅是经验性安全，提供了数学上的合规证明，理论可靠性强。
- **架构解耦**：繁重的验证离线进行，在线监控轻量，兼顾了严格性与实时性。
- **实用性强**：针对医疗等真实高风险场景设计，直接回应行业对AI代理安全的需求。
- **迭代优化机制**：策略若不达标会自动精化，保证了最终策略的正确性。

### 8. 不足与局限

- **实验细节缺失**：由于仅获取到摘要，无法评估实验的规模、多样性及对比公平性（例如是否考虑了不同LLM基座的影响）。
- **领域泛化性**：方法虽然声称适用于敏感领域，但实验可能主要集中于医疗，其他领域（如金融、法律）的适应性有待验证。
- **规范提取难度**：用户意图澄清并转化为形式化安全规范的过程可能依赖专家知识，实际应用中或面临成本高、易出错的问题。
- **对抗攻击覆盖**：摘要提及对抗攻击风险，但方法在复杂、自适应攻击下的鲁棒性未在可用信息中体现。
- **计算开销**：离线形式化验证的计算开销可能较大，对策略的规模和复杂度有限制；摘要未提及可扩展性分析。

（完）
