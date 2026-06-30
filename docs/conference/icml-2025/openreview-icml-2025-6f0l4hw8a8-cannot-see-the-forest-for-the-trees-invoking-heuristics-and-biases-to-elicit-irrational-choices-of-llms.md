---
title: "Cannot See the Forest for the Trees: Invoking Heuristics and Biases to Elicit Irrational Choices of LLMs"
title_zh: 只见树木不见森林：调用启发式与偏误以诱发大语言模型的非理性选择
authors: "Haoming Yang, Ke Ma, Xiaojun Jia, Yingfei Sun, Qianqian Xu, Qingming Huang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=6F0L4HW8a8"
tags: ["query:priv-sec"]
score: 9.0
evidence: 利用启发式与认知偏误的越狱攻击
tldr: 现有越狱攻击多依赖暴力优化或手工设计，未充分利用人类认知弱点。本文受启发式与偏误启发，提出 ICRT 攻击框架，通过认知分解降低恶意提示复杂性，并利用相关性偏误重组提示以增强语义对齐，从而诱发生成有害内容。实验表明该方法能有效突破多款 LLM 的安全防线。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 需要揭示现实场景中 LLM 可能面临的认知漏洞，而非仅依赖优化式攻击。
method: 提出 ICRT，结合简洁效应进行认知分解，利用相关性偏误重构恶意提示。
result: ICRT 在多个模型上成功越狱，揭示了认知偏误可被武器化。
conclusion: LLM 安全对齐需考虑人类认知偏误带来的新型攻击面。
---

## Abstract
Despite the remarkable performance of Large Language Models (\textbf{LLMs}), they remain vulnerable to jailbreak attacks, which can compromise their safety mechanisms. Existing studies often rely on brute-force optimization or manual design, failing to uncover potential risks in real-world scenarios. To address this, we propose a novel jailbreak attack framework, \textbf{ICRT}, inspired by heuristics and biases in human cognition. Leveraging the \textit{simplicity effect}, we employ \textit{cognitive decomposition} to reduce the complexity of malicious prompts. Simultaneously, \textit{relevance bias} is utilized to reorganize prompts, enhancing semantic alignment and inducing harmful outputs effectively. Furthermore, we introduce a ranking-based harmfulness evaluation metric that surpasses the traditional binary success-or-failure paradigm by employing ranking aggregation methods such as Elo, HodgeRank, and Rank Centrality to comprehensively quantify the harmfulness of generated content. Experimental results show that our approach consistently bypasses mainstream \textbf{LLMs}' safety mechanisms and generates high-risk content.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
*   **核心问题**：当前大语言模型（LLMs）在安全对齐后仍易受越狱攻击（Jailbreak Attack）。现有攻击多依赖暴力优化（brute-force optimization）或手工设计，未能充分挖掘现实场景中基于人类认知弱点的潜在风险。
*   **研究动机**：揭示 LLMs 在真实交互中可能面临的认知漏洞，而不仅仅是展示优化驱动的攻击成功。论文受人类启发式思维与认知偏误（Heuristics and Biases）启发，试图通过调用这些认知捷径来诱发模型的非理性、有害输出。
*   **整体含义**：该工作提出了一个全新的攻击框架，从认知心理学角度拓展了 LLM 安全威胁面，强调安全对齐必须考虑认知偏误被武器化的风险。

### 2. 论文提出的方法论
*   **攻击框架名称**：ICRT（Influencing Cognitive biases for Jailbreak）。
*   **核心思想**：借鉴人类决策中的两类认知偏差——简洁效应（Simplicity Effect）和相关性偏误（Relevance Bias）。
*   **关键技术细节**：
    *   **认知分解（Cognitive Decomposition）**：利用简洁效应，将原本语义复杂、可能触发安全过滤的恶意提示，拆解或转换为更简单、看似无害的子结构，降低其感知复杂度。
    *   **相关性偏误重组**：利用人类倾向于基于表面相关而非严格逻辑关联进行判断的偏好，对分解后的提示进行重组，使其在语义上与无害上下文产生“伪相关”，从而骗过模型的安全对齐机制，诱发生成有害内容而模型不易察觉。
    *   **输出危害性评估**：引入**基于排序的危害性度量指标**，超越传统二元成功/失败判定。采用排名聚合方法（如 Elo 系统、HodgeRank、Rank Centrality）全面量化生成内容的危害程度。
*   **算法流程**：（文中未给出详细伪代码）整体流程可概括为：原始恶意输入 → 认知分解降低复杂度 → 基于相关性偏误重组提示 → 输入 LLM → 获得生成结果 → 用排序聚合方法评估危害等级。

### 3. 实验设计
*   **数据集/场景**：通过设计的认知越狱攻击生成高风险内容，具体数据集在摘要中未列明，但从上下文推断为覆盖主流安全测试场景的恶意提示集。
*   **Benchmark**：对比对象为现有的越狱攻击方法（如暴力优化类和手工设计类攻击），但具体名称暂未提供。
*   **评估指标**：除传统的越狱成功率外，还使用了提出的基于 Elo、HodgeRank、Rank Centrality 的排序聚合危害度指标，以更细粒度地衡量攻击效果。

### 4. 资源与算力
*   在给定的元数据及摘要中，**没有明确提及**所使用的 GPU 型号、数量、训练时长或任何算力相关信息。由于这是一项攻击方法研究而非大模型训练，其攻击过程可能推理消耗较少，但在摘要和元数据段无法确认。

### 5. 实验数量与充分性
*   **实验组数量**：摘要与元数据未详细列出消融实验或不同场景的具体数量，但显示出实验设计具有多维度性：多款主流 LLM 上的攻击验证、不同攻击方法对比、以及引入排名聚合指标后的细粒度评估。
*   **客观与公平性**：使用了 ELo、HodgeRank 等较客观的排序聚合方法，显著提高了评估的科学性，超越了简单分类。基于已有信息判断，实验设计及指标较为充分，但具体实验规模和消融细节需看全文。

### 6. 论文的主要结论与发现
*   ICRT 攻击框架可以稳定绕过多个主流 LLM 的内置安全机制。
*   生成的内容具有高风险性，且传统二元判断不足以衡量其危害，需要更细粒度的排序评估。
*   揭示了 LLM 安全领域的一个重要方向：**对 LLM 的防护必须纳入对人类认知偏误的考虑**，这是一个新的攻击面。

### 7. 优点
*   **视角新颖**：首次将人类认知启发式与偏误系统性地转化为越狱攻击武器，为红队测试提供了全新工具。
*   **方法优雅**：认知分解与相关性偏误重组的设计不依赖高强度暴力搜索，攻击路径更简洁而隐蔽。
*   **评估方法先进**：引入排序聚合指标进行危害性度量，比传统的成功率更具解释性和区分度（例如能够区分“极危险”与“略微有害”的输出）。
*   **潜在价值高**：被 ICML 2025 接收，表明该方法学贡献和安全性发现的认可度高。

### 8. 不足与局限
*   **细节未知**：由于目前仅提供元数据与摘要，具体技术实现、提示模板、重组算法、实验所用模型清单、消融实验覆盖以及攻击效果的精确数值均缺失，难以评估其可复现性与泛化能力。
*   **防御对策未讨论**：摘要未提及是否探讨了基于该攻击的防御加固方法。
*   **潜在偏差风险**：“相关性偏误”的利用可能对某些特定类型的安全话题更有效，在其他安全场景下的覆盖度有待验证。
*   **应用限制**：该攻击假设攻击者能细致地进行认知层面的提示工程，而这种能力本身有较高门槛，大规模自动化攻击的稳定性还未可知。

（完）
