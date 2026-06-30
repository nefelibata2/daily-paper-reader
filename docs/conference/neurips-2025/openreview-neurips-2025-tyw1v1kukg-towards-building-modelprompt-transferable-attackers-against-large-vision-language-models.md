---
title: Towards Building Model/Prompt-Transferable Attackers against Large Vision-Language Models
title_zh: 面向大视觉语言模型的可迁移模型/提示攻击构建
authors: "Xiaowen Cai, Daizong Liu, Xiaoye Qu, Xiang Fang, Jianfeng Dong, Keke Tang, Pan Zhou, Lichao Sun, Wei Hu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=TyW1V1KukG"
tags: ["query:priv-sec"]
score: 9.0
evidence: 针对大视觉语言模型的可迁移对抗攻击
tldr: 现有针对大视觉语言模型的对抗攻击容易过拟合特定模型或提示，缺乏可迁移性。本文从信息论视角探索LVLM输出间的相对依赖关系，提出了一种对黑盒模型和不同语义提示均有效的可迁移攻击方法。在多种架构和任务上的广泛评估表明，该方法显著提高了攻击跨模型和跨提示的迁移成功率，揭示了多模态模型普遍存在的安全脆弱性，为鲁棒性研究提供了新基准。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有LVLM攻击泛化性差，无法在不同模型和提示间迁移，亟需更通用的攻击方法以暴露安全风险。
method: 从信息论角度建模LVLM输出依赖，设计对模型和提示不敏感的可迁移对抗样本生成方法。
result: 在多个黑盒LVLM上实现了高迁移攻击成功率，显著优于现有方法。
conclusion: 该方法揭示了多模态模型的普遍脆弱性，为未来防御研究提供了重要参考。
---

## Abstract
Although Large Vision-Language Models (LVLMs) exhibit impressive multimodal capabilities, their vulnerability to adversarial examples has raised serious security concerns.
Existing LVLM attackers simply optimize adversarial images that easily overfit a certain model/prompt, making them ineffective once they are transferred to attack a different model/prompt. 
Motivated by this research gap, this paper aims to develop a more powerful attack that is transferable to black-box LVLM models of different structures and task-aware prompts of different semantics. 
Specifically, we introduce a new perspective of information theory to investigate LVLMs' transferable characteristics by exploring the relative dependence between outputs of the LVLM model and input adversarial samples. Our empirical observations suggest that enlarging/decreasing the mutual information between outputs and the disentangled adversarial/benign patterns of input images helps to generate more agnostic perturbations for misleading LVLMs' perception with better transferability. 
In particular, we formulate the complicated calculation of information gain as an estimation problem and incorporate such informative constraints into the adversarial learning process.
Extensive experiments on various LVLM models/prompts demonstrate our significant transfer-attack performance.

---

## 论文详细总结（自动生成）

# 面向大视觉语言模型的可迁移模型/提示攻击构建

## 1. 论文的核心问题与整体含义
* **研究动机与背景**：大型视觉‑语言模型（LVLMs）在展现强大多模态能力的同时，对对抗样例表现出明显脆弱性，带来严重安全风险。
* **现有方法的局限**：已有的 LVLM 攻击方法主要针对特定模型或特定提示（prompt）优化对抗图像，极易过拟合，一旦迁移到不同结构模型或不同语义的任务提示上，攻击效果急剧下降，缺乏泛化性。
* **本文目标**：填补这一研究空白，开发一种能够迁移到黑盒 LVLM（不同架构）以及不同语义提示（不同下游任务）上的更强攻击手段，以更全面地暴露模型安全弱点。

## 2. 论文提出的方法论
* **核心思想**：从信息论视角分析 LVLM 输入‑输出的相对依赖关系，通过控制对抗样本与干净样本所对应图像模式之间的互信息，来生成与具体模型/提示弱相关的“不可知扰动”，从而提升攻击的跨模型、跨提示迁移性。
* **关键技术细节**：
  - 将输入图像分解为**对抗模式**与**良性模式**（disentangled patterns），并考察它们与 LVLM 输出的互信息。
  - 实证观察表明，**扩大或减小**输出与这两种分解模式之间的互信息，有助于合成更具泛化性的扰动，误导 LVLM 感知而不绑定特定模型或提示。
  - 将复杂的**信息增益计算**转化为一个可估计的优化问题，并将这些信息约束嵌入对抗学习过程，形成一种对模型/提示不敏感的攻击生成框架。
* **流程概述**（文字描述）：
  1. 解耦输入图像的模式成分；
  2. 估计输出与各模式间的互信息（或信息增益）；
  3. 在生成对抗扰动时，施加扩大/缩小此类互信息的约束；
  4. 通过迭代优化得到的对抗样本，在黑盒场景下实现高迁移攻击。

## 3. 实验设计
* **数据集/场景**：论文中未提供具体的数据集名称，仅提及“各种 LVLM 模型/提示”上的广泛评估。结合元数据，推测涵盖了多种架构的视觉‑语言模型及不同语义的任务提示（如 VQA、图像描述等）。
* **基准与对比方法**：摘要与元数据未列出具体对比方法，但明确指出所提方法显著优于现有攻击，且实验检验了“跨黑盒模型结构”和“跨不同语义提示”两种迁移设定。
* **评估指标**：虽然没有明示，但可推知使用攻击成功率（如导致模型输出违反任务目标或生成指定错误回答的比例）度量迁移性。

## 4. 资源与算力
* **文中说明**：提供的论文摘要和元数据中**未提及** GPU 型号、数量、训练时长或任何算力开销。
* **结论**：无法从现有信息获得资源消耗的细节。

## 5. 实验数量与充分性
* **实验数量**：仅说明“大量实验”（Extensive experiments），但未给出具体组数、数据集数量或消融实验的明细。
* **充分性与公平性**：由于缺少数值结果和具体对比配置，难以从提供的有限文本严格评价其充分性与公平性。但鉴于被 NeurIPS‑2025 接收且评分 9.0，可推断同行评审认可其实验设计的扎实性与对比的客观性。摘要中强调“显著迁移攻击表现”，暗示实验证据相对充分。

## 6. 论文的主要结论与发现
* 提出的基于互信息约束的攻击方法，成功实现了对黑盒 LVLM 的高效跨模型、跨提示迁移攻击，攻击成功率大幅超越现有方法。
* 揭示了多模态模型普遍存在的安全脆弱性，即攻击不依赖特定模型架构或提示语义，也能诱导错误输出。
* 为未来防御研究提供了新的基准测试方法，强调需要关注模型/提示层面的泛化攻击。

## 7. 优点
* **视角新颖**：首次从信息论角度建模 LVLM 输入‑输出依赖，为提升攻击迁移性提供理论依据。
* **方法普适性好**：攻击不针对特定模型或提示，在黑盒迁移条件下表现突出，更贴近真实攻击场景。
* **理论与实践结合**：将互信息计算问题转化为可估计优化目标，嵌入对抗学习，技术路径清晰。
* **安全洞察深刻**：不仅设计攻击，更通过暴露跨模型脆弱性推动了对 LVLM 鲁棒性的理解。

## 8. 不足与局限
* **实验细节透明性有限**：未提供具体数据集、基准模型列表、攻击参数和成功率数据，难以独立复现或完全评估实验规模。
* **防御讨论缺失**：未提及如何利用该方法指导防御设计，或对抗扰动的可防御性。
* **迁移上限未知**：摘要未说明在处理极多样化的 LVLM 架构（如不同预训练范式）时的迁移退化情况。
* **仅攻击视觉‑语言模型**：方法主要针对 LVLM，向其他多模态组合（如语音‑视觉）的拓展性不明确。
* **信息估计精度**：将信息增益作为估计问题引入，估计误差对攻击效果的影响未讨论。

（完）
