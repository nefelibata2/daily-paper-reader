---
title: "Hidden No More: Attacking and Defending Private Third-Party LLM Inference"
title_zh: 无处隐藏：攻击与防御私有第三方LLM推理
authors: "Rahul Krishna Thomas, Louai Zahran, Erica Choi, Akilesh Potti, Micah Goldblum, Arka Pal"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=QfD9P9IIoz"
tags: ["query:priv-sec"]
score: 10.0
evidence: 从第三方LLM推理的隐藏状态中重构提示，并提出Cascade防御
tldr: 针对第三方LLM推理服务中隐藏状态可能泄露用户提示的隐私威胁，本文设计了一种新颖的攻击方法，能从隐藏状态中近乎完美地重构原始提示，并证明现有置换和噪声防御不足。为此，作者提出Cascade多层防御框架，通过组合防御机制有效降低重构攻击的成功率，为开放权重模型的隐私保护提供了实用解决方案，推动了安全LLM推理的发展。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 第三方LLM推理服务广泛使用，但其隐藏状态可能泄露用户提示，隐私风险严峻。
method: 提出一种新颖的重构攻击，从隐藏状态中以近乎完美的准确率恢复原始提示，并设计Cascade防御方案。
result: 攻击在多个SOTA模型上有效，且能绕过置换和噪声防御；Cascade防御显著降低攻击成功率。
conclusion: 该工作揭示了开放权重LLM的严重隐私漏洞，提出的Cascade防御为安全推理提供了新思路。
---

## Abstract
Recent advances in Large Language Models (LLMs) have led to widespread adoption of third-party inference services, raising critical privacy concerns. In this work, we introduce a novel reconstruction technique that can recover original prompts from hidden states with nearly perfect accuracy across multiple state-of-the-art LLMs in the increasingly important open-weights setting. Although the attack is conceptually simple, it has not  -- to the best of our knowledge -- previously been described nor shown to work practically. Furthermore, our attack remains effective against various permutation and noise-based defenses, challenging assumptions about the security of previously proposed schemes. To address these vulnerabilities, we propose Cascade, a multi-party inference scheme that leverages sharding in the sequence dimension to retain privacy of the user input. Through theoretical analysis and empirical evaluation, we demonstrate that Cascade is secure against both our attack as well as previous methods, while maintaining computational and communication efficiency. Our findings highlight the importance of rigorous security analysis in privacy-preserving LLM inference and offer practical solutions for secure deployment.

---

## 论文详细总结（自动生成）

# 论文总结：无处隐藏：攻击与防御私有第三方LLM推理

## 1. 核心问题与研究背景
- **核心问题**：第三方大语言模型（LLM）推理服务在提供便利的同时，其内部运算过程中产生的**隐藏状态（hidden states）** 可能被服务提供方或中间人截获，从而泄露用户的原始提示（prompts），构成严重隐私威胁。
- **整体含义**：这项工作聚焦于**开放权重（open-weights）模型**这一日益重要的现实场景，揭示了一个此前未被充分认识、且实际中可被利用的隐私漏洞，并给出了系统性的攻击验证与防御方案，为安全 LLM 推理部署提供了关键见解。

## 2. 方法论
### 核心思想
- 从模型的隐藏状态中**重构原始提示**。虽然攻击思路在概念上简单，但作者首次将其在多个先进 LLM 上实现到近乎完美的准确率，并证实其实际危害。
- 针对该攻击，提出防御框架 **Cascade**：一种多参与方推理方案，在**序列维度**上对计算进行分片（sharding），从而使任何单方无法掌握完整隐藏状态，从而保护用户输入隐私。

### 关键技术细节
- **攻击方法**：设计了一种新颖的提示重构技术，能够从模型内部隐藏状态直接恢复原始文本。论文指出攻击对多种**置换（permutation）和噪声（noise）类的防御**依然有效，推翻了此前关于这些防御方案安全性的假设。
- **防御方法**：Cascade 通过将序列维度的分片分配给不同计算节点，使每个节点仅接触到局部信息。结合理论分析与实验评估，证明 Cascade 既能有效抵御本论文提出的攻击，也能抵御已有攻击，同时保持可接受的计算与通信开销。

### 算法/公式说明
- 原文未提供详细公式或伪代码，但可概括为：攻击端利用隐藏状态与词表/嵌入空间的映射关系，通过优化或直接解码恢复提示；防御端通过分片策略打破隐藏状态的完整性，从信息论层面限制单点可获取的信息量。

## 3. 实验设计
- **数据集/场景**：由于论文原文未提供完整内容，具体使用的数据集和 benchmark 细节未知。但从元信息可推断，实验覆盖了多个最先进的开源 LLM，并在第三方推理的隐藏状态泄露威胁模型下进行评估。
- **对比方法**：攻击实验对比了不同模型上的重构准确率；防御实验对比了单一防御（如置换、加噪）与 Cascade 的抗攻击表现，证明了现有防御的不足以及 Cascade 的有效性。

## 4. 资源与算力
- **文中未明确说明**：提供的元数据及有限文本中没有提及 GPU 型号、数量、训练时长或推理算力消耗。该论文可能主要涉及推理阶段的攻击和模拟，算力需求相对可控，但无具体数据佐证。

## 5. 实验数量与充分性
- **估计实验组数**：由于信息不全，难以精确统计，但根据摘要可以预期包含以下实验维度：
  - 多个 SOTA LLM 上的攻击成功率评估；
  - 针对不同防御（置换、噪声等）的攻击鲁棒性验证；
  - Cascade 防御与其他防御的对比实验；
  - 计算与通信效率的测量。
- **充分性与公平性**：从研究立意和结论看，攻击方法的有效性经过了多模型验证，且防御方案有理论和实验双重支撑，实验设计在逻辑上足够充分和客观。但缺少具体指标和数据，无法深入评估。

## 6. 主要结论与发现
- 隐藏状态泄漏会导致**严重的隐私风险**，攻击者可以近乎完美地还原用户提示。
- 此前提出的置换、噪声等防御并不可靠，攻击仍能有效绕过。
- Cascade 多参与方推理方案通过序列维度的分片设计，从根源上限制了隐藏状态的泄露，能够显著降低重构攻击的成功率，同时保持效率。
- 研究强调了在隐私保护 LLM 推理中进行严格安全分析的必要性，并为开放权重模型的安全部署提供了可行路径。

## 7. 优点与亮点
- **揭示新威胁**：首次将隐藏状态提示重构攻击从理论变为现实，并展示了其强大威力，具有重要的警示意义。
- **打破旧防御**：用实验证明了现有简单防御（置换、噪声）的不安全性，刷新了社区对安全策略的认知。
- **实用防御方案**：Cascade 不依赖于单一技巧，而是通过多参与方架构在序列维度上进行根本性防护，兼具安全性与效率，具有较高实际部署潜力。
- **理论与实践结合**：工作包含理论分析和实验验证，论证严密。

## 8. 不足与局限
- **论文原文缺失**：本次分析基于元信息和摘要，无法深入评价实验细节、结果显著性以及结论的泛化性。
- **实验细节未明**：具体使用的模型列表、数据集、评估指标、统计显著性等关键信息无法获知，限制了对其严谨性的全面判断。
- **防御的适用性**：Cascade 依赖多参与方协作，在实际单点推理或非合作场景下可能难以直接部署，存在应用场景限制。
- **潜在偏差**：攻击和防御主要在开放权重模型上验证，对黑盒 API 或私有模型不一定成立；可能对特定模型架构和隐藏维度有隐含假设。

（完）
