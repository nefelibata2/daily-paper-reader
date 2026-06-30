---
title: How Much Can a Query Reveal? Structural Knowledge Stealing from Graph RAG via Traversal Reconstruction
title_zh: 查询能泄露多少？通过遍历重建从图RAG窃取结构知识
authors: "Jinze Gu, Qinghua Mao, Xi Lin, Jun Wu"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=QTKuEyRHaY"
tags: ["query:priv-sec"]
score: 9.0
evidence: 基于查询的图RAG结构知识窃取
tldr: 本文首次研究图RAG系统的隐私脆弱性，证明恶意查询可窃取大量结构知识，并设计了一种黑盒攻击策略，通过查询重建知识图谱的结构特征，揭露了此类系统存在的严重隐私风险。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 图RAG系统广泛应用但隐私影响未知，亟需评估其结构知识泄露风险。
method: 提出一种基于查询的高效攻击策略，在黑盒设置下通过遍历重建图结构。
result: 实验表明，攻击者能仅凭查询提取大量图谱结构信息，隐私风险显著。
conclusion: 研究揭示图RAG的固有隐私漏洞，呼吁加强安全防护设计。
---

## Abstract
Retrieval-Augmented Generation (RAG) has become a popular paradigm for enhancing large language models (LLMs) with external knowledge. Recent advances have extended this framework to structured data, leading to the emergence of Graph RAG systems that retrieve and reason over knowledge graphs. Despite their widespread applications, the privacy implications of such systems remain largely unexplored. In this work, we investigate a critical privacy vulnerability in Graph RAG systems: a significant portion of inherent structural knowledge can be easily exploited by malicious adversaries through carefully crafted queries, even under the black-box setting. We propose a query-based attack strategy that efficiently reconstructs knowledge graph including node-level and topology-level information, leveraging breadth-first traversal for untargeted attack and depth-first traversal for targeted attack. Experiments on generic and healthcare scenarios show that our method can recover over 90\% of the original knowledge graph from representative Graph RAG systems, exposing sensitive information with high fidelity. We further evaluate the efficacy of existing defense strategies and discuss primary challenges of safeguarding Graph RAG pipelines. To the best of our knowledge, this is the first systematic study of privacy risks in Graph RAG systems. Our findings underscore the urgent need for privacy-aware mechanisms in current graph retrieval-augmented AI systems.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：检索增强生成（RAG）已成为用外部知识增强大语言模型的主流范式，并逐渐扩展到结构化数据，出现了能够检索和推理知识图谱的 **Graph RAG 系统**。此类系统在医疗、金融等敏感领域应用广泛，但其隐私影响尚未被充分探索。
- **核心问题**：Graph RAG 系统在响应查询时，是否会不经意地泄露其所依赖的知识图谱的结构信息（节点、边等拓扑特征）？恶意用户能否通过**黑盒查询**大规模窃取这些敏感的结构知识？
- **整体含义**：本文首次系统性地揭示了 Graph RAG 系统面临的**固有隐私脆弱性**——攻击者即使仅能获取查询响应，也能高效重建底层知识图谱的大部分结构，从而暴露其中的敏感关联与实体信息。研究呼吁亟需为图检索增强 AI 系统设计隐私保护机制。

### 2. 论文提出的方法论
- **攻击设定**：黑盒攻击，攻击者仅能向 Graph RAG 系统发送查询并收到文本形式的回答，无法访问模型参数、检索过程或图谱本身。
- **核心思想**：利用 **遍历重建** 策略，通过精心设计的查询逐步探测图谱的节点及邻接关系，以图搜索的方式还原完整结构。
- **关键技术细节**：
  - **无目标攻击**：采用 **广度优先遍历（BFS）**。从某些初始节点出发，每轮查询识别当前节点的所有邻居，然后向未访问节点扩展，直至遍历全图。
  - **目标攻击**：采用 **深度优先遍历（DFS）**。针对特定目标节点或路径，沿着感兴趣的方向深入探测，重点恢复与目标高度相关的局部子图。
  - **查询构造**：攻击者将图谱探索需求转化为自然语言问题，例如询问“实体 X 与哪些实体有关联？”或“从 X 出发的路径有哪些？”，从系统回答中解析出节点名称与关系类型，逐步拼接拓扑结构。
- **攻击流程**：初始化节点集合 → 生成探测查询 → 提取响应中的实体/关系 → 更新已重建图谱 → 选择下一批待探测节点（依据 BFS/DFS 策略），直至达到预算或图谱稳定。

### 3. 实验设计
- **数据集/场景**：
  - **通用场景**：未具体具名（摘要提及“generic scenarios”），可能采用公开知识图谱或百科类图谱。
  - **医疗场景**：医疗领域的知识图谱，包含敏感的疾病、药物、患者关联等信息。
- **测试平台**：在**代表性 Graph RAG 系统**上进行评估，摘要未列出具体系统名称（推测为当前主流框架如 Graph-LLM 融合系统）。
- **对比方法**：
  - 主要对比自身攻击策略的不同变体（BFS vs. DFS，有目标 vs. 无目标）。
  - 评估现有**防御策略**的效力，这些防御策略作为对比基线，用于衡量攻击的鲁棒性。
- **评估指标**：以**原始知识图谱的恢复比例**（节点和边层面）作为核心衡量，报告“恢复超过90%的原始知识图谱”。

### 4. 资源与算力
- 摘要及提供的元数据中**未明确说明**所使用的 GPU 型号、数量、训练时长或查询攻击所耗费的具体算力资源。因攻击主要基于查询交互而非大规模模型训练，算力需求可能较低，但论文若涉及防御策略的再训练或 Graph RAG 系统本身的部署，具体资源消耗有待全文披露。

### 5. 实验数量与充分性
- **实验组数推测**：至少涵盖：
  - 2 种攻击类型（无目标 BFS、目标 DFS）× 2 个场景（通用、医疗）。
  - 针对防御策略的有效性评估实验。
  - 可能包含不同查询预算、不同图规模、不同系统配置下的消融实验。
- **充分性与公平性**：从摘要看，实验覆盖了多场景和对比维度，并能达到 90% 以上的恢复率，说明攻击有效性得到充分验证。对比部分包含了现有防御，体现了公平比较。但具体细节（如重复次数、统计显著性）需看全文，目前信息不足以判断彻底充分性。

### 6. 论文的主要结论与发现
- Graph RAG 系统存在**严重隐私漏洞**：恶意查询可大规模窃取图谱的结构知识。
- 提出的基于遍历的攻击策略高效且隐蔽：在通用和医疗场景中，可从多个代表性系统中恢复**超过 90% 的原始知识图谱节点和拓扑信息**，以高保真度暴露敏感实体与关系。
- 现有防御策略效果有限，保护 Graph RAG 管道仍面临**核心挑战**，须从头设计隐私感知机制。
- 这是**首个对 Graph RAG 系统隐私风险的系统性研究**，为后续安全设计敲响警钟。

### 7. 优点
- **首发性与新颖性**：首次定义并系统探究 Graph RAG 的结构知识窃取问题，填补了该领域的空白。
- **攻击方法设计巧妙**：仅通过黑盒查询和常规文本响应，利用图遍历思想重建图谱，无需任何模型内部信息，展示出高实用性。
- **双模式攻击**：无目标 BFS 与目标 DFS 兼顾全面窃取与定向挖掘，攻击粒度和灵活性突出。
- **实验有说服力**：高恢复率（>90%）和场景多样性（包含医疗等敏感领域）有力证明了威胁的严重性。
- **关注防御**：不仅揭露漏洞，还评估了现有防御的不足，指明了未来研究方向。

### 8. 不足与局限
- **对 Graph RAG 系统接口的依赖**：攻击成功依赖于系统能如实返回完整的邻接信息或详细路径。若系统对回答进行截断或模糊化，恢复率可能下降，这种情形在摘要中未充分探讨。
- **查询开销未详细说明**：90% 恢复率所需查询次数、时间成本未知，可能在实际中引发速率限制或异常检测。
- **防御评估范围不明**：摘要仅提“评估现有防御策略”，未指明具体是哪些防御（如输入净化、回答脱敏、图谱差分隐私等），其效果和迁移性有待扩展。
- **实验生态可能受限**：仅测试了“代表性 Graph RAG 系统”，不确定对其他架构（如紧耦合的图神经网络+LLM）的泛化能力。
- **对抗性防御响应下的鲁棒性**：现实系统可能部署动态防御，例如检测并阻断遍历式查询，论文可能未深入模拟此类自适应防御。

（完）
