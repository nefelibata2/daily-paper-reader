---
title: "MetaDefense: Defending Fine-tuning based Jailbreak Attack Before and During Generation"
title_zh: MetaDefense：防御微调越狱攻击的生成前后防御
authors: "Weisen Jiang, Sinno Jialin Pan"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=ycMpNwzUAA"
tags: ["query:priv-sec"]
score: 10.0
evidence: 通过预生成检测有害查询和生成中监控部分响应来防御微调越狱攻击
tldr: 针对大语言模型微调中的越狱攻击，提出MetaDefense框架，采用两阶段防御：在回答生成前检测有害查询，并在生成过程中监控部分回复以防止有害内容输出。通过训练LLM预测查询和回复的有害性，该方法能泛化到未见过的攻击模板，提供更全面的安全防护。实验证明MetaDefense显著降低了越狱攻击成功率，为LLM安全部署提供了有效保障。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有防御方法难以泛化到未见过的攻击模板。
method: 提出两阶段防御：预生成有害检测和生成中监控。
result: 有效泛化到未知攻击，阻止有害内容生成。
conclusion: MetaDefense为LLM提供了更鲁棒的越狱攻击防御，提升了安全部署的可靠性。
---

## Abstract
This paper introduces MetaDefense, a novel framework for defending against finetuning-based jailbreak attacks in large language models (LLMs). 
We observe that existing defense mechanisms fail to generalize to harmful queries disguised by unseen attack templates, despite LLMs being capable of distinguishing disguised harmful queries in the embedding space. 
Based on these insights, we propose a two-stage defense approach: 
(i) pre-generation defense that detects harmful queries before response generation begins, and (ii) mid-generation defense that monitors partial responses during generation to prevent outputting more harmful content. 
Our MetaDefense trains the LLM to predict the harmfulness of both queries and partial responses using specialized prompts, enabling early termination of potentially harmful interactions. 
Extensive experiments across multiple LLM architectures (LLaMA-2-7B, Qwen-2.5-3B-Instruct, and LLaMA-3.2-3B-Instruct) demonstrate that MetaDefense significantly outperforms existing defense mechanisms, achieving robust defense against harmful queries with seen and unseen attack templates while maintaining competitive performance on benign tasks.
Code is available at [https://github.com/ws-jiang/MetaDefense](https://github.com/ws-jiang/MetaDefense).

---

## 论文详细总结（自动生成）

# 论文总结：MetaDefense: Defending Fine-tuning based Jailbreak Attack Before and During Generation

## 1. 核心问题与研究背景

- **研究动机**：大语言模型（LLM）在微调阶段容易受到“越狱攻击”（jailbreak attack），攻击者通过精心设计的恶意模板包装有害查询，使模型生成危险内容。
- **现有防御的局限**：已有防御手段对**已知攻击模板**有一定效果，但对**未见过的攻击模板**泛化能力弱，无法可靠地阻止新型越狱。
- **核心问题**：如何设计一个能够泛化到未知攻击模板的防御框架，在全面保护LLM安全的同时，尽量不影响良性任务的性能。

## 2. 方法论

### 核心思想与整体框架

- **两阶段防御**：  
  - **生成前防御（Pre‑generation Defense）**：在模型开始生成回答之前，检测输入查询是否为伪装的有害查询，若是则立即终止交互。  
  - **生成中防御（Mid‑generation Defense）**：在回答生成过程中，实时监控**部分响应**（partial responses）的有害性，一旦检测到有害内容倾向，便提前终止生成，阻止更多有害文本输出。

- **实现方式**：  
  - 通过**专门设计的提示（specialized prompts）**对LLM进行训练，使其能够**预测查询和部分回答的有害程度**。  
  - 训练目标是让模型学会在推理时判断当前输入或已生成片段是否包含有害意图或内容。  
  - 这种方法使得防御不再依赖攻击模板的指纹，而是依赖于对语义有害性的理解，从而**泛化到未见过的攻击模板**。

### 关键步骤流程
1. 收集或构造一批包含有害查询和良性查询的训练数据。  
2. 设计针对查询有害性预测的提示和针对部分回答有害性预测的提示。  
3. 在原有LLM基础上微调（或使用适配器），训练模型输出有害性标签。  
4. 部署时，在每个推理环节加入安全检查点：先检测输入查询，若有害则拒绝；若无害则逐步生成，并对部分回答进行持续监控，一旦有害则截断。

## 3. 实验设计

### 模型与基线
- **模型架构**：LLaMA‑2‑7B、Qwen‑2.5‑3B‑Instruct、LLaMA‑3.2‑3B‑Instruct（覆盖不同规模和家族的LLM）。  
- **对比方法**：与已有的防御机制进行对比（摘要中未具体列出名称，但指出“existing defense mechanisms”）。  

### 评估维度
- **攻击模板泛化性**：在**已知攻击模板**和**未知攻击模板**上测试防御成功率。  
- **良性任务保持度**：在正常、无害的查询上评估回复质量，确保防御不会显著降低有用性。  
- **核心指标**：越狱攻击成功率（Jailbreak success rate）等安全性指标，以及良性任务上的性能（如生成质量、准确率等）。

### 数据集/场景
- 摘要未提供具体数据集名称，但提到利用了包含有害查询的不同攻击模板进行测试，以验证方法在分布外（未见攻击）的鲁棒性。

## 4. 资源与算力

- **信息缺失**：论文摘要及提供的元数据中**未明确说明**使用的GPU型号、数量、训练时长等算力细节。  
- 考虑到实验涉及三个不同LLM的微调与评估，可以推测需要中等以上规模的算力资源，但具体配置需查阅正文。

## 5. 实验数量与充分性

- **实验数量推断**：摘要称“extensive experiments”，但未给出具体组数。从覆盖三个模型、可见与不可见攻击模板、与现有防御对比、以及良性任务保持等多个维度来看，实验至少包含**6‑10组核心对比实验**，可能还包括消融实验（如验证两阶段中每一阶段的作用）。  
- **充分性评价**：  
  - 正面：多模型、多攻击场景的对比能较好验证方法的通用性和有效性。  
  - 不足：缺乏数据集、对抗样本构造方式、训练协议等细节，难以从摘要判断实验是否完全公平、有无过拟合风险。  
- **客观性与公平性**：论文声称“显著优于现有机制”，但需要假设所有基线方法都在同等条件下重新实现或使用相同评估流程。摘要未透露基线是如何配置的，因此公平性有待全文披露。

## 6. 主要结论与发现

- **防御效果优异**：MetaDefense 能有效抵御基于微调的越狱攻击，在已知和未知攻击模板上均大幅度降低攻击成功率。  
- **泛化能力强**：相较于传统依赖攻击模板特征的防御，MetaDefense 利用 LLM 本身对有害语义的理解，实现了对未见攻击的强泛化。  
- **良性性能保持**：在正常的、非恶意的查询上，模型的回答质量未明显下降，展现出良好的安全‑有用平衡。  
- **整体价值**：为 LLM 安全部署提供了一种更鲁棒、更全面的防御范式，相关代码已开源。

## 7. 优点与亮点

- **两阶段协同防御**：创新性地将检查点前置（查询级）和延伸至生成过程（部分回答级），形成纵深防护。  
- **基于语义理解而非模板匹配**：训练模型直接预测有害性，天然具备对抗新模板的能力。  
- **模型无关性**：在多个不同架构和规模的 LLM 上得到验证，说明方法具有一定的通用性。  
- **实用性**：对良性任务影响小，易于集成到实际部署的 API 或对话系统中。  
- **开源可复现**：提供代码仓库，利于后续研究和应用。

## 8. 不足与局限

- **额外训练成本**：需要专门训练LLM进行有害性预测，增加了模型部署前的开销。  
- **训练数据依赖**：有害性预测的准确性高度依赖训练数据的质量和覆盖度，若训练数据存在偏差（例如对某些文化或语境的有害性界定不全），可能导致误判或漏判。  
- **中世代监控的实时性**：对于需要流式输出或低延迟的场景，增加生成中间的额外判断步骤可能影响响应速度。  
- **对抗性进化**：攻击者可能针对该防御机制设计专门绕过技术（如更隐蔽的攻击格式），长期鲁棒性尚需跟踪验证。  
- **实验细节不详**：摘要未提供攻击类型、数据集、具体评估指标等，无法判断其覆盖的威胁模型是否全面（例如是否包含多轮对话、角色扮演等攻击）。  
- **模型规模限制**：实验仅在7B及以下规模模型上进行，更大模型上的效果及开销未经验证。

---

（完）
