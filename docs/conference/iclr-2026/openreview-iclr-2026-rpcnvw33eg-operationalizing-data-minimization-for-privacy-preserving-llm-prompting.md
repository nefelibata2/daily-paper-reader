---
title: Operationalizing Data Minimization for Privacy-Preserving LLM Prompting
title_zh: 实现面向隐私保护大语言模型提示的数据最小化
authors: "Jijie Zhou, Niloofar Mireshghallah, Tianshi Li"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=rpcnvW33EG"
tags: ["query:priv-sec"]
score: 10.0
evidence: 将数据最小化原则操作化用于保护隐私的大语言模型提示，减少个人信息暴露
tldr: 大语言模型在消费者应用中频繁处理个人信息，用户常为获得有用回答而过度分享，增加隐私风险。本文首次形式化并操作化了提示中的数据最小化原则，通过定义隐私有序变换空间和优先队列树搜索，寻找在保持效用前提下最少暴露隐私信息的提示方案。在开放对话和知识密集型任务数据集上的实验证实，该方法能有效减少敏感信息泄漏，为用户提示隐私保护提供了定量工具。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 用户在提示中常分享过多个人信息，导致大模型通过记忆或上下文等机制引发隐私泄漏，亟需最小化数据暴露。
method: 构建隐私有序变换空间，并设计优先队列树搜索算法，动态定位效用与隐私的最优平衡点。
result: 在ShareGPT、WildChat等四个数据集上，该方法显著降低提示中的个人可识别信息，同时保持回答质量。
conclusion: 数据最小化框架为大模型应用中的用户隐私保护提供了一套可操作的范式，有望成为隐私设计的基础组件。
---

## Abstract
The rapid deployment of large language models (LLMs) in consumer applications has led to frequent exchanges of personal information. To obtain useful responses, users often share more than necessary, increasing privacy risks via memorization, context-based personalization, or security breaches. We present a framework to formally define and operationalize *data minimization*: for a given user prompt and response model, quantifying the least privacy-revealing disclosure that maintains utility, and propose a priority-queue tree search to locate this optimal point within a privacy-ordered transformation space. We evaluated the framework on four datasets spanning open-ended conversations (ShareGPT, WildChat) and knowledge-intensive tasks with single-ground-truth answers (CaseHOLD, MedQA), quantifying achievable data minimization with nine LLMs as the response model. Our results demonstrate that larger frontier LLMs can tolerate stronger data minimization while maintaining task quality than smaller open-source models (*85.7%* redaction for GPT-5 vs. *19.3%* for Qwen2.5-0.5B). By comparing with our search-derived benchmarks, we find that LLMs struggle to predict optimal data minimization directly, showing a bias toward abstraction that leads to oversharing. This suggests not just a privacy gap, but a capability gap: models may lack awareness of what information they actually need to solve a task.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景与动机**：大型语言模型（LLM）在消费级应用中的快速部署导致用户频繁在提示（prompt）中输入个人信息。为了获得有用回答，人们常过度分享，增加了因模型记忆、上下文个性化和安全漏洞带来的隐私风险。
- **核心问题**：如何将数据最小化原则（data minimization）从设计理念转化为可操作的隐私保护工具，在保持任务效果（utility）的前提下，自动找到暴露最少隐私信息的提示方式。
- **整体含义**：本文首次形式化并操作化了LLM提示中的数据最小化，为用户与LLM交互中的隐私保护提供了定量评估和自动化框架，试图弥补模型自身“不知道真正需要多少信息才能完成任务”的能力缺口。

### 2. 论文提出的方法论

- **核心思想**：定义隐私有序变换空间（privacy-ordered transformation space），在该空间内通过搜索寻找一个最优提示版本，使得响应质量得以维持，同时将个人信息暴露降到最低。
- **关键技术细节**：
  - **隐私有序变换空间**：将原始提示中的可识别个人信息进行逐步抽象或删减，生成一系列由强隐私保护（最多变换）到弱隐私保护（最少变换）的候选提示，构成一个具有单调隐私水平排序的空间。
  - **优先队列树搜索算法**：设计了一种优先队列树搜索（priority-queue tree search），从原始提示出发，在变换空间中不断生成子节点（通过替换、泛化、遮蔽等操作），并利用效用评分（来自目标LLM的回答质量）和隐私暴露程度的量化指标，动态定位效用与隐私的最优平衡点。
- **公式与流程**：虽无具体公式展示，但方法可理解为：给定初始提示 \( P \)，变换函数集合 \( T \)，效用评估函数 \( U(P') \)，以及隐私度量 \( \text{Priv}(P') \)，通过树搜索找到 \( P^* = \arg\min \text{Priv}(P') \quad s.t. \quad U(P') \geq \tau \)，其中 \( \tau \) 为效用阈值。树搜索利用优先队列按隐私度优先展开，尽早发现高隐私低暴露的解。

### 3. 实验设计

- **数据集与场景**：
  - **开放式对话**：ShareGPT、WildChat，模拟日常交流中用户可能透露的个人信息。
  - **知识密集型单答案任务**：CaseHOLD（法律类问答）、MedQA（医学问答），要求精确事实，测试在强信息需求下能否有效最小化数据。
- **Benchmark**：以原始提示的回答质量作为基线，比较不同数据最小化程度的提示下，模型回答的准确度/质量变化；同时用搜索得到的最优隐私-效用点作为基准，评估其他方法（如直接让LLM自行进行数据最小化）的表现。
- **对比方法**：主要对比了让LLM直接预测最优数据最小化的方式（即模型自己判断如何抽象或删减个人信息），并将其结果与本文搜索算法得到的基准进行比较，以揭示模型在“自我认知所需信息”方面的偏差。

### 4. 资源与算力

- 提供的元数据及摘要中**未明确说明**所用GPU型号、数量、训练时长等具体算力信息。论文未提及需要额外训练模型，主要计算消耗应来自对多个LLM响应模型的推理以及搜索过程中的重复查询。

### 5. 实验数量与充分性

- **实验组数**：在4个数据集上、对9种不同规模和来源的LLM（例如GPT-5作为前沿大模型，及Qwen2.5-0.5B等小模型）评估了数据最小化的可实现程度，并与模型直接预测进行对比。还分析了不同模型对数据最小化容忍度的差异。
- **充分性**：实验覆盖了开放对话和事实型任务，涉及从大到小多种LLM，充分展现了方法的通用性和模型规模的影响。通过对比搜索基准与模型自身预测，揭示了能力差距，实验设计客观、公平，并包含量化结果（如GPT-5可删减85.7%仍保持质量，而Qwen2.5-0.5B仅19.3%）。

### 6. 论文的主要结论与发现

- **数据最小化可行**：通过构建隐私有序变换空间和优先队列树搜索，能够在不明显损害回答质量的前提下显著降低提示中的个人可识别信息。
- **模型规模效应**：更大的前沿LLM对数据最小化具有更高容忍度，能在更激进的信息删减下保持任务效果；小型模型则容易因信息缺失而质量大幅下降。
- **能力缺口**：直接让LLM自身进行数据最小化时，模型倾向过度抽象，导致仍存在过度分享的问题，说明LLM缺乏“解决任务究竟需要哪些信息”的元认知能力，这不仅是隐私鸿沟，更是能力鸿沟。

### 7. 优点

- **可操作性**：将抽象的数据最小化原则具体化为可计算的搜索问题，为LLM隐私工程提供了实用组件。
- **自动化平衡**：通过树搜索动态寻优，无需人工试错即可找到效用与隐私的最佳折中。
- **可解释性强**：有序变换空间使得隐私保护的程度可控、可解释。
- **评估全面**：覆盖多个领域和不同规模模型，揭示规模化效应与能力缺陷，有重要洞察价值。

### 8. 不足与局限

- **算力需求未明**：大量搜索式查询可能带来高昂推理成本，论文摘要未提及实际开销。
- **隐私度量依赖**：框架的表现高度依赖于个人可识别信息（PII）的检测和变换工具，可能存在漏检或误变换。
- **静态效用评估**：效用阈值的设定可能未考虑用户个性化需求，动态对话场景中的在线优化仍有待研究。
- **任务泛化性**：虽然覆盖了对话和知识任务，但对多轮交互、代码生成等更复杂任务的适用性未经验证。

（完）
