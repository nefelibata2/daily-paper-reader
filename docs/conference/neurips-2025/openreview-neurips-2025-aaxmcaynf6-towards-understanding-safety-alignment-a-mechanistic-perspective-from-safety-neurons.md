---
title: "Towards Understanding Safety Alignment: A Mechanistic Perspective from Safety Neurons"
title_zh: 理解安全对齐：从安全神经元的机械视角
authors: "Jianhui Chen, Xiaozhi Wang, Zijun Yao, Yushi Bai, Lei Hou, Juanzi Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=AAXMcAyNF6"
tags: ["query:priv-sec"]
score: 7.0
evidence: 识别LLM中的安全神经元以理解和恢复安全对齐，有助于防御有害内容生成
tldr: "尽管经过安全对齐，大语言模型仍可能生成有害内容。本文从机械可解释性角度探索安全对齐机制，提出推理时激活对比定位安全神经元，并通过动态激活修补验证其因果作用。实验发现约5%的神经元负责安全行为，仅修补其激活即可恢复超90%的安全性能，为理解并加固模型安全提供了新思路。"
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 安全对齐后LLM仍存在安全风险，内部机制不清，缺乏有效的定位与修复方法。
method: 提出推理时激活对比法定位安全神经元，并用动态激活修补检验因果效应。
result: "在多个LLM中稳定识别出约5%的安全神经元，修补后安全性能恢复超过90%。"
conclusion: 揭示了LLM安全的神经元基础，为可解释安全防御提供了新方向。
---

## Abstract
Large language models (LLMs) excel in various capabilities but pose safety risks such as generating harmful content and misinformation, even after safety alignment. In this paper, we explore the inner mechanisms of safety alignment through the lens of mechanistic interpretability, focusing on identifying and analyzing safety neurons within LLMs that are responsible for safety behaviors. We propose inference-time activation contrasting to locate these neurons and dynamic activation patching to evaluate their causal effects on model safety. Experiments on multiple prevalent LLMs demonstrate that we can consistently identify about 5% safety neurons, and by only patching their activations we can restore over 90% of the safety performance across various red-teaming benchmarks without influencing general ability. The finding of safety neurons also helps explain the ''alignment tax'' phenomenon by revealing that the key neurons for model safety and helpfulness significantly overlap, yet they require different activation patterns for the same neurons. Furthermore, we demonstrate an application of our findings in safeguarding LLMs by detecting unsafe outputs before generation.

---

## 论文详细总结（自动生成）

# 论文总结：理解安全对齐——从安全神经元的机械视角

## 1. 研究动机与核心问题
- **安全对齐的局限**：大语言模型（LLM）虽在安全对齐（safety alignment）后仍存在生成有害内容、错误信息等安全风险，表明现有对齐方式并未根除模型内部的脆弱性。
- **机制黑箱**：安全对齐的内部机制尚不清晰，缺少可解释、可定位、可修复的神经元级理解。
- **研究目标**：从机械可解释性（mechanistic interpretability）角度，识别并分析LLM中负责安全行为的“安全神经元”，从而解释、评估并加固模型安全。

## 2. 方法论
- **核心思想**：安全行为由少量可定位的神经元承载，通过对比安全与不安全输入下的激活差异，找出关键神经元，再通过定向干预验证因果作用。
- **关键技术细节**：
  - **推理时激活对比（Inference-time Activation Contrasting）**：前向传播过程中，对比同一模型在处理安全提示与不安全提示（或经扰动的提示）时的神经元激活，定位激活模式差异显著的神经元作为“安全神经元”。
  - **动态激活修补（Dynamic Activation Patching）**：对已失效或弱化的安全神经元进行激活值修补（即在推理时强行将其激活调整为安全状态下的值），以恢复模型的安全拒绝行为，而不影响通用能力。
- **算法流程说明**（基于文本描述）：
  1. 收集成对的安全/不安全输入样本。
  2. 记录模型各层各神经元的激活值。
  3. 通过对比分析，筛选出激活差异最大的神经元集合（约5%）。
  4. 在推理时，对定位出的安全神经元实施激活修补，观察安全性能恢复情况，验证因果性。

## 3. 实验设计
- **数据集与评测基准**：使用多个广泛使用的红队测试基准（red-teaming benchmarks），具体名称在摘要中未列出，但通常包括对有害内容、偏见、越狱等安全维度的评估。
- **对比方法**：未详细说明基线对比方法，但实验主要验证定位方法的准确性以及修补后安全性能恢复程度（恢复超过90%），并与无干预的原始模型进行对比。
- **场景**：涵盖多种主流LLM，表明方法的跨模型泛化能力。

## 4. 资源与算力
- **文中未明确提及**GPU型号、数量、训练时长等具体算力信息。元数据及摘要中未给出硬件配置或能耗数据。推测使用标准学术推理环境，但无法确认。

## 5. 实验数量与充分性
- **实验组数**：
  - 在多个流行LLM上进行定位实验（数量未详述，但至少涵盖多个模型）。
  - 安全神经元占比统计（约5%重现）。
  - 激活修补后的安全性能恢复测试（红队基准上对比）。
  - 通用能力影响测试（确保修补不损害通用表现）。
  - “对齐税”现象分析（安全与有用性神经元重叠但激活模式相反）。
  - 应用验证：基于安全神经元检测不安全输出（可能含分类或预警实验）。
- **充分性**：从摘要看，实验设计涵盖定位、因果验证、泛化性、副作用分析以及实际应用，整体较为全面。但具体数据集规模、消融实验细节未透露，无法进一步判断统计充分性。

## 6. 主要结论与发现
- **安全神经元可稳定识别**：在多种LLM中，约5%的神经元可以被一致地定位为安全相关。
- **因果效应强**：仅修补这些神经元的激活就能恢复超过90%的安全性能，且不影响通用能力。
- **解释“对齐税”**：安全与有用性共享关键神经元，但两者对同一神经元的激活模式要求相反，这解释了为什么强安全对齐可能降低模型有用性。
- **实用价值**：可利用安全神经元检测未生成即判断不安全输出，为实时安全防护提供新手段。

## 7. 优点
- **机械可解释性视角**：提供神经元级别的安全机制理解，超越黑盒分析。
- **方法简单有效**：无需重新训练或微调，推理时干预即可大幅恢复安全性。
- **细粒度因果验证**：动态激活修补为因果推断提供直接证据。
- **对齐税的新解释**：从神经元激活模式重叠与冲突的角度揭示安全与有用的权衡。
- **应用导向**：展示安全神经元在输出前检测的潜力，具有实际防御价值。

## 8. 不足与局限
- **实验覆盖未详述**：具体测试基准、对抗性越狱类型、模型规模范围等信息缺失，可能影响结论普适性。
- **数据集偏差风险**：安全神经元的定位依赖对比样本的构造，若对比集覆盖不全，可能漏掉隐蔽攻击模式。
- **安全性恢复上限**：恢复90%安全性能仍留有残余风险，未说明剩余10%的失败模式。
- **动态修补的工程可行性**：推理时逐神经元修补可能引入额外开销，文中未讨论延迟或部署成本。
- **机制深度有限**：仅定位神经元而未分析其内部计算回路或多层协同机制，解释力尚局限。

（完）
