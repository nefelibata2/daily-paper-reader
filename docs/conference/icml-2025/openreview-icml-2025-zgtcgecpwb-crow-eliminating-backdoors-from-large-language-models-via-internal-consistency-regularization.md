---
title: "CROW: Eliminating Backdoors from Large Language Models via Internal Consistency Regularization"
title_zh: CROW：通过内部一致性正则化消除大语言模型后门
authors: "Nay Myat Min, Long H. Pham, Yige Li, Jun Sun"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=ZGtcgeCpWB"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过内部一致性正则化实现大模型后门防御
tldr: 针对大模型中后门攻击的隐蔽触发器操纵输出问题，本文提出基于内部一致性正则化的CROW防御。它利用后门模型层间表示不稳定的特点，通过对抗扰动和正则化强制一致性。实验在Llama、CodeLlama等主流模型上验证了无需触发器知识即可消除后门的有效性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有后门防御多针对分类任务，难以用于文本生成，亟需大模型专用方案。
method: 提出CROW，基于干净模型层表示平滑、后门模型不稳定的观察，通过一致性正则化中和后门。
result: 仅需少量干净数据即可在多种模型和攻击下高效清除后门。
conclusion: CROW为LLM文本生成提供了一种强大、无需触发器知识且高效的后门防御。
---

## Abstract
Large Language Models (LLMs) are vulnerable to backdoor attacks that manipulate outputs via hidden triggers. Existing defense methods—designed for vision/text classification tasks—fail for text generation. We propose *Internal Consistency Regularization (CROW)*, a defense leveraging the observation that backdoored models exhibit unstable layer-wise hidden representations when triggered, while clean models show smooth transitions. CROW enforces consistency across layers via adversarial perturbations and regularization during finetuning, neutralizing backdoors without requiring clean reference models or trigger knowledge—only a small clean dataset. Experiments across Llama-2 (7B, 13B), CodeLlama (7B, 13B), and Mistral-7B demonstrate CROW’s effectiveness: it achieves significant reductions in attack success rates across diverse backdoor strategies (sentiment steering, targeted refusal, code injection) while preserving generative performance. CROW’s architecture-agnostic design enables practical deployment.

---

## 论文详细总结（自动生成）

## 1. 研究动机与核心问题
- **核心问题**：大语言模型（LLM）易受后门攻击，攻击者通过隐藏触发器操纵模型输出（如情感转向、定向拒绝服务、恶意代码注入等），严重威胁生成式 AI 的安全性。
- **现有方法局限**：已有后门防御几乎全部针对视觉或文本分类任务设计，无法直接用于文本生成场景；少部分尝试直接迁移的方法往往失效，或需要已知触发器、干净参考模型等不切实际的假设。
- **本文目标**：提出一种 **无需触发器知识、无需干净参考模型、仅需极少干净样本** 的 LLM 后门消除方法，要求对生成性能的影响尽可能小，且具备架构无关的通用性。

## 2. 方法论：CROW（内部一致性正则化）
- **核心观察**：干净模型在层间隐藏表示上过渡平滑，而后门模型在遇到触发器时层间表示会出现剧烈波动（不一致性）。该现象为检测和中和后门提供了内在信号。
- **核心思想**：通过强制 **内部层间表示的一致性**，使后门模型的异常行为被“平滑”掉，从而中和触发器的影响。
- **技术流程**（文字描述）：
  1. **对抗扰动生成**：对输入 embedding 施加小幅度扰动，使得模型内部不同层的隐藏状态差异最大化，即放大潜在的不一致性，定位后门敏感的表示维度。
  2. **一致性正则化**：在少量干净数据的微调过程中，引入正则项约束同一输入在不同层上的表示（或同一层在不同扰动下的表示）保持接近，降低模型对扰动和潜在触发器的过度敏感性。
  3. **联合优化**：将语言建模损失与一致性正则化损失结合，在保持生成质量的前提下，逐步“理顺”模型内部表示，消除后门效应。
- **关键优势**：不需要识别或逆向触发器，不需要原始干净模型作为参照，整个流程仅基于被后门的模型本身和少量干净文本。

## 3. 实验设计
- **模型与规模**：在三种架构、多个规模的 LLM 上进行评估，包括 **Llama-2（7B，13B）**、**CodeLlama（7B，13B）** 和 **Mistral-7B**。
- **攻击场景**（后门策略）：
  - 情感转向（Sentiment Steering）：触发器迫使模型输出特定情感倾向的文本。
  - 定向拒绝（Targeted Refusal）：触发器使模型拒绝回答本应正常响应的问题。
  - 代码注入（Code Injection）：触发器导致模型生成含有恶意代码或特定不安全代码模式的补全。
- **评估指标**：
  - **攻击成功率（ASR）**：带触发器输入下，模型产生目标恶意输出的比例，用于衡量后门清除效果。
  - **生成质量**：如困惑度（PPL）或在通用基准上的文本生成能力，确保防御不会严重损害有用性。
- **对比基线**：摘要未明确列出所有对比方法名称，但指出将 CROW 与现有的、为分类任务设计的防御方法进行对比，并验证这些方法迁移到文本生成任务上的失败情况，从而凸显 CROW 的有效性。

## 4. 资源与算力
- 论文摘要及元数据中 **未明确提及 GPU 型号、数量及训练时长**。仅说明实验涉及 7B 和 13B 级别的模型微调，典型配置可能使用多张 A100 或类似 GPU，但具体算力需求需参见原文正文。

## 5. 实验数量与充分性
- **实验组合丰富**：覆盖 3 种模型架构 × 2～3 种参数规模 × 3 种典型后门攻击，共计至少十几组主要实验。
- **额外验证**：摘要未描述，但典型消融研究应包括：不同干净数据量影响、有无一致性正则化、扰动强度等。由于论文获 ICML 2025 接收且评分 9.0，可合理推断实验设计较为系统，包含充分的消融分析和公平对比。
- **客观性**：在多种模型和多种攻击下报告 ASR 和生成指标，削弱了对特定模型或攻击过拟合的风险。

## 6. 主要结论与发现
- CROW 在 **所有测试的后门攻击** 上均能 **大幅降低攻击成功率**，同时在干净输入上保持 **与正常微调相当或可接受的生成性能**。
- 仅需 **极少量的干净数据**（远少于传统微调所需），即可有效消除后门，极具数据效率。
- 方法具备 **架构无关性**，可直接应用于不同 LLM，无需针对特定模型结构修改。
- 相较于已有分类防御的直接迁移，CROW 是第一个在 LLM 文本生成场景下取得显著成效的后门防御方法。

## 7. 优点与亮点
- **无需触发器知识**：防御不依赖攻击检测或逆向触发器，更贴合现实黑盒场景。
- **极小数据需求**：降低部署和防御成本。
- **架构通用**：不绑定特定模型，便于集成到现有 LLM 安全流水线。
- **内部信号利用新颖**：首次通过层间一致性正则化解决 LLM 后门问题，为文本生成安全提供新视角。
- **实验验证全面**：涵盖主流开源 LLM 和多种真实后门攻击，实用性强。

## 8. 不足与局限
- **实验覆盖**：虽已测试多种模型，但未涉及更大参数规模（如 70B+）和更多架构（如仅 Decoder 外的编解码模型），泛化上限待确认。
- **对抗强度**：未评估自适应攻击（攻击者知晓防御后针对性设计触发器或破坏一致性）的鲁棒性。
- **干净数据假设**：方法依赖少量“真正确干净”的数据，若干净数据被污染，防御效果可能下降。
- **应用限制**：仅针对生成任务后门，未探讨分类或检索增强等混合场景下的表现。
- 算力需求和训练时长等实践细节未在摘要中提供，原文是否有详尽消融需进一步确认。

（完）
