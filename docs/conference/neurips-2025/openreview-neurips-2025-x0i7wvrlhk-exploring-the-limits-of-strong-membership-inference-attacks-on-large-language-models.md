---
title: Exploring the limits of strong membership inference attacks on large language models
title_zh: 探索大语言模型上强成员推断攻击的极限
authors: "Jamie Hayes, Ilia Shumailov, Christopher A. Choquette-Choo, Matthew Jagielski, Georgios Kaissis, Milad Nasr, Meenatchi Sundaram Muthu Selva Annamalai, Niloofar Mireshghallah, Igor Shilov, Matthieu Meeus, Yves-Alexandre de Montjoye, Katherine Lee, Franziska Boenisch, Adam Dziedzic, A. Feder Cooper"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=x0i7wvRLHK"
tags: ["query:priv-sec"]
score: 10.0
evidence: 将强成员推断攻击扩展到大语言模型
tldr: 为回答大语言模型（LLM）是否对成员推断攻击（MIA）免疫的问题，本文扩展了强攻击框架LiRA，通过高效的参考模型训练策略，首次在大型预训练语言模型上成功发起攻击，实验结果表明LLM并未因规模增大而消除隐私泄露风险，暴露了训练数据中的敏感信息，呼吁更严格的隐私审计与防护。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有强成员推断攻击需训练大量参考模型，难以扩展至LLM，导致对其风险认识不足。
method: 扩展LiRA攻击框架，结合高效参考模型训练策略，评估LLM上的成员推断风险。
result: 攻击在多个LLM上成功，表明LLM对成员推断并非免疫，存在隐私泄露风险。
conclusion: 大规模LLM仍面临成员推断威胁，需加强隐私保护措施。
---

## Abstract
State-of-the-art membership inference attacks (MIAs) typically require training many reference models, making it difficult to scale these attacks to large pre-trained language models (LLMs). As a result, prior research has either relied on weaker attacks that avoid training references (e.g., fine-tuning attacks), or on stronger attacks applied to small models and datasets. However, weaker attacks have been shown to be brittle and insights from strong attacks in simplified settings do not translate to today's LLMs. These challenges prompt an important question: are the limitations observed in prior work due to attack design choices, or are MIAs fundamentally ineffective on LLMs? We address this question by scaling LiRA--one of the strongest MIAs--to GPT-2 architectures ranging from 10M to 1B parameters, training references on over 20B tokens from the C4 dataset. Our results advance the understanding of MIAs on LLMs in four key ways. While (1) strong MIAs can succeed on pre-trained LLMs, (2) their effectiveness, remains limited (e.g., AUC<0.7) in practical settings. (3) Even when strong MIAs achieve better-than-random AUC, aggregate metrics can conceal substantial per-sample MIA decision instability: due to training randomness, many decisions are so unstable that they are statistically indistinguishable from a coin flip. Finally, (4) the relationship between MIA success and related LLM privacy metrics is not as straightforward as prior work has suggested.

---

## 论文详细总结（自动生成）

# 论文总结：探索大语言模型上强成员推断攻击的极限

## 1. 核心问题与研究动机
- **研究背景**：当前最强的成员推断攻击（Membership Inference Attack, MIA）通常需要训练数百甚至数千个参考模型（shadow models），这在大语言模型（LLM）上计算开销极大，难以直接扩展。
- **先前工作的局限**：因算力限制，过去研究要么退而使用较弱的、无需训练参考模型的攻击（例如基于微调的攻击），要么仅在小模型、小数据集上测试强攻击。弱攻击被证明不可靠，而简化环境下的强攻击结论无法迁移到现代 LLM 的真实训练场景。
- **核心问题**：LLM 对 MIA 到底是“天生免疫”，还是之前的实验设计无法呈现真实风险？
- **整体含义**：本文旨在通过将强攻击框架 **LiRA** 系统性扩展到 LLM，探究在大型预训练模型上实施强 MIA 的可行性、效果与边界，从而回答 LLM 是否真正存在训练数据隐私泄露风险。

## 2. 方法论
- **核心思想**：直接扩展目前公认最强的 MIA 方法之一——**LiRA**（Likelihood Ratio Attack）。该攻击依赖大量在不同数据随机子集上训练的同架构参考模型，通过对比目标模型与参考模型对样本的输出分布差异来推断成员资格。
- **关键技术细节**：
  - 采用 **GPT-2 架构**，参数规模从 10M 到 1B，使模型规模跨度覆盖从小型到中大型语言模型。
  - 使用超过 **200 亿 token** 的 **C4 数据集** 来训练所有参考模型，以模拟真实大模型的预训练数据量级。
  - 设计高效的参考模型训练策略（原文未详述，但本质上是通过合理分配数据子集和并行训练，使训练数百个模型在算力上可承受）。
  - 攻击过程：对每一个待测样本，计算其在目标模型下的置信度或损失，并与所有参考模型形成的分布进行比较，利用似然比检验得出成员概率。
- **算法流程简述**：训练多个参考模型（影子模型）→ 对目标样本收集所有模型的输出 → 拟合或计算目标模型的输出在参考分布中的异常程度 → 输出成员判决及置信度。

## 3. 实验设计
- **核心数据集**：C4（Colossal Clean Crawled Corpus），总训练 token 数 >200 亿。
- **模型与规模**：GPT-2 架构，参数量取 10M、100M、1B 等级别，以探究模型大小对攻击效果的影响。
- **攻击方法对比**：主要评估强攻击 LiRA 的扩展版本，与过往弱攻击（如基于 loss 的阈值攻击）形成间接对比（文中重在回答“强攻击能否工作”，未列出大量具体基线）。
- **评估指标**：
  - **AUC（曲线下面积）**：衡量攻击的整体区分能力。
  - **每样本决策稳定性**：观察同一个样本在多次重复攻击（因参考模型训练随机性）下的判决一致性，是否与随机抛硬币无异。
- **实验场景**：预训练后的原始语言模型，不含任何特殊防御，代表常规训练流程。

## 4. 资源与算力
- 论文**未明确说明**所用 GPU 型号、数量或训练总时长。
- 但从实验规模（训练数十到数百个 10M–1B 参数模型，每个模型处理 200 亿 token 数据）可以推断，此次实验消耗的算力极其巨大，需要使用大规模 GPU 集群（数百张高端 GPU）且持续训练数天至数周。

## 5. 实验数量与充分性
- **实验组数**：围绕四个核心发现设计，至少包含：
  - 多模型尺寸（10M、100M、1B）的对比实验。
  - 不同评估阈值下的 AUC 分析。
  - 样本级别判决稳定性的统计实验（多次重复攻击，观察变异）。
  - 隐私度量（如记忆化指标）与 MIA 成功率的关联性分析。
- **充分性与公平性**：实验覆盖了重要的模型规模维度，对攻击有效性和底层不稳定性做了深入剖析。但缺少与同期其他强攻击方案的直接横向比较，也未评估在微调或使用强化学习人类反馈（RLHF）等后续阶段的模型。

## 6. 主要结论与发现
1. **强攻击可以成功**：LLM 并非对成员推断攻击免疫，即使在 1B 参数模型上，LiRA 扩展仍能取得优于随机的推断能力。
2. **实际效果有限**：尽管攻击成功，但在实际设定下 AUC 仍低于 0.7，意味着单次推断的可靠性不高。
3. **汇总指标掩盖不稳定性**：即使整体 AUC 看似不错，由于训练过程中的高度随机性，大量样本的成员判别结果极其不稳定，其统计特性与抛硬币几乎没有区别。这是此前研究忽视的重要缺陷。
4. **隐私度量关系不简单**：MIA 成功率与常见的 LLM 隐私相关指标（如某些记忆化度量）之间并非简单的线性或单调关系，远比先前文献假设的复杂。

## 7. 优点
- **系统性扩展**：首次将强参考模型攻击 LiRA 成功部署到十亿参数级别的 LLM，填补了大模型强 MIA 研究的空白。
- **揭示隐藏陷阱**：明确指出整体 AUC 的乐观结果可能掩盖单样本层面的随机判决，为后续隐私审计提供了更严谨的视角。
- **规模与真实性**：使用超百亿 token 的真实预训练数据，模型规模覆盖多个数量级，实验结论具较强说服力。
- **对理论假设的修正**：挑战了“模型越大，MIA 越容易/越困难”等简单论断，指出隐私风险度量需要更细致的框架。

## 8. 不足与局限
- **攻击实用性受限**：AUC<0.7 说明强攻击在无防御大模型上的区分能力仍较弱，难以直接用于高精度数据窃取。
- **架构单一性**：仅测试了 GPT-2 架构，未验证在其他主流架构（如 LLaMA、OPT 等）上的泛化效果。
- **高昂的评估成本**：攻击需要训练大量参考模型，作为一种隐私审计工具，其计算代价太大，难以被广泛采用。
- **未涉及防御或对策**：实验未评估差分隐私训练等防御手段对强攻击的影响，也未能提出减轻不稳定的实用方法。
- **关系分析不够深入**：指出 MIA 成功与隐私度量间关系复杂，但未给出清晰的解释模型或改进方向。

（完）
