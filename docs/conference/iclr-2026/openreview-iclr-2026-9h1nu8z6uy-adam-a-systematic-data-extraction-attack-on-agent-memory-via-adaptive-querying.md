---
title: "ADAM: A Systematic Data Extraction Attack on Agent Memory via Adaptive Querying"
title_zh: ADAM：通过自适应查询对智能体记忆的系统性数据窃取攻击
authors: "XINGYU LYU, Jianfeng He, Ning Wang, Yidan Hu, Tao Li, DANJUE CHEN, Shixiong Li, Yimin Chen"
date: 2025-09-14
pdf: "https://openreview.net/pdf?id=9H1nu8Z6Uy"
tags: ["query:priv-sec"]
score: 10.0
evidence: ADAM：通过自适应查询对LLM智能体记忆的数据提取攻击
tldr: 本文提出ADAM攻击方法，通过数据分布估计和自适应查询，从配备记忆模块或RAG机制的大语言模型智能体中系统性地提取敏感信息。实验表明，该攻击显著提高了数据窃取成功率，揭示了智能体记忆功能带来的严重隐私漏洞。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: LLM智能体引入记忆/RAG机制后存在隐私泄露风险，现有攻击成功率低。
method: 估计目标记忆数据分布，自适应生成查询以提取敏感信息。
result: ADAM将攻击成功率大幅提升，系统性暴露了智能体记忆的隐私漏洞。
conclusion: LLM智能体记忆功能亟待加强隐私防护。
---

## Abstract
Large Language Model (LLM) agents have achieved rapid adoption and demonstrated remarkable capabilities across a wide range of applications. To improve reasoning and task execution, modern LLM agents would incorporate memory modules or retrieval-augmented generation (RAG) mechanisms, enabling them to further leverage prior interactions or external knowledge. However, such a design also introduces a group of critical privacy vulnerabilities: sensitive information stored in memory can be leaked through query-based attacks. Although feasible, existing attacks often achieve only limited performance, with low attack success rates (ASR). In this paper, we propose ADAM, a novel privacy attack that features data distribution estimation of a victim agent’s memory and employs an entropy-guided query strategy for maximizing privacy leakage. Extensive experiments demonstrate that our attack substantially outperforms state-of-the-art ones, achieving up to 100% ASRs. These results thus underscore the urgent need for robust privacy-preserving methods for current LLM agents. Our code is available at: https://anonymous.4open.science/r/agent-privacy-attack-iclr/.

---

## 论文详细总结（自动生成）

ADAM：通过自适应查询对智能体记忆的系统性数据窃取攻击

### 1. 论文的核心问题与整体含义
*   **研究背景**：大型语言模型（LLM）驱动的智能体已获得广泛应用。为提升推理与任务执行能力，现代智能体普遍集成“记忆模块”或“检索增强生成”（RAG），以利用先前的交互记录或外部知识。
*   **核心问题**：这种记忆机制在增强性能的同时，也引入了严重的隐私漏洞。攻击者可通过发送恶意查询来提取存储在智能体记忆中的敏感信息。
*   **研究动机**：虽然现有攻击证实了此威胁的存在，但其攻击成功率普遍较低。因此，本研究旨在探索一种更高效、更具系统性的攻击方法，以揭示该漏洞的严重性。

### 2. 论文提出的方法论
*   **核心思想**：提出 **ADAM** 攻击框架，通过 **估计受害者智能体记忆的数据分布**，并利用 **熵引导的自适应查询策略**，来最大化隐私泄露程度。
*   **关键技术细节与流程**：
    *   **数据分布估计**：首先对目标智能体记忆模块中存储的数据进行类型推断和分布模型估计，了解攻击者可能获得的信息密度。
    *   **熵引导查询策略**：基于估计出的数据分布，计算查询的信息增益或不确定性（熵）。系统优先选择那些预期能减少最大不确定度、从而最直接“套取”出新敏感数据的查询，进行自适应迭代攻击。

### 3. 实验设计
*   **任务/场景**：设计为“数据窃取攻击”（Data Extraction Attack），即通过黑盒查询将智能体记忆中的某段特定完整信息逐字还原。
*   **对比方法**：将 ADAM 与现有 state-of-the-art 攻击方法进行了对比（摘要中未列出具体方法名，但强调了是“现有攻击”）。
*   **评估指标**：核心指标为**攻击成功率**。

### 4. 资源与算力
*   提供的摘要与元数据中**未提及**具体的算力资源详情（如 GPU 型号、数量、训练时长等）。因此，无法从现有材料中推断其算力消耗规模。

### 5. 实验数量与充分性
*   **实验量级**：论文摘要中提到进行了“广泛实验”（Extensive experiments）。
*   **充分性与客观性**：通过在多种设置下验证 ADAM 对攻击成功率的大幅提升效果（高达 100%），可以从一定程度上认为实验较为充分。由于直接对标现有先进方法并使用了硬性指标，具备基本的公平性和客观性。

### 6. 论文的主要结论与发现
*   **显著有效性**：ADAM 攻击方法大幅超越了 state-of-the-art 的攻击表现，攻击成功率最高可达 **100%**。
*   **风险警示**：实验结果系统性地暴露了当大模型智能体引入记忆功能后，所带来的极其严重的隐私漏洞。
*   **最终结论**：研究结果强调了为当前 LLM 智能体开发鲁棒的隐私保护机制的迫切性。

### 7. 优点
*   **创新性攻击视角**：提出基于熵引导的自适应查询策略，相比简单随机查询更具智能性和针对性。
*   **效果极其显著**：高达 100% 的攻击成功率非常有力地证明了漏洞的严重性和方法的优越性。
*   **直击核心安全痛点**：聚焦于工业落地广泛采用的记忆与 RAG 机制，研究成果对 AI 安全具有高度现实意义。

### 8. 不足与局限
*   **信息缺失**：提供的文本仅限于摘要和元数据，缺失具体实验配置（数据集、基准模型）、消融实验细节以及算力开销评估。
*   **防御策略缺失**：论文指出了防护的迫切性，但未对本领域提出具体的防御机制或缓解建议。
*   **真实应用场景的复杂性**：现有实验设定可能为受控环境，在面对真实世界智能体极其多样的记忆格式与内容时，100% 的攻击率在现实中可能需要进一步验证。

（完）
