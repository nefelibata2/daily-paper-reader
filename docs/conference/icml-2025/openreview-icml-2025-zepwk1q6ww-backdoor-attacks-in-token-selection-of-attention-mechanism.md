---
title: Backdoor Attacks in Token Selection of Attention Mechanism
title_zh: 注意力机制词元选择中的后门攻击
authors: "Yunjuan Wang, Raman Arora"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=ZEPWk1Q6ww"
tags: ["query:priv-sec"]
score: 9.0
evidence: 利用注意力机制中词元选择的后门攻击
tldr: 后门攻击严重威胁基础模型安全，但成功原理缺乏理论解释。本文聚焦注意力机制中的词元选择，证明单头自注意力 Transformer 经梯度下降训练会内插投毒数据，并揭示触发词嵌入与查询/键矩阵的厄米特积的某个特性是攻击成功的关键。这为理解和防御此类攻击提供了理论基础。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 缺乏对 Transformer 后门攻击成功原理的严格理论分析。
method: 通过分析单头自注意力的梯度下降动力学，证明模型能内插投毒数据。
result: 推导出攻击成功需满足的触发词条件，并给出理论保证。
conclusion: 理论洞察可为设计更鲁棒的注意力机制或后门检测提供指导。
---

## Abstract
Despite the remarkable success of large foundation models across a range of tasks, they remain susceptible to security threats such as backdoor attacks. By injecting poisoned data containing specific triggers during training, adversaries can manipulate model predictions in a targeted manner. While prior work has focused on empirically designing and evaluating such attacks, a rigorous theoretical understanding of when and why they succeed is lacking. In this work, we analyze backdoor attacks that exploit the token selection process within attention mechanisms--a core component of transformer-based architectures. We show that single-head self-attention transformers trained via gradient descent can interpolate poisoned training data. Moreover, we prove that when the backdoor triggers are sufficiently strong but not overly dominant, attackers can successfully manipulate model predictions. Our analysis characterizes how adversaries manipulate token selection to alter outputs and identifies the theoretical conditions under which these attacks succeed. We validate our findings through experiments on synthetic datasets.

---

## 论文详细总结（自动生成）

# 论文总结：注意力机制词元选择中的后门攻击

## 1. 研究动机与核心问题
- **背景**：大规模基础模型（如Transformer）虽在多项任务上表现优异，却易受后门攻击威胁。攻击者在训练数据中注入含特定“触发器”的投毒样本，即可在推理阶段操控模型对特定输入的预测。
- **现有不足**：已有工作多为经验性设计攻击与防御，缺乏严格的理论解释，不清楚后门攻击为何及在何种条件下成功。
- **核心问题**：本文聚焦基于注意力机制中**词元选择过程**的后门攻击，旨在从理论层面揭示这类攻击成功的原理与条件。通过分析单头自注意力Transformer的梯度下降训练动力学，解释投毒数据的拟合过程，并推导出攻击生效所需满足的触发词特征条件。

## 2. 方法论
- **核心思想**：将后门攻击解释为模型通过注意力机制“内插”投毒数据的过程，进而从优化动力学角度分析攻击成功的充分条件。
- **关键技术细节**：
    - 研究对象为单头自注意力Transformer，分析其在梯度下降训练下对投毒数据的适应行为。
    - 证明模型能在训练中内插投毒样本，即模型输出可与投毒标签一致。
    - 揭示攻击成功的关键在于**触发词嵌入与查询/键矩阵的厄米特积**之间需满足某种谱特性：触发信号需足够强以引导注意力选择，但又不能过度主导，否则会破坏正常预测。
- **理论贡献**：
    - 给出攻击者操控词元选择以改变输出的机理。
    - 严格刻画了攻击成功的理论条件，并提供理论保证。

## 3. 实验设计
- **数据集**：仅提及在**合成数据集**上进行验证，未具体说明合成数据的生成方式或规模。
- **基线/对比方法**：摘要中未提及与其它后门攻击方法的对比，实验主要用于验证理论推导。
- **实验场景**：侧重理论验证，而非大规模基准评测。

## 4. 资源与算力
- **未明确说明**：所提供的摘要与元数据未提及GPU型号、数量、训练时长等算力细节。由于本文侧重理论分析，实验可能仅为小规模验证，算力需求可能较低，但无法确认。

## 5. 实验数量与充分性
- **实验数量有限**：基于现有信息，仅在合成数据集上进行实验，未展示在不同任务、不同数据分布或多头注意力下的扩展性。
- **充分性与客观性**：作为理论论文的实证补充，实验基本服务于验证命题，但未提及消融实验、超参数敏感性分析或与经验性攻击方法的量化比较，其充分性较难判断。从公平性角度看，缺乏横向对比可能使理论优势的实践价值不够直观。

## 6. 主要结论与发现
- 单头自注意力Transformer经梯度下降训练能内插投毒数据。
- 后门攻击成功需满足触发词嵌入与注意力参数交互的特定谱条件（足够强但不过度主导）。
- 理论分析为设计更鲁棒的注意力机制或后门检测方法提供了指导性洞察。

## 7. 优点
- **理论首创性**：首次对注意力机制中基于词元选择的后门攻击提供严格理论分析，填补了“知其然而不知其所以然”的空白。
- **机理阐释清晰**：将攻击归结于注意力矩阵与触发嵌入之间的内插与谱特性，可解释性强。
- **实践指导潜力**：推导出的成功条件可为防御方提供攻击检测与模型鲁棒性设计的理论依据。

## 8. 不足与局限
- **模型简化**：分析仅针对单头自注意力，而真实Transformer多为多头、多层的复杂结构，结论扩展性待验证。
- **实验覆盖不足**：仅在合成数据上验证，未在真实NLP或CV任务中检验，也缺乏与主流后门攻击方法的对比，结论的通用性受限。
- **假设严格性**：理论条件（触发信号强度适中）可能在实际中难以精确控制，攻击者在真实场景下的成功率未知。
- **潜在偏差**：理想化的理论设定可能忽略训练过程的随机性、优化器差异（如Adam）以及数据特性带来的影响。

（完）
