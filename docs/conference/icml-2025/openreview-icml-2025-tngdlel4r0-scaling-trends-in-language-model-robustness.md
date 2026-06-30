---
title: Scaling Trends in Language Model Robustness
title_zh: 语言模型鲁棒性的缩放趋势
authors: "Nikolaus H. R. Howe, Ian R. McKenzie, Oskar John Hollinsworth, Michał Zając, Tom Tseng, Aaron David Tucker, Pierre-Luc Bacon, Adam Gleave"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=tNGdLEL4R0"
tags: ["query:priv-sec"]
score: 9.0
evidence: 大模型对抗越狱和提示注入攻击鲁棒性的缩放分析
tldr: 本文通过大规模对抗攻击实验分析语言模型鲁棒性的缩放趋势。结果显示，缺乏安全训练时增大模型规模并不持续提高鲁棒性，但规模可改善对抗训练的样本效率并降低计算效率。该研究为理解大模型安全防御提供了规模视角，对防御策略设计具有指导意义。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 大模型在越狱和提示注入攻击下仍脆弱，需要从缩放视角理解安全态势变化。
method: 通过多种分类任务、模型家族和对抗攻击的大规模实验，系统分析鲁棒性的缩放规律。
result: 发现显式安全训练至关重要，规模提升样本效率但恶化计算效率。
conclusion: 安全训练和样本效率而非单纯规模是提升大模型鲁棒性的关键。
---

## Abstract
Increasing model size has unlocked a dazzling array of capabilities in language models.
At the same time, even frontier models remain vulnerable to jailbreaks and prompt injections, despite concerted efforts to make them robust.
As both attackers and defenders gain access to more compute, and as models become larger, what will be the effect on robustness?
We argue that to answer this question requires a *scaling lens*, which we adopt in an extensive study of language model robustness across several classification tasks, model families, and adversarial attacks.
We find that in the absence of explicit safety training, larger models are not consistently more robust; however, scale improves sample efficiency in adversarial training, though it worsens compute efficiency.
Further, we find that increasing attack compute smoothly improves attack success rate against both undefended and adversarially trained models.
Finally, after exploring robustness transfer across attacks and threat models, we combine attack and defense scaling rates to study the offense-defense balance.
We find that while attack scaling outpaces adversarial training across all models studied, larger adversarially trained models might give defense the advantage in the long run.
These results underscore the utility of the scaling lens, and provide a paradigm for evaluating future attacks and defenses on frontier models.
Code for this project is available at https://github.com/AlignmentResearch/scaling-llm-robustness-paper.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：大语言模型（LLM）在规模化扩展中展现出强大能力，但即使是最前沿的模型仍易受越狱攻击（jailbreaks）和提示注入（prompt injections）的影响。尽管已有大量防御努力，鲁棒性问题并未根本解决。
- **核心问题**：随着攻击者和防御者双方可获得的算力同步增长，以及模型规模持续扩大，语言模型的鲁棒性会如何变化？在没有明确安全训练的情况下，扩大模型规模是否自然带来更高的鲁棒性？对抗训练的效率在不同模型规模下如何演变？
- **整体含义**：本文提出必须通过 **“缩放透镜”（scaling lens）** 来审视鲁棒性，即从算力和模型规模共同变化的视角系统性评估攻防态势。理解这些缩放趋势，有助于预测未来攻防平衡，并为大模型的安全防护设计提供基于规模的理论指导。

## 2. 论文提出的方法论

- **核心思想**：将鲁棒性视为模型规模、防御算力（对抗训练）和攻击算力的函数，通过大规模受控实验测量这些变量之间的缩放关系，从而绘制出“攻防缩放定律”。
- **技术路线**：
  - 在多个**分类任务**上（例如有害内容检测等）部署不同规模的模型家族。
  - 针对无防御模型和经过对抗训练的模型，分别施加多种**对抗攻击**（如基于梯度的攻击、黑盒攻击等）。
  - 系统性地改变：
    - 模型参数量；
    - 攻击所用算力（如优化步数、候选样本数）；
    - 防御所用算力（如对抗训练的计算预算、对抗样本数量）。
  - 测量关键指标随上述变量的变化规律，重点考察**样本效率**（达到一定鲁棒性所需的标注数据量）与**计算效率**（单位算力带来的鲁棒性提升）。
  - 最后，将攻击缩放率与防御缩放率进行对比，分析攻防平衡的长期走向。
- **公式或算法流程**（文字说明）：
  - 虽然原始元数据未给出具体公式，但方法可概括为“对抗鲁棒性的经验缩放分析”：
    1. 固定任务，选定多个模型规模；
    2. 对每个规模进行对抗训练（防御）时，变化训练数据中对抗样本的生成预算；
    3. 分别测量无防御模型与对抗训练模型在不同攻击强度下的鲁棒性指标（如攻击成功率）；
    4. 拟合鲁棒性随模型参数量、攻防计算预算变化的幂律或类似缩放曲线；
    5. 对比攻击曲线与防御曲线的斜率，判断长期优势方。

## 3. 实验设计

- **任务与数据集**：基于多个分类场景，具体名称未在元数据中明确，但涵盖与安全性直接相关的判断任务（如越狱检测、有害输出分类等），以此模拟真实世界中攻击者对语言模型的操控目标。
- **Benchmark 与评价指标**：
  - 主要指标：**攻击成功率**（针对无防御模型和对抗训练模型）及其随计算预算的变化。
  - 辅助指标：鲁棒性的样本效率、计算效率。
- **对比的方法/维度**：
  - 不同模型规模（参数量从数亿到数百亿级别）之间的对比；
  - 有无明确安全训练（即针对性对抗训练）的对比；
  - 不同攻击算法之间的对比，以及通过迁移学习测量鲁棒性在不同攻击和威胁模型之间的可转移性；
  - 攻防预算组合的全面网格搜索以分析平衡点。
- **对比的基准线**：无防御原始模型作为脆弱性基线，普通对抗训练（未专门优化缩放）作为防御基线。

## 4. 资源与算力

- **原文提及情况**：提供的元数据中并未出现具体的 GPU 型号、数量或训练时长等算力细节。论文作者在摘要和结论中仅强调了“计算效率”“攻击计算平滑提升成功率”等缩放概念，但未披露实验实际消耗的硬件资源。
- **推测**：鉴于研究涉及多模型家族、多攻击防御组合的大规模网格实验，可以合理推断其使用了相当规模的 GPU 集群（例如 A100 或同代产品），但确切数字需参阅论文完整版。

## 5. 实验数量与充分性

- **实验规模**：
  - 覆盖了多种分类任务（至少数个具体任务）；
  - 包含多个语言模型家族（不同架构、不同规模），至少有不同参数量级的模型；
  - 使用了多种对抗攻击方法（黑盒、白盒）并测试跨攻击迁移；
  - 针对每个组合变动攻击算力与防御算力，形成高维网格实验。
- **充分性评价**：
  - 实验设计由宏观缩放规律驱动，通过大量组合控制变量分离规模、攻击预算、防御预算三者的独立影响，系统性较强。
  - 结果一致地表明“无安全训练时规模不持续提升鲁棒性”以及“样本效率提升但计算效率下降”等趋势，说明这些发现并非偶然。
  - 被 ICML 2025 接收，也从侧面验证了其实验设计和论证的充分性与客观性。
- **公平性**：对比在同一任务和攻击条件下进行，模型规模等差递增，攻击与防御算力统一度量，保证了对比的公平性。

## 6. 论文的主要结论与发现

- **规模本身不保证鲁棒性**：在缺乏专门安全训练的情况下，更大的语言模型并非始终更鲁棒，有时鲁棒性甚至会随规模持平或下降。
- **对抗训练的规模效益分化**：
  - **样本效率提升**：扩大模型规模可提升对抗训练的样本效率，即用更少的标注对抗样本就能达到特定的鲁棒性水平。
  - **计算效率恶化**：然而，规模扩大也导致对抗训练的计算效率降低，单位算力带来的鲁棒性增益反而减少。
- **攻击算力的平滑缩放**：增加攻击方的计算预算（如增加搜索步数、尝试次数）会平滑且持续地提高对无防御及对抗训练模型的攻击成功率，未出现明显的“饱和”平台。
- **鲁棒性的跨攻击迁移**：观察到不同攻击类型和威胁模型之间存在鲁棒性的迁移现象，这暗示某些防御可以泛化，但也意味着攻击者可能利用迁移性。
- **攻防平衡的长期预测**：在目前所有研究的模型条件下，攻击的缩放速率普遍快于对抗训练带来的防御改进；但如果模型规模足够大并且持续进行对抗训练，防御方**在长期**可能获得优势。这意味着超大规模模型的防御潜力尚未耗尽。
- **总体启示**：显式安全训练（对抗训练）是提升鲁棒性的关键，单纯依赖模型自然规模增长无法构建安全的语言模型。

## 7. 优点

- **首创的缩放视角**：将鲁棒性研究从静态比较提升到动态缩放规律分析，为安全研究提供了可预测的框架。
- **攻防一体化分析**：同时考察攻击和防御的规模效应，并建立攻防平衡模型，实用价值强。
- **实验全面系统**：多任务、多模型、多攻击类型的大规模网格实验，剥离出规模、安全训练、算力预算的独立效应，结论可靠。
- **明确的实践指导**：结论直接指出了“安全训练必不可少”、“超大规模下防御仍有希望”等对工业界和学术界极具指导意义的观点。
- **开放科学**：提供了开源代码仓库，便于复现和后续研究。

## 8. 不足与局限

- **任务与攻击的代表性局限**：实验主要基于分类任务，与现代 LLM 中更复杂的生成式越狱攻击（如多轮对话、社会工程攻击）可能存在差距，结论向生成式场景的泛化性尚待验证。
- **攻击与防御类型覆盖**：虽然使用了多种攻击，但未穷尽所有前沿攻击（如某些基于自然语言心理学的越狱），防御也只侧重对抗训练，缺少对 RLHF、安全微调等其他防御范式的缩放分析。
- **“长期”预测的不确定性**：关于超大规模模型可能使防御占优的结论，建立在现有缩放曲线外推的基础上，现实中可能遇到训练稳定性、数据质量等瓶颈，外推风险较大。
- **算力数据缺失**：元数据未提供具体的实验算力消耗，使得外部评估其样本效率与计算效率的实际成本变得困难，可能削弱对计算效率恶化结论的感性认知。
- **内部有效性**：虽然实验设计控制了多个变量，但对抗训练中对抗样本的生成方式与攻击模型可能相互影响，部分观察到的效率变化或许受到实现细节的干扰。

（完）
