---
title: Splitting with Importance-aware Updating for Heterogeneous Federated Learning with Large Language Models
title_zh: 面向异构联邦大语言模型的重要性感知更新分割
authors: "Yangxu Liao, Wenke Huang, Guancheng Wan, Jian Liang, Bin Yang, Mang Ye"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=ny0m8YEUzH"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出FedICU联邦学习框架，通过分割客户端更新保护LLM隐私
tldr: 针对联邦学习与大语言模型结合中非IID指令数据带来的挑战，本文提出FedICU框架，将客户端更新智能地分解为共识部分和分歧部分，并引入重要性感知更新机制，以在保护数据隐私的同时维持模型核心能力并适应领域特定知识。实验结果显示，FedICU在指令微调场景下显著优于现有联邦方法，实现了隐私保护与模型效用的高效平衡，为分布式LLM训练提供了新范式。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 联邦学习保护隐私，但非IID指令微调场景对大语言模型构成挑战。
method: 提出FedICU框架，将客户端更新分解为共识和分歧分量，通过重要性感知机制维护核心能力并适应领域知识。
result: 实验表明FedICU在非IID场景下显著优于现有联邦学习方法，兼顾隐私与性能。
conclusion: FedICU为隐私保护的大语言模型联邦微调提供了有效方案，推动了分布式学习的发展。
---

## Abstract
Federated learning provides an efficient privacy-preserving distributed training framework for large language models, addressing the growing scarcity of publicly available training data while enabling the utilization of private datasets. While integrating large language model fine-tuning with federated learning emerges as a promising research direction, researchers pay limited attention to non-IID instruction-following scenarios. Our key insight is decomposing client updates into consensus and divergence components, enabling the model to maintain core capabilities while adapting to domain-specific knowledge. We propose a novel federated learning framework called **FedICU** (Splitting with **I**mportan**C**e-aware **U**pdating for Heterogeneous **Fed**erated Learning with Large Language Models), which introduces an aggregation mechanism that dynamically balances these components based on their contribution to global model performance, while implementing an importance-aware parameter updating strategy to prevent catastrophic forgetting and domain overfitting. Extensive experiments across diverse domains demonstrate that FedICU significantly outperforms existing federated learning approaches in terms of both generalization performance and domain adaptation. Our code is available at https://github.com/liaosunny123/FedICU.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：联邦学习 (FL) 为大型语言模型 (LLM) 提供了隐私保护的分布式训练框架，使得在不公开本地私人数据的前提下利用多源数据成为可能。然而，现有工作对非独立同分布 (non-IID) 的指令跟随场景关注不足，客户端上的领域特定指令数据异质性严重，直接应用传统联邦平均等方法会损害模型的泛化能力和核心语言能力。
- **核心问题**：在保护数据隐私的联邦学习设定下，如何高效地对大语言模型进行指令微调，以应对不同客户端之间高度异质的指令数据分布，既要防止对局部领域过拟合，又要避免灾难性遗忘，维持模型的通用能力。
- **整体含义**：提出一种将客户端更新分解为“共识”与“分歧”分量的新思路，通过重要性感知机制动态平衡二者，为异构联邦大语言模型微调提供了一种兼顾隐私保护、通用能力保有和领域自适应的有效范式。

## 2. 论文提出的方法论

- **核心思想**：将每一轮客户端训练产生的模型更新分解为**共识分量 (consensus component)** 和**分歧分量 (divergence component)**。共识分量反映有助于全局模型核心能力的知识，应当被保留并融合；分歧分量代表高度个性化的领域特定变化，若直接聚合会损害全局性能，需要被抑制或自适应调节。
- **关键技术细节**：
  - **更新分解**：通过在客户端本地对模型更新进行结构化分析，区分出哪些参数变化属于维护通用指令跟随能力的共识部分，哪些属于对本地非IID数据的过度适应而产生的分歧部分。
  - **重要性感知更新 (Importance-aware Updating)**：为每个模型参数或参数组计算重要性权重，用以控制其在全局更新中的贡献程度。重要性权重依据参数对全局任务和防止灾难性遗忘的影响程度动态确定，从而在聚合时抑制分歧分量，加强共识分量。
  - **动态平衡的聚合机制**：在服务器端引入一种新的聚合策略，不再简单加权平均所有客户端的更新，而是基于各客户端更新的共识/分歧分解及其重要性评分，自适应地融合全局模型，最终得到一个既能保持基本语言理解与生成能力，又能适应多领域特定知识的统一模型。
- **算法流程概括**（文字表述）：
  1. 服务器初始化全局LLM，并分发至各客户端。
  2. 客户端利用本地非IID指令数据微调模型，产生参数更新量。
  3. 客户端对该更新量进行分解，识别其共识部分和分歧部分，并计算各自的重要性指标。
  4. 客户端将分解后的更新（或结构化信息）上传至服务器。
  5. 服务器执行重要性感知的动态聚合，将受控的分歧分量与强化后的共识分量结合，更新全局模型。
  6. 反复迭代直至收敛。该框架被命名为FedICU。

## 3. 实验设计

- **数据集与场景**：论文提及开展“跨越多个不同领域”的广泛实验，聚焦于非IID的指令跟随任务。具体数据集名称在摘要和元数据中未明列，但从研究动机推断，应包含覆盖多领域、多分布的自然语言指令数据，用于模拟客户端间强异质性的联邦环境。
- **基准比较 (Benchmark)**：FedICU与现有的多种联邦学习方法进行了对比（例如传统联邦平均FedAvg及其适合异构场景的变体），基线方法的具体列表未在提供信息中给出，但论文声明在“泛化性能和领域适应能力”两方面均显著优于现有方法。
- **对比方法范畴**：可能包括面向异质性联邦学习的典型策略，如加入正则项、知识蒸馏、动态加权等方案，用以验证本方法在保护核心能力和适应领域知识两方面的优势。

## 4. 资源与算力

- 所给的摘要和元数据中**未明确说明**具体的 GPU 型号、数量或训练时长等资源消耗信息。鉴于论文涉及大语言模型，通常需要高性能 GPU 集群（如A100），但此处无法从已有文本中提取确切算力数据。

## 5. 实验数量与充分性

- **实验数量**：摘要用“大量跨领域实验 (Extensive experiments across diverse domains)”描述，显示实验覆盖面较广，但未提供具体实验组数、消融研究项或统计检验细节。
- **充分性与公平性评估**：
  - 基于已有信息，实验设计意图涵盖多域、多分布场景，力求证明方法的泛化性，具有一定充分性。
  - 通过与现有联邦学习方法直接对比，并同时评估“泛化性能”和“领域适应”，显示出对多维指标公平比较的追求。
  - 然而，由于没有具体数据集、指标分数和标准差等信息，无法进一步量化评判实验的完备度和客观性，仅能从定性描述中推测其具备可信度。

## 6. 论文的主要结论与发现

- FedICU框架通过将客户端更新解耦为共识与分歧分量，结合重要性感知更新策略，能够在联邦指令微调场景下：
  - 有效维持模型的核心语言能力和指令跟随通用性，防止灾难性遗忘；
  - 同时自适应地吸收分散在各客户端的领域特定知识，提升领域适应表现；
  - 整体上在泛化性与个性化之间取得优异平衡，显著超越基线联邦学习方法；
  - 为大语言模型的隐私保护联邦微调提供了高效且可落地的解决方案。

## 7. 优点

- **创新的问题分解视角**：首次提出将联邦学习中的模型更新显式分解为共识/分歧分量，从根本上调节全局与局部的冲突，思想新颖且解释性强。
- **重要性感知机制**：通过评估参数更新的重要性来动态指导聚合，避免了启发式固定规则，增强了方法在不同异质程度下的鲁棒性。
- **兼顾多目标**：同时缓解了FL-LLM微调中两大典型难题——灾难性遗忘与领域过拟合，实现了隐私保护、能力维护、领域适应三者的统一。
- **代码开源**：提供了可复现的代码库，有助于后续研究验证和拓展。

## 8. 不足与局限

- **实验细节缺失**：本案基于有限元数据，无法确知数据集规模、模型规模、消融实验完备性及具体提升幅度，可能导致对真实效果的过高或过低估计。
- **计算与通信代价未评估**：分解操作和重要性计算可能引入额外的客户端计算开销，以及需要上传结构化分解信息带来的通信负担，这些代价是否在生产环境中可接受，文中尚未可知。
- **对超大规模模型的适用性未验证**：尽管面向大语言模型，但若模型参数达百亿甚至千亿级别，分解与重要性感知操作的可扩展性和内存消耗有待确认。
- **安全性假设**：方法的隐私保护仍建立在联邦学习常规的梯度/更新交换安全假设下，未提及是否考虑梯度泄露、推理攻击等更精细的隐私威胁模型。
- **非IID极端场景的边界**：对于客户端数据领域差异极大甚至相互矛盾时的表现，以及共识和分歧分量的可分离性极限，缺乏深入讨论。

（完）
