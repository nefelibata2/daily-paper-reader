---
title: "RepGuard: Adaptive Feature Decoupling for Robust Backdoor Defense in Large Language Models"
title_zh: RepGuard：面向大语言模型的鲁棒后门防御的自适应特征解耦
authors: "Chenxu Niu, Jie Zhang, Yanbing Liu, Yunpeng Li, Jinta Weng, Yue Hu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=jv7OHhQ0YP"
tags: ["query:priv-sec"]
score: 10.0
evidence: 通过解耦异常特征为LLM提供后门防御
tldr: 针对大语言模型面临的后门攻击威胁，现有防御多需已知触发器模式且治标不治本，本文提出RepGuard防御框架，通过融合局部一致性与全局对比的双重视角定位异常特征，并自适应解耦这些不可靠表征，从而在不依赖触发器具体形式的情况下增强模型鲁棒性，实验证明其在多种攻击下均有效，为LLM的安全部署提供了更稳固的保障。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有LLM后门防御依赖触发器先验知识，仅提供表面缓解，未根本解决不可靠特征依赖。
method: 提出RepGuard，通过双重视角特征定位与自适应解耦异常特征，实现与触发器模式无关的防御。
result: 防御方法在多种后门攻击下表现出强鲁棒性，且不影响正常任务性能。
conclusion: RepGuard为LLM的后门威胁提供了更根本和通用的防御策略。
---

## Abstract
Backdoor attacks pose a significant threat to large language models (LLMs) by embedding malicious triggers that manipulate model behavior. However, existing defenses primarily rely on prior knowledge of backdoor triggers or targets and offer only superficial mitigation strategies, thus struggling to fundamentally address the inherent reliance on unreliable features. To address these limitations, we propose a novel defense strategy, \textit{RepGuard}, that strengthens LLM resilience by adaptively separating abnormal features from useful semantic representations, rendering the defense agnostic to specific trigger patterns. Specifically, we first introduce a dual-perspective feature localization strategy that integrates local consistency and sample-wise deviation metrics to identify suspicious backdoor patterns. Based on this identification, an adaptive mask generation mechanism is applied to isolate backdoor-targeted shortcut features by decomposing hidden representations into independent spaces,  while preserving task-relevant semantics. With a multi-objective optimization framework, our method can inherently mitigates backdoor attacks. Across \textit{Target Refusal} and \textit{Jailbreak} tasks under four types of attacks, RepGuard consistently reduced the attack success rate on poisoned data by nearly 80\% on average, while maintaining near-original task performance on clean data. Extensive experiments demonstrate that RepGuard provides a scalable and interpretable solution for safeguarding LLMs against sophisticated backdoor threats.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究动机（背景）

- **问题背景**：大语言模型（LLM）在现实部署中面临后门攻击的严重威胁。攻击者通过在训练数据中嵌入恶意触发器，操纵模型行为，例如使模型在输入包含特定触发词时输出错误或有害内容。
- **现有防御的局限性**：
  - 大多依赖对后门触发器或攻击目标的先验知识（如已知触发词、中毒数据分布），这在实践中难以获取。
  - 提供的缓解策略多为表面修补，未能从根本上解决模型对不可靠特征（即后门捷径特征）的内在依赖。
  - 缺乏一种与具体触发器模式无关的、能从根本上增强模型鲁棒性的防御方法。
- **核心动机**：设计一种无需预先知晓触发器形式的通用防御，通过解耦异常特征来真正消除LLM对后门特征的依赖，使防御具有更强的泛化性和鲁棒性。

## 2. 方法论：RepGuard

- **整体思想**：通过自适应地将异常后门特征从有用语义表征中分离出来，从根本上削弱后门攻击的影响，实现与触发器模式无关的防御。
- **关键技术细节**：
  - **双重视角异常特征定位**：
    - 引入**局部一致性**指标：考察样本在局部邻域内的表征一致性，后门样本通常会破坏这种一致性。
    - 引入**样本级偏离**指标：衡量单个样本在全局特征空间中的偏离程度，后门特征常表现为显著异常。
    - 将两种视角融合，精准识别出可能被植入后门的可疑表征。
  - **自适应掩码生成与特征解耦**：
    - 基于上一步定位结果，自动生成掩码，将隐藏层表征分解到相互独立的子空间中。
    - 一部分子空间用于隔离与后门相关的捷径特征（不可靠特征），另一部分保留任务相关语义。
    - 通过这种方式，模型在下游处理中仅使用解耦后的干净语义表征，从而免疫后门触发。
  - **多目标优化框架**：在训练过程中同时优化干净数据上的任务性能与后门特征抑制目标，使防御与任务学习协同进行，模型内在地减轻后门攻击。

## 3. 实验设计（数据集/场景/基准/对比方法）

- **评估任务**：在 `Target Refusal`（拒绝目标对象）和 `Jailbreak`（越狱）两大类任务上验证。
- **攻击类型**：覆盖四种具有代表性的后门攻击方法，展现了防御的通用性。
- **对比基准**：
  - 攻击成功率（Attack Success Rate, ASR）在有后门的数据（poisoned data）上的下降幅度。
  - 干净数据（clean data）上的任务性能保持程度。
  - 文中未列明具体对比的防御方法名称，但强调与依赖触发器先验的防御形成对比。

## 4. 资源与算力

- 提供的摘要与元数据中**未明确说明**使用的硬件资源（如GPU型号、数量）、训练时长或参数量级。因此，无法从现有信息推断其算力消耗。

## 5. 实验数量与充分性

- **实验组数推断**：
  - 2个任务 × 4种攻击类型 × 至少1种干净/中毒数据设置 = 至少8组主要对比实验，外加消融研究（如双视角解耦模块的有效性、多目标优化的贡献等），估计总体实验数量在10组以上。
- **充分性与客观性**：
  - 攻击类型覆盖较广，验证了跨攻击的通用性。
  - 同时关注攻击成功率和干净数据性能，避免了以牺牲正常功能为代价的片面防御评估。
  - 消融实验可进一步支撑方法各模块的必要性，实验设计相对客观、公平。
- **可能不足**：由于摘要仅提供平均“近80%”的ASR降低，未报告不同攻击/任务下的详细波动，读者无法判断在某些极端情况下防御是否依然稳定。

## 6. 主要结论与发现

- RepGuard能够**平均降低近80%的攻击成功率**（在有后门的数据上），显著遏制多种后门攻击。
- 在干净数据上，模型**保持了与原始相近的任务性能**，表明防御不会损害正常功能。
- 该方法提供了一种**可扩展、可解释**的LLM安全防护方案，不依赖具体触发模式，为对抗日益复杂的后门威胁提供了更根本的解决路径。

## 7. 优点与亮点

- **触发无关性**：无需假设攻击者使用的触发器形式，极大提升了实战可用性。
- **根本性防御**：通过解耦特征空间直接消除对捷径特征的依赖，而非简单拒绝可疑输入，属于更彻底的治理方案。
- **多维特征定位**：融合局部一致性与全局偏离的视角，创新性地从表征层面锁定后门信号。
- **多任务验证**：在Target Refusal和Jailbreak两类性质不同的任务上均有效，展示了一定的任务泛化能力。

## 8. 不足与局限

- **实验细节缺失**：当前仅依据摘要，未能提供具体的数据集、模型规模、对比基线方法、消融结果等关键信息，难以评估方法的真实边界。
- **泛化边界不明确**：虽测试了四种攻击，但未知这四种攻击的覆盖度是否足够（如是否涵盖数据中毒、权重投毒等不同威胁模型），且不一定代表所有现实攻击场景。
- **计算开销未知**：特征解耦和双视角定位可能引入额外计算或存储开销，文中未讨论效率问题，可能影响其在超大规模LLM上的部署可行性。
- **与最新防御的对比缺失**：摘要未列出具体的对比防御算法，无法判断RepGuard相较当下最先进防御的优势幅度及是否仍存在短板。
- **评估指标单一**：仅报告攻击成功率与干净任务性能，未涉及防御引入的虚假拒绝率、表征质量等更细粒度的度量。

（完）
