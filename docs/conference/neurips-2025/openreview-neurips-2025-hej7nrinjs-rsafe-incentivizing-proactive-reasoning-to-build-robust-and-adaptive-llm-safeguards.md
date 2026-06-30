---
title: "RSafe: Incentivizing proactive reasoning to build robust and adaptive  LLM safeguards"
title_zh: RSafe：通过激励主动推理构建鲁棒自适应的大语言模型安全防护
authors: "Jingnan Zheng, Xiangtian Ji, Yijun Lu, Chenhang Cui, Weixiang Zhao, Gelei Deng, Zhenkai Liang, An Zhang, Tat-Seng Chua"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=heJ7NRInjs"
tags: ["query:priv-sec"]
score: 9.0
evidence: 基于推理的防护模型，防御越狱攻击和分布外威胁
tldr: 现有大语言模型安全防护依赖大量人工标注数据，难以应对越狱攻击等分布外威胁。RSafe提出一种基于自适应安全推理的轻量级守卫模型，通过引导模型进行安全推理，在不依赖额外训练数据的情况下提供鲁棒防护。实验表明其有效抵御多种越狱攻击，并具备对新兴威胁的泛化能力。该工作为低成本、高适应性的LLM安全架构提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 大模型仍易受越狱攻击等分布外威胁，现有外部守卫模型依赖大量人工数据。
method: 提出RSafe框架，利用引导式安全推理构建自适应守卫模型，无需额外标注数据。
result: 在多种越狱攻击场景下实现高检测率，并展现出对新威胁的泛化能力。
conclusion: RSafe为部署灵活、人力成本低的大模型安全防护提供了有效新范式。
---

## Abstract
Large Language Models (LLMs) continue to exhibit vulnerabilities despite deliberate safety alignment efforts, posing significant risks to users and society. To safeguard against the risk of policy-violating content, system-level moderation via external guard models—designed to monitor LLM inputs and outputs and block potentially harmful content—has emerged as a prevalent mitigation strategy. Existing approaches of training guard models rely heavily on extensive human curated datasets and struggle with out-of-distribution threats, such as emerging harmful categories or jailbreak attacks. To address these limitations, we propose RSafe, an adaptive reasoning-based safeguard that conducts guided safety reasoning to provide robust protection within the scope of specified safety policies. RSafe operates
in two stages: (1) guided reasoning, where it analyzes safety risks of input content through policy-guided step-by-step reasoning, and (2) reinforced alignment, where rule-based RL optimizes its reasoning paths to align with accurate safety prediction. This two-stage training paradigm enables RSafe to internalize safety principles to generalize safety protection capability over unseen or adversarial safety violation
scenarios. During inference, RSafe accepts user-specified safety policies to provide enhanced safeguards tailored to specific safety requirements. Experiments demonstrate that RSafe matches state-of-the-art guard models using limited amount of public data in both prompt- and response-level harmfulness detection, while achieving superior out-of-distribution generalization on both emerging harmful category and jailbreak attacks. Furthermore, RSafe provides human-readable explanations for its safety judgments for better interpretability. RSafe offers a robust, adaptive, and interpretable solution for LLM safety moderation, advancing the development of reliable safeguards in dynamic real-world environments. Our code is available at https://anonymous.4open.science/r/RSafe-996D.

---

## 论文详细总结（自动生成）

由于提供的 PDF 提取文本仅包含验证页面，未能获取论文正文，以下总结完全基于提供的论文元数据（标题、作者、动机、方法、结果、结论等）和已知常识进行推断。部分细节（如具体数据集、算力、实验规模）因缺失而无法详述，将在相应条目中说明。

## 1. 核心问题与研究动机
- 尽管大语言模型（LLMs）经过了安全对齐，仍易受越狱攻击和新兴有害类别等**分布外威胁**的影响。
- 当前主流的系统级安全方案依赖**外部守卫模型**，但这些模型通常需要大量人工标注数据进行训练，成本高、覆盖面有限，且在分布外场景下表现脆弱。
- **RSafe**旨在解决这一矛盾：构建一种**低依赖、高泛化、可自适应**的守卫模型，使其在少量公开数据下即可提供鲁棒防护，并能灵活响应用户指定的安全策略。

## 2. 方法论
### 2.1 核心思想
- 赋予守卫模型**主动安全推理**能力，使其内部化安全原则，从而对未见过的、对抗性的违规场景进行泛化判断。
- 采用**两阶段训练范式**：引导式推理 + 强化对齐，无需额外人工标注。

### 2.2 关键技术细节（根据元数据推断）
- **引导式推理阶段**：模型在指定安全策略的引导下，对输入内容进行**分步骤的安全风险分析**，生成推理过程。
- **强化对齐阶段**：通过**基于规则的强化学习（RL）**优化模型的推理路径，使其朝着准确的安全预测方向对齐。
- **推理时的自适应**：模型可接受**用户自定义的安全政策**，根据不同场景动态调整防护目标，并提供**人类可读的安全性判断解释**，增强可解释性。

> 注：元数据未提供具体公式或算法伪代码，以上为对“guided safety reasoning”和“rule‑based RL”的合理展开。

## 3. 实验设计
- **任务场景**：提示级和响应级的有害内容检测。
- **评测维度**：常规模态检测、**新兴有害类别泛化**、**越狱攻击防御**。
- **对比基准**：与同期最先进的守卫模型进行对比（元数据中未列出具体模型名，但提到“state‑of‑the‑art guard models”）。
- **使用的数据集**：文中提及仅使用了**少量公开数据**，具体数据集名称未给出（如ToxicChat、OpenAI Moderation等常见基准待补全）。

## 4. 资源与算力
- 提供的元数据中**没有说明**训练所使用的 GPU 型号、数量及训练时长。从论文来源（NeurIPS‑2025‑Accepted）和仅用少量公开数据推断，训练成本可能较低，但确切实况未知。

## 5. 实验数量与充分性
- 具体进行的实验组数未在元数据中说明。根据结果描述，至少覆盖了：
  - 提示级和响应级检测任务；
  - 多个越狱攻击场景；
  - 分布外有害类别泛化测试；
  - 很可能包含消融实验（如去掉强化对齐或推理模块），但信息缺失无法确认。
- **充分性评价**：从结论来看，实验展示了有效的泛化能力，且不依赖大量标注数据，但在没有看到具体量化结果和对比基线的情况下，无法评估其客观性与公平性。

## 6. 主要结论与发现
- RSafe 在使用**有限公开数据**的条件下，达到了与最先进守卫模型相当的**提示级和响应级有害检测性能**。
- 在**新兴有害类别**和**越狱攻击**等分布外挑战上，RSafe 展现出**显著优势**，证明其推理‑泛化范式的有效性。
- 模型能够输出**可解释的安全判断推理**，便于审计和调试。
- 整体而言，RSafe 为构建**鲁棒、自适应、可解释**的 LLM 安全防护提供了低成本、易部署的新范式。

## 7. 优点与亮点
- **低数据依赖**：不依赖大量人工标注，大幅降低安全维护的人力成本。
- **分布外泛化能力强**：通过内化安全推理，有效应对未知的攻击方式和有害内容。
- **策略自适应**：推理时可插入用户定义的安全政策，实现定制化防护，灵活适应不同部署环境。
- **可解释性**：提供人类可读的推理链，提升透明度，便于安全审计。
- **简洁训练框架**：引导推理 + 规则 RL 的两阶段设计，思路清晰，复用性强。

## 8. 不足与局限
- **细节信息缺失**：由于论文正文不可见，无法评估方法的具体实现难度、推理开销、对复杂策略的表现等。
- **实验可比性未知**：缺少数据集、基线方法、具体指标数值，难以判断实验的严谨性和绝对性能。
- **推理成本**：生成逐步推理链可能增加推理时的计算开销和延迟，这对实时审查场景可能存在挑战。
- **策略依赖性**：安全防护效果可能很大程度上取决于所提供安全策略的质量与完备性，策略本身若存在偏差，可能影响判断。
- **对抗鲁棒性边界**：虽然声称对分布外越狱攻击有效，但未揭示在多轮对抗性提示、自适应越狱等方法下的退化情况。

---
（完）
