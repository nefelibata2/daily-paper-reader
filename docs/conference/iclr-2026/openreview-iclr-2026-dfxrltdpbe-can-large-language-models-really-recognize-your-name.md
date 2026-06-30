---
title: Can Large Language Models Really Recognize Your Name?
title_zh: 大型语言模型真的能识别你的名字吗？
authors: "Dzung Pham, Peter Kairouz, Niloofar Mireshghallah, Eugene Bagdasarian, Chau Minh Pham, Amir Houmansadr"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=dfxrltDpBe"
tags: ["query:priv-sec"]
score: 8.0
evidence: 揭示了大语言模型在识别敏感姓名方面的不可靠性，削弱了隐私保护方案
tldr: "针对大语言模型被用于隐私保护但可能无法可靠识别个人身份信息的问题，构建了包含歧义姓名的AMBENCH基准。实验显示，先进LLM和PII工具在AMBENCH上的召回率比常规姓名低20-40%，表明模型存在严重漏识。该基准为评估和改进LLM的隐私保护能力提供了重要工具。"
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 现有的基于LLM的隐私方案假设模型能可靠检测命名实体，但实际可能失效。
method: 构建AMBENCH基准，包含真实但具歧义的姓名，并设计了包含良性提示注入的文本片段。
result: "发现LLM及专用PII检测工具对AMBENCH姓名的召回率下降20-40%，漏识问题严重。"
conclusion: 揭示了LLM在隐私保护中的关键缺陷，强调需要更鲁棒的PII检测方法。
---

## Abstract
Large language models (LLMs) are increasingly being used to protect personal user data. These privacy solutions often assume that LLMs can reliably detect named entities and personally identifiable information (PII). In this paper, we challenge that assumption by revealing how LLMs can regularly overlook broad types of sensitive names even in short text snippets due to ambiguity in the contexts. We construct AMBENCH, a benchmark dataset of seemingly ambiguous yet real entity names designed around the name regularity bias phenomenon and embedded within concise text snippets containing benign prompt injections. Our experiments with state-of-the-art LLMs and specialized PII detection tools show that the recall of AMBENCH names drops by 20--40\% compared to more recognizable names. AMBENCH names are also four times more likely to be ignored in supposedly privacy-preserving LLM-powered text analysis tools adopted in the industry. Our findings showcase blind spots in current LLM-based privacy defenses and call for a systematic investigation into their privacy failure modes.

---

## 论文详细总结（自动生成）

# 论文结构化分析与总结

## 1. 论文的核心问题与整体含义

- **研究动机**：大语言模型（LLM）越来越多地被用于隐私保护任务，例如自动检测并删除用户数据中的姓名等个人身份信息（PII）。然而，这些应用通常基于一个隐含假设——模型能够可靠地识别文本中的命名实体。
- **核心问题**：论文挑战了这一假设，指出 LLM 在面对因上下文歧义而“看似普通”的姓名时会出现系统性漏识，从而严重削弱基于 LLM 的隐私保护方案的有效性。
- **整体含义**：即使是最先进的 LLM 与专用 PII 检测工具，也会因姓名与日常词汇的歧义重叠而大量遗漏真实敏感姓名，这暴露了现有隐私防御的关键盲区。

## 2. 论文提出的方法论

- **核心思想**：设计一个基准测试，专门考察模型在存在“名称规律性偏差”（name regularity bias）时的命名实体识别能力。所谓规律性偏差是指：当一个真实姓名同时也可以被解释为普通单词、短语或常见字符串时，模型倾向于忽略其实体属性。
- **关键技术细节**：
  - 构建了 **AMBENCH** 基准数据集，其中包含看似有歧义但真实存在的姓名。
  - 每个姓名被嵌入**简短的文本片段**中，同时注入**良性的提示（prompt injections）** 以模拟真实应用场景（如 LLM 被要求提取信息或执行隐私过滤）。
  - 数据集构造原则：姓名在上下文中的出现方式既符合自然语言表达，又能触发模型的“非实体”解读，从而测量模型的漏检倾向。
- **评估方式**：通过与传统可识别姓名对比，衡量 AMBENCH 姓名被正确检测出的比例（召回率）变化。

## 3. 实验设计

- **数据集与场景**：
  - **AMBENCH**：本研究构建的专用基准数据集。
  - 对比组：一组更典型、歧义性较低的姓名（作为高可识别性基线）。
  - 测试文本：人工构造的短文本片段，带有提示注入，反映真实隐私检测工具的使用方式（如“请提取以下文本中的姓名”）。
- **对比方法/模型**：
  - 当前最先进的 **大语言模型**（具体模型名称摘要未列出，但明确指 SOTA LLMs）。
  - **专用的 PII 检测工具**（工业界中已采用的、据称能保护隐私的 LLM 驱动文本分析工具）。
- **评估指标**：重点观察姓名检测的 **召回率**（recall）变化。

## 4. 资源与算力

- 论文摘要及提供的元数据中**未明确说明**使用的 GPU 型号、数量、算力规模或训练时长。
- 公开信息不足，无法判断是否有大规模训练需求；AMBENCH 作为评估基准，其构建与实验主要涉及推理而非训练，但具体计算资源消耗仍需查阅原文才能确认。

## 5. 实验数量与充分性

- 摘要中未提及具体的实验组数量或消融实验的详细设置。
- 但核心对比已清晰：
  - **两组姓名类型**：歧义姓名（AMBENCH） vs 常规高可识别姓名。
  - **两类系统**：SOTA LLM vs 专用 PII 检测工具。
  - 结果呈现为量化下降幅度（20-40%）和忽略概率倍数（4倍），表明提供了多角度的统计证据。
- **充分性与公平性**：从描述看，对比设计直接针对前提假设，控制变量在于姓名歧义程度，比较对象涵盖前沿研究与工业系统，逻辑客观。但由于未见详细实验表与统计显著性检验，全面评价需依赖全文。

## 6. 论文的主要结论与发现

- **严重漏检**：在 AMBENCH 上，先进 LLM 与 PII 工具的姓名召回率比处理常规姓名时下降 **20–40%**。
- **高危遗漏**：AMBENCH 姓名被现有“隐私保护”LLM 分析工具忽略的可能性是普通姓名的 **大约四倍**。
- **隐私防护假设不成立**：现有多数 LLM 隐私方案依赖的“模型可稳定检测命名实体”前提存在系统缺陷。
- **呼吁系统调查**：研究揭示了 LLM 隐私保护中的关键失效模式，强调需要开发更鲁棒、能处理歧义实体的 PII 检测方法。

## 7. 优点

- **问题洞察新颖**：跳出了单纯追求准确率的思路，专注于因**上下文歧义**导致的系统性失灵，角度切中实际部署痛点。
- **基准针对性强**：AMBENCH 的构造直指“姓名规律性偏差”现象，具有诊断价值，可用于未来其他模型的鲁棒性测试。
- **实验现实意义高**：测试覆盖了科研前沿的 LLM 和工业界已采用的工具，结论对实践有直接警示作用。
- **启发性强**：为改进隐私保护 LLM 指出了明确方向——不能只依赖表面的实体识别准确率，必须考虑歧义上下文的泛化能力。

## 8. 不足与局限

- **摘要信息有限**：未提供模型名称、PII 工具具体版本、实验规模与统计检验细节，难以判断结论的可复现性与显著性。
- **歧义姓名的覆盖范围**：未说明 AMBENCH 涵盖的姓名数量、语言文化背景（如是否仅限于英文），通用性待验证。
- **仅评估召回率**：未提及精度（precision）或整体 F1 的变化；过度提高召回可能引入误报，隐私方案需权衡。
- **提示注入的泛化性**：良性注入的设计是否会导致过拟合于某些 LLM 的特定行为模式，原文未展开。
- **对抗性考量**：未探讨攻击者是否可能故意构造歧义文本来逃避检测（主动对抗场景），研究停留在被动评估阶段。

（完）
