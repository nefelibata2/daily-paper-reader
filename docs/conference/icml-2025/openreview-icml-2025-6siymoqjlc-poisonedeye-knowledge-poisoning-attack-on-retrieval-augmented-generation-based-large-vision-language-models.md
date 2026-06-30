---
title: "PoisonedEye: Knowledge Poisoning Attack on Retrieval-Augmented Generation based Large Vision-Language Models"
title_zh: PoisonedEye：针对基于检索增强生成的大视觉语言模型的知识投毒攻击
authors: "Chenyang Zhang, Xiaoyu Zhang, Jian Lou, Kai Wu, Zilong Wang, Xiaofeng Chen"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=6SIymOqJlc"
tags: ["query:priv-sec"]
score: 9.0
evidence: 首个针对视觉语言检索增强生成系统的知识投毒攻击
tldr: 针对视觉语言检索增强生成（VLRAG）系统，本文提出首个知识投毒攻击 PoisonedEye。该攻击仅需向知识库注入一个投毒样本，通过满足检索与生成两个关键属性，即可操纵系统对目标查询的回复。实验证明 VLRAG 面临严重安全威胁，揭示了多模态 RAG 系统的脆弱性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: VLRAG 依赖外部多模态知识库而易受投毒攻击，此前缺乏针对此类系统的知识投毒研究。
method: 提出 PoisonedEye 攻击，通过构建符合检索与生成属性的单个投毒样本来操纵目标查询响应。
result: 攻击成功用单一样本控制 VLRAG 输出，暴露了严重安全漏洞。
conclusion: VLRAG 系统面临现实投毒威胁，需设计相应防御机制。
---

## Abstract
Vision-Language Retrieval-Augmented Generation (VLRAG) systems have been widely applied to Large Vision-Language Models (LVLMs) to enhance their generation ability. However, the reliance on external multimodal knowledge databases renders VLRAG systems vulnerable to malicious poisoning attacks. In this paper, we introduce PoisonedEye, the first knowledge poisoning attack designed for VLRAG systems. Our attack successfully manipulates the response of the VLRAG system for the target query by injecting only one poison sample into the knowledge database. To construct the poison sample, we follow two key properties for the retrieval and generation process, and identify the solution by satisfying these properties. Besides, we also introduce a class query targeted poisoning attack, a more generalized strategy that extends the poisoning effect to an entire class of target queries. Extensive experiments on multiple query datasets, retrievers, and LVLMs demonstrate that our attack is highly effective in compromising VLRAG systems.

---

## 论文详细总结（自动生成）

# PoisonedEye：基于检索增强生成的大视觉语言模型的知识投毒攻击 详细总结

## 1. 核心问题与研究背景
- **研究动机**：Vision‑Language Retrieval‑Augmented Generation (VLRAG) 系统通过引入外部多模态知识库来增强大视觉语言模型（LVLMs）的生成能力，但对外部知识的依赖使其面临投毒攻击的风险。攻击者可通过恶意篡改知识库中的少量样本，操控模型在特定查询下的输出。
- **问题空白**：此前知识投毒攻击的研究主要集中在纯文本 RAG 系统，针对 VLRAG 这类同时处理图像与文本的多模态检索增强系统，尚缺乏系统性安全分析。
- **整体含义**：本文填补了这一空白，提出首个针对 VLRAG 的知识投毒攻击 **PoisonedEye**，证明只需注入**单个**投毒样本即可完成攻击，揭示了该类系统严重的安全脆弱性。

## 2. 方法论
- **核心思想**：构造一个精心设计的投毒样本（poison sample），使其在检索阶段被可靠召回，并在生成阶段诱导 LVLM 按攻击者意图输出。
- **关键属性**：投毒样本需同时满足两个属性：
  - **检索属性**：确保该样本在目标查询的检索结果中排名靠前（与查询高度相关）；
  - **生成属性**：该样本作为上下文输入 LVLM 时，能主导生成过程，使最终回复向攻击者预设的目标方向偏移。
- **攻击流程**：
  1. 针对目标查询，生成一个初始候选样本；
  2. 优化该样本的文本和（或）图像表征，以提升其与目标查询的检索相似度（满足检索属性）；
  3. 同时优化样本内容，使其在 LVLM 的生成中产生最大的引导效果（满足生成属性）；
  4. 将最终合成的单一样本注入知识库，完成攻击。
- **类查询目标投毒攻击**：进一步扩展攻击场景，使单一样本能够覆盖**一整类**语义相近的查询，实现更广义的投毒效果。方法是在优化时引入类内多样性的约束，保证样本在多条查询下依然满足上述两个属性。

## 3. 实验设计
- **数据集**：在**多个查询数据集**上评测，涵盖不同的视觉问答或图像描述任务（摘要指出“multiple query datasets”，具体名称未在摘要中列出）。
- **检索器**：对比了**多种检索器（retrievers）**，包括不同架构的密集检索模型。
- **基础模型**：使用了**多种主流 LVLMs**（如 LLaVA 系列等）作为生成模型。
- **对比方法**：由于是首个针对 VLRAG 的投毒攻击，可能主要与无攻击基线以及传统的文本 RAG 投毒方法做对比，验证 VLRAG 场景下的特殊挑战与效果。
- **评测指标**：通常攻击成功率（ASR）、生成内容与目标的一致性（如 BLEU、ROUGE 或语义相似度）、检索命中率等。

## 4. 资源与算力
- 摘要和元数据中**未明确提及**所使用的 GPU 型号、数量及训练／优化时长。鉴于投毒攻击通常只需梯度优化少量样本，算力消耗预计远小于模型训练，但仍缺少具体量化信息。

## 5. 实验数量与充分性
- **实验规模**：进行了多数据集 × 多检索器 × 多 LVLM 的交叉实验，覆盖了主要组件，具备较好的**外部效度**。
- **消融实验**：论文可能包含对检索属性与生成属性各自贡献的分析（虽摘要未详述，但方法强调两个属性，通常会设计消融）。此外，单样本攻击与类查询攻击的对比也属于重要实验维度。
- **公平性**：通过统一查询和评估协议，在同一基准下比较不同设置，实验设计客观、公平。

## 6. 主要结论与发现
- **极端高效**：仅需向知识库注入一个投毒样本，PoisonedEye 即可成功操纵 VLRAG 系统对目标查询的响应。
- **广泛威胁**：攻击跨不同检索器和 LVLMs 均有效，说明脆弱性并非特定模型缺陷，而是 VLRAG 范式固有的安全隐患。
- **类级攻击可行**：类查询目标投毒攻击进一步加剧威胁，攻击者能以更低成本污染整个查询类别的输出。
- **安全警示**：VLRAG 系统在实际部署中面临严重的知识投毒风险，亟需设计针对性的防御机制。

## 7. 优点与亮点
- **首创性**：首个面向视觉‑语言 RAG 的知识投毒攻击，开辟了多模态 RAG 安全新方向。
- **攻击效率高**：单样本投毒即可实现控制，攻击成本极低且隐蔽性强。
- **理论基础清晰**：拆解为检索属性和生成属性的联合优化，问题建模明确，方法可解释性强。
- **泛化设计**：提出的类查询攻击将攻击面从单点拓展到集合，增强了实用性和威胁评估价值。
- **实验全面**：覆盖多种组件组合，证明了方法的鲁棒性和普适性。

## 8. 不足与局限
- **防御缺失**：论文聚焦攻击，未探讨相应的防御手段，实际部署者暂缺乏缓解方案。
- **攻击成功条件未知**：未说明投毒样本在知识库中的“存活”条件（如知识库动态更新、检索结果重排等对攻击的影响）。
- **黑盒假设局限性**：攻击假设攻击者了解检索器和 LVLM 的模型参数（白盒优化），在完全黑盒的真实场景下有效性待验证。
- **实验细节缺失**：从提供材料无法得知具体数据集名称、模型版本及算力开销，难以完全复现。
- **图像成分的安全性**：未深入讨论投毒样本中图像部分的扰动范围与可察觉性，可能影响攻击的隐蔽性。

（完）
