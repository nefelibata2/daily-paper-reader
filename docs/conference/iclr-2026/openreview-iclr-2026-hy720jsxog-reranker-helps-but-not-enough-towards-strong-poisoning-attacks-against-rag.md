---
title: "Reranker Helps, but Not Enough: Towards Strong Poisoning Attacks Against RAG"
title_zh: 重排序器有帮助但还不够：针对RAG的强投毒攻击
authors: "Xiaokun Yang, Yesheng Liu, Xin Xiong, Jian Liang, Ran He, Tieniu Tan"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=hY720JSxOG"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出针对RAG的强投毒攻击并分析基于重排序器的防御措施。
tldr: 现有针对检索增强生成（RAG）的投毒攻击面对重排序器时效果有限。本文通过揭示重排序器的盲点，设计了一种更强的投毒攻击方法，表明仅靠重排序器防御不足，从而推动RAG安全红队测试。实验显示该攻击有效绕过防御，强调了加强RAG安全对策的必要性。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 现有RAG投毒攻击在配备重排序器后效果有限，防御能力存在盲点。
method: 提出基于提示扰动的强投毒攻击方法，利用重排序器漏洞绕过过滤。
result: 实验表明攻击能有效突破重排序器防御，增强了RAG安全性评估。
conclusion: 仅靠重排序器不足以防御投毒攻击，需要更全面的安全措施。
---

## Abstract
Retrieval-Augmented Generation (RAG) augments Large Language Models with timely, external information, making their retrieval corpora a prime target for data poisoning. 
However, existing targeted poisoning attacks exhibit limited effectiveness against RAG equipped with a reranker to enhance retrieval quality.
Remarkably, this defensive benefit comes at no additional cost: a reranker fine-tuned only on benign, in-domain documents can effectively filter malicious content without any adversarial training. 
To realistically evaluate RAG and strengthen red-teaming efforts, we conclude practical prompt design principles that reveal reranker blind spots.
Building on these insights, we introduce the $\textbf{P}$rompt-$\textbf{P}$erturbation $\textbf{P}$oisoning $\textbf{A}$ttack ($\mathbf{P}^3 \mathbf{A}$), a novel framework for generating sophisticated poisoned documents. 
$\text{P}^3\text{A}$ first employs rule-based prompt engineering to craft initial poisoned texts designed to evade reranker filtering.
It then injects subtle character-level perturbations into these texts, which promotes their ranking by the reranker while maintaining their adversarial effectiveness. 
These perturbations introduce only about 1\% textual change, ensuring the poisoned texts remain natural and readable.
Extensive experiments demonstrate that our methods achieve effective attack performance, compromising reranker-enhanced RAG pipelines.
Furthermore, our method exhibits strong transferability, proving equally effective against vanilla RAG—offering a more realistic and challenging benchmark for evaluating defense mechanisms.
Code is available in the supplementary material.

---

## 论文详细总结（自动生成）

# 论文总结：重排序器有帮助但还不够：针对RAG的强投毒攻击

## 1. 核心问题与研究动机
- **背景**：检索增强生成（RAG）通过引入外部知识库提升大语言模型的事实性与时效性，但也使得检索语料库成为投毒攻击的天然目标。
- **现有问题**：已有的针对性投毒攻击在面对带有重排序器（reranker）的 RAG 系统时，攻击效果大幅下降。而且这种防御几乎零成本——仅用良性、领域内文档微调的重排序器，无需对抗训练就能有效过滤恶意内容。
- **动机**：为了更真实地评估 RAG 系统的安全性、推动红队测试，必须揭示重排序器的盲点，并设计出能绕过其过滤的更强投毒攻击。

## 2. 方法论：Prompt‑Perturbation Poisoning Attack (P³A)
- **核心思想**：两阶段生成投毒文档，先通过提示工程绕过重排序器的语义理解，再引入不可察觉的字符级扰动来“操纵”重排序器的排序分数。
- **第一阶段：规则型提示工程**
  - 利用对重排序器弱点的分析，设计一套提示工程原则，手工构造初始的投毒文本，使其在语义层面不易被重排序器判定为恶意。
- **第二阶段：字符级扰动注入**
  - 在初始文本中注入微小的字符级扰动（如拼写变体、同形字符、微小词形变化等），这些扰动能显著提升文本在重排序器中的排名，同时仍保留对抗样本的攻击效力。
  - 扰动程度仅占文本的约 **1%**，确保文本的自然性与可读性。
- **特点**：该框架生成的投毒文档既能有效绕过重排序器，又能保持对下游生成任务的对抗影响，且攻击具有强迁移性，对无重排序器的 vanilla RAG 同样有效。

## 3. 实验设计
- **数据集与场景**：摘要中仅提及“广泛实验”（extensive experiments），未列出具体数据集名称或领域。从研究背景推测，可能使用了开放域问答或知识密集型任务的标准测试集。
- **对比方法**：
  - 带有重排序器的 RAG 系统作为基线防御；
  - 与已有针对性投毒攻击方法进行对比；
  - 攻击在 vanilla RAG 与 reranker‑enhanced RAG 两种设置下测试，并评估迁移性。
- **评估指标**：尽管未直接给出，但通常会关注攻击成功率、重排序器过滤率、生成文本的准确性/毒性变化等。
- **公正性与客观性**：通过展示攻击对两种 RAG 变体均有效，以及攻击构建过程中对扰动的严格控制（1% 文本变动），保持了对比的公平性。

## 4. 资源与算力
- 摘要及提供的元数据中**未提及**任何 GPU 型号、数量、训练时长等算力信息。该部分缺失，无法判断其计算开销。

## 5. 实验数量与充分性
- 文中提到“广泛实验”（extensive experiments），但**未提供具体实验组数**，如消融实验数量、跨数据集测试数量等。从摘要推断，至少应包括：
  - 不同攻击方法的对比；
  - 有无重排序器的对比；
  - 攻击迁移性测试；
  - 可能包含对不同重排序器或不同 RAG 配置的测试。
- 实验的充分性虽在作者陈述中获得肯定，但缺少具体数字支撑，完整性有待补充。

## 6. 主要结论与发现
- **重排序器并非万无一失**：仅靠良性数据微调的重排序器存在可被利用的盲点，不足以完全防御投毒攻击。
- **P³A 攻击有效且隐蔽**：所提方法能稳定攻破重排序器增强的 RAG，且生成的投毒文本自然程度高、扰动比例极低。
- **强迁移性**：攻击同样适用于未部署重排序器的简单 RAG 系统，为评估 RAG 防御提供了一个更真实、更具挑战性的基准。
- **安全启示**：需要比当前重排序器更全面的防御措施，才能保障 RAG 管道的安全。

## 7. 优点与亮点
- **揭示防御盲点**：系统性地分析了重排序器在对抗投毒时的弱点，并归纳出实用的提示设计原则。
- **创新的双层攻击框架**：结合语义层的提示工程与字符级的扰动优化，兼顾绕过能力与不可察觉性。
- **现实意义强**：强调红队测试与真实风险评估，攻击方法不依赖对防御设施的过度假设，贴近实际威胁模型。
- **高扰控水平**：仅约 1% 的文本变动即达到攻击目的，保持了样本质量，不易触发基于困惑度等的简单防御。

## 8. 不足与局限
- **实验细节缺失**：提供的论文内容仅为摘要，无法获知具体数据集、对比的基线方法细节、消融实验结构、评估指标等，难以独立评判实验的严谨性与覆盖范围。
- **攻击策略可能被针对性防御**：一旦攻击方法公开，防御方可通过微调重排序器、引入字符级扰动检测等手段进行抵抗，攻击的长期有效性存疑。
- **场景泛化性未知**：摘要未说明在多种领域、不同语种或不同模型上的泛化效果，跨领域鲁棒性有待验证。
- **伦理风险**：强攻击技术的披露可能被恶意利用，论文的平衡性（同时提出防御思路）在摘要中未见体现。

（完）
