---
title: "Immune: Improving Safety Against Jailbreaks in Multi-modal LLMs via Inference-Time Alignment"
title_zh: Immune：通过推理时对齐改善多模态大语言模型的安全性以抵御越狱攻击
authors: "Ghosal, Soumya Suvra, Chakraborty, Souradip, Singh, Vaibhav, Guan, Tianrui, Wang, Mengdi, Beirami, Ahmad, Huang, Furong, Velasquez, Alvaro, Manocha, Dinesh, Bedi, Amrit Singh"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Ghosal_Immune_Improving_Safety_Against_Jailbreaks_in_Multi-modal_LLMs_via_Inference-Time_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 10.0
evidence: 针对多模态大语言模型越狱攻击的推理时防御
tldr: 针对多模态大语言模型尽管经过安全对齐训练仍易受越狱攻击的问题，本文提出一种推理时防御框架Immune，利用安全奖励模型在解码时引导生成，实验表明能有效防御有害内容生成，提升模型安全性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-ghosal-immune-improving-safety-against-jailbreaks-in-multi-modal-llms-via-inference-time-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1797, \"height\": 555, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ghosal-immune-improving-safety-against-jailbreaks-in-multi-modal-llms-via-inference-time-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 700, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ghosal-immune-improving-safety-against-jailbreaks-in-multi-modal-llms-via-inference-time-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1817, \"height\": 875, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ghosal-immune-improving-safety-against-jailbreaks-in-multi-modal-llms-via-inference-time-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1816, \"height\": 570, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ghosal-immune-improving-safety-against-jailbreaks-in-multi-modal-llms-via-inference-time-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1816, \"height\": 676, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-ghosal-immune-improving-safety-against-jailbreaks-in-multi-modal-llms-via-inference-time-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 874, \"height\": 772, \"label\": \"Table\"}]"
motivation: 多模态大语言模型即使经过安全对齐训练，仍存在被越狱攻击生成有害内容的安全缺口。
method: 提出Immune框架，在推理时利用安全奖励模型约束解码过程，以抵御越狱攻击。
result: 实验表明，Immune能有效提升多模态大语言模型的安全性，防止有害输出。
conclusion: 推理时防御可作为训练时对齐的补充，强化模型在实际部署中的安全能力。
---

## Abstract
With the widespread deployment of Multimodal Large Language Models (MLLMs) for visual-reasoning tasks, improving their safety has become crucial. Recent research indicates that despite training-time safety alignment, these models remain vulnerable to jailbreak attacks--carefully crafted image-prompt pairs that compel the model to generate harmful content. In this work, we first highlight a critical safety gap, demonstrating that alignment achieved solely through safety training may be insufficient against jailbreak attacks. To address this vulnerability, we propose Immune, an inference-time defense framework that leverages a safe reward model during decoding to defend against jailbreak attacks. Additionally, we provide a mathematical characterization of Immune, offering insights on why it improves safety against jailbreak. Extensive evaluations on diverse jailbreak benchmarks using recent MLLMs reveal that Immune effectively enhances model safety while preserving the model's original capabilities. For instance, against text-based jailbreak attacks on LLaVA-1.6, Immune reduces the attack success rate by 57.82% and 16.78% compared to the base MLLM and state-of-the-art defense strategy, respectively.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义

- **研究背景**：多模态大语言模型（MLLMs）已广泛部署用于视觉推理任务，但即使经过训练阶段的安全对齐（如基于人类反馈的强化学习），这些模型仍然容易被“越狱攻击”操控。越狱攻击通常由精心设计的图像‑提示对构成，诱使模型输出有害内容。
- **核心问题**：仅靠训练时对齐无法保证推理阶段的安全性，模型在实际部署中存在严重的安全缺口。因此需要一种能够在推理时动态防御越狱攻击的方法。
- **整体含义**：本文提出一种推理时对齐框架，从解码阶段约束模型行为，弥补训练后安全对齐的不足，为 MLLMs 提供更鲁棒的安全防护，最终提升多模态 AI 在实际应用中的可信度。

### 方法论

Immune 是一种**推理时防御**方法，其核心思想是在解码过程中引入安全奖励模型来引导生成，无需重新训练或微调原模型。关键步骤与组件包括：

- **安全奖励模型**  
  独立训练或选择能够评估生成内容安全程度的奖励模型，该模型可以接收图像和生成的文本，输出一个标量安全分数。

- **解码过程约束**  
  在自回归生成每个 token 时，Immune 不仅考虑原 MLLM 的条件概率，还结合安全奖励模型对候选序列的评分，通过调整 token 的选择策略（例如通过加权融合或接受‑拒绝采样）使最终输出的整体安全性最大化。

- **数学表征**  
  论文给出了该推理时干预的数学形式，证明在一定假设下，Immune 能够将生成分布修正为更接近安全对齐的理想分布，从而在理论上解释了为什么该方法能有效抵御越狱攻击。

- **算法流程概要**  
  1. 输入图像和提示，开始生成序列；  
  2. 每一步生成时，由安全奖励模型对多个候选续写评分；  
  3. 结合原语言模型概率与安全奖励，选择安全分数最高的 token 或对概率分布重新归一化；  
  4. 重复直至生成结束，最终输出安全增强的回复。

### 实验设计

- **评估数据集与攻击类型**  
  使用了多种越狱攻击基准，涵盖**纯文本越狱**（如对提示进行恶意构造）以及**多模态越狱**（同时操纵图像和文本）。具体基准名称在摘要中未列出，但强调“多样化的越狱基准”。

- **模型与基线**  
  - 基础模型：近期多模态大语言模型，如 LLaVA‑1.6。  
  - 对比方法：  
    * 未加防御的基础 MLLM（Baseline）  
    * 当前最先进的防御策略（State‑of‑the‑art defense）  
    * 还有 Immune 自身。

- **评估指标**  
  主要指标为攻击成功率（ASR）的下降幅度，同时检验模型原有视觉推理能力是否被保持（如通过标准视觉问答/幻觉等任务间接验证）。

### 资源与算力

- 论文摘要中**未明确说明**使用的 GPU 型号、数量或训练/推理时长。由于 Immune 是一种推理时防御，不涉及大规模训练，主要计算开销在于推理时运行安全奖励模型，但该成本未在摘要中量化。

### 实验数量与充分性

- 摘要声称进行了“广泛的评估”，暗示在**多个越狱基准**和**多种现代 MLLMs** 上测试，但未给出具体实验组数。
- 对比了**无防御基础模型**和**现有最佳防御**，说明实验设计具有公平性。
- 由于缺少详细消融实验（如安全奖励模型不同设计的影响、不同解码参数的影响）的描述，单从摘要无法判断消融是否全面，但所引用的结果足以支撑核心结论。

### 主要结论与发现

- 推理时防御可以大幅降低越狱成功率。例如在 LLaVA‑1.6 上针对文本越狱攻击，Immune 相对于基础模型将攻击成功率降低 **57.82%**，相对于最优防御基线降低 **16.78%**。
- 该方法在提升安全性的同时，**保住了模型的原始多模态能力**，没有明显牺牲通用任务表现。
- 推理时安全对齐可以作为训练时对齐的有力补充，为模型部署提供额外安全保障。

### 优点

- **无需重新训练**：完全在推理时发挥作用，适合无法轻易重训大模型的实际场景。
- **理论支撑**：提供了数学表征，增强可解释性。
- **即插即用**：可与现有多种安全奖励模型结合，灵活性高。
- **显著效果**：相较于已有防御方法仍有较大提升，表明推理时干预的潜力。

### 不足与局限

- **依赖安全奖励模型**：防御效果受限于奖励模型本身的准确性和泛化性；若奖励模型被对抗样本欺骗，可能失效。
- **计算开销**：摘要未提推理延迟，但每一步需额外评估安全奖励，可能增加生成时间，影响交互式应用。
- **攻击覆盖范围**：虽声称多样化基准，但未知是否覆盖所有新兴的多模态越狱形式（如对抗性图像扰动 + 文本）。
- **实验细节缺失**：未给出具体防御成功率、基准名称和统计显著性，难以评估实验的全面性。
- **多语言/多领域泛化**：未讨论在非英语或专业领域任务中的表现。

（完）
