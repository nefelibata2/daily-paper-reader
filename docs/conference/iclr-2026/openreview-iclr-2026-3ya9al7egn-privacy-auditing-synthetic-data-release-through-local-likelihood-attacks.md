---
title: Privacy Auditing Synthetic Data Release through Local Likelihood Attacks
title_zh: 通过局部似然攻击审计合成数据发布的隐私
authors: "Joshua Ward, Chi-Hua Wang, Guang Cheng"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=3ya9al7egn"
tags: ["query:priv-sec"]
score: 9.0
evidence: 针对表格生成模型的成员推理攻击用于隐私审计
tldr: 本文提出Gen-LRA，一种计算高效的无盒成员推理攻击，利用表格生成模型对训练分布局部区域的过拟合现象，审计合成数据发布中的隐私泄露，为生成模型隐私评估提供了实用的审计工具。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有合成数据隐私审计框架依赖启发式方法，无法有效检测生成模型对训练数据的隐私暴露。
method: 提出生成似然比攻击Gen-LRA，利用模型过拟合特性，在无模型访问假设下进行成员推理。
result: 实验证明Gen-LRA能以较低计算代价准确检测训练数据泄露。
conclusion: 该方法填补了表格生成模型隐私审计的空白，有助于安全合成数据部署。
---

## Abstract
Auditing the privacy leakage of synthetic data is an important but unresolved problem. Most existing privacy auditing frameworks for synthetic data rely on heuristics and unreasonable assumptions to attack the failure modes of generative models, exhibiting limited capability to describe and detect the privacy exposure of training data through synthetic data release. In this paper, we study designing Membership Inference Attacks (MIAs) that specifically exploit the observation that tabular generative models tend to significantly overfit to certain regions of the training distribution. Here, we propose Generative Likelihood Ratio Attack (Gen-LRA), a novel, computationally efficient No-Box MIA that, with no assumption of model knowledge or access, formulates its attack by evaluating the influence a test observation has in a surrogate model's estimation of a local likelihood ratio over the synthetic data. Assessed over a comprehensive benchmark spanning diverse datasets, model architectures, and attack parameters, we find that Gen-LRA consistently dominates other MIAs for generative models across multiple performance metrics. These results underscore Gen-LRA's effectiveness as a privacy auditing tool for the release of synthetic data, highlighting the significant privacy risks posed by generative model overfitting in real-world applications.

---

## 论文详细总结（自动生成）

基于提供的论文摘要及元数据，以下是对该论文的结构化中文总结：

## 1. 核心问题与研究动机
- **核心问题**：合成数据发布中的隐私泄露审计是一个重要但未解决的难题。现有框架多依赖启发式方法和不合理的假设来攻击生成模型的失效模式，难以有效描述和检测训练数据通过合成数据暴露的隐私。
- **研究动机**：表格生成模型存在一个关键观察——它们倾向于对训练分布的某些局部区域严重过拟合。本文旨在设计一种能专门利用此现象的成员推理攻击（MIA），为合成数据提供更可靠的隐私审计工具。

## 2. 方法论：生成似然比攻击（Gen‑LRA）
- **核心思想**：利用生成模型对训练分布局部区域的过拟合特性，通过评估一个测试样本对代理模型在合成数据上估计的局部似然比的影响，来推断该样本是否为训练成员。
- **关键假设与设定**：
  - **无盒（No‑Box）攻击**：不需要假设任何模型知识或访问权限（如模型参数、梯度），仅依赖合成数据本身。
  - **局部似然比**：攻击的核心是构造一个局部统计量，衡量测试样本的出现如何改变代理模型对合成数据的似然估计。过拟合区域中，训练样本会对此似然产生异常影响。
- **算法流程（文字概述）**：
  1. 使用合成数据训练一个代理模型（surrogate model），用于近似生成模型的行为。
  2. 对于一个待测样本，将其融入代理模型的训练过程或似然评估中，计算局部似然比的变化量。
  3. 基于该变化量制定攻击决策（成员/非成员），变化越显著，越可能是训练成员。
- **计算效率**：方法被设计为计算高效，无需重复训练复杂模型。

## 3. 实验设计
- **数据集与场景**：据摘要描述，实验覆盖了多样化的数据集（具体名称未在给定文本中列出），并针对表格数据生成模型进行审计。
- **基准方法**：与多种针对生成模型的其它成员推理攻击（MIAs）进行对比。
- **实验变量**：综合基准测试涵盖了不同的模型架构和攻击参数，以全面评估 Gen‑LRA 的性能。
- **评估指标**：采用多个性能指标（如攻击准确率、真正率、精确率等，未具体展开），证明 Gen‑LRA 持续占优。

## 4. 资源与算力
- 论文摘要及元数据中**未明确提及**所使用的 GPU 型号、数量、训练时长或算力开销。仅描述了方法“计算高效”，但未提供具体的硬件配置或运行时间数据。

## 5. 实验数量与充分性
- **实验规模**：摘要指出实验在“全面的基准”上进行，跨越多样数据集、模型架构和攻击参数，暗示进行了多组对比实验和参数分析。
- **充分性与公平性**：
  - 通过跨数据集、跨模型、多指标对比，实验设计较为充分。
  - 与现有 MIA 直接比较，且在不具备模型访问权限的相同条件下评估，公平性较高。
  - 但由于提供的文本未给出具体实验数量（如多少数据集、多少消融实验），无法量化判断其详尽程度。

## 6. 主要结论与发现
- Gen‑LRA 在多种性能指标上**持续显著优于**其它针对生成模型的成员推理攻击。
- 实验结果证实了生成模型过拟合造成的显著隐私风险，并强调 Gen‑LRA 可作为合成数据发布前的一种有效隐私审计工具。
- 该方法填补了表格生成模型隐私审计领域的空白，对安全部署合成数据具有实际意义。

## 7. 优点
- **攻击假设现实**：无需模型访问或先验知识，符合真实场景中的审计需求。
- **直接针对过拟合现象**：利用生成模型的固有缺陷设计攻击，原理清晰，检测能力强。
- **计算高效**：声称计算开销低，有潜力应用于大规模审计。
- **实验全面**：跨越多种数据集和模型架构，验证了方法的通用性和鲁棒性。

## 8. 不足与局限
- **信息有限**：基于现有摘要和元数据，无法得知具体的数据集类型（如医疗、金融等）、模型库以及攻击的绝对性能值。实验的统计显著性和误差棒也未呈现。
- **应用局限**：方法仅在表格生成模型上验证，对其他类型生成模型（如图像、文本）的适用性未知。
- **代理模型依赖**：需要对合成数据训练代理模型，该代理模型的选取和训练方式可能影响攻击效果，文中未说明其敏感性。
- **对抗适应性未知**：若生成模型特意加入了针对局部似然攻击的防御措施，攻击有效性可能下降。

（完）
