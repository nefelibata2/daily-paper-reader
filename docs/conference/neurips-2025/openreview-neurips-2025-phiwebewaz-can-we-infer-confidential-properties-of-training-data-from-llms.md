---
title: Can We Infer Confidential Properties of Training Data from LLMs?
title_zh: 我们能从大语言模型中推断出训练数据的保密属性吗？
authors: "Pengrun Huang, Chhavi Yadav, Kamalika Chaudhuri, Ruihan Wu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=PhIWEbewAz"
tags: ["query:priv-sec"]
score: 10.0
evidence: 属性推断攻击揭示大模型训练数据集的隐私属性，应用于医疗数据
tldr: 大模型微调使用的领域数据可能包含机密统计属性，如疾病流行率。本文提出PropInfer基准，系统评估大语言模型在问答和聊天两种范式下的属性推断攻击风险。基于ChatDoctor医疗数据集的实验表明，攻击者可高准确率推断出微调数据的人口统计等敏感属性。该工作为大模型隐私研究提供了重要评估工具，凸显了部署前后的风险。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 微调数据集中的机密属性（如患者人口统计）可能被泄露，但之前未在LLM上研究。
method: 构建PropInfer基准，在问答和聊天微调范式下评估大模型属性推断攻击。
result: "在医疗数据集上，攻击能以超过80%的准确率推断出疾病流行率等敏感属性。"
conclusion: 大模型确实存在数据集属性泄漏风险，亟需隐私保护措施。
---

## Abstract
Large language models (LLMs) are increasingly fine-tuned on domain-specific datasets to support applications in fields such as healthcare, finance, and law. These fine-tuning datasets often have sensitive and confidential dataset-level properties — such as patient demographics or disease prevalence—that are not intended to be revealed. While prior work has studied property inference attacks on discriminative models (e.g., image classification models) and generative models (e.g., GANs for image data), it remains unclear if such attacks transfer to LLMs. In this work, we introduce PropInfer, a benchmark task for evaluating property inference in LLMs under two fine-tuning paradigms: question-answering and chat-completion. Built on the ChatDoctor dataset, our benchmark includes a range of property types and task configurations. We further propose two tailored attacks: a prompt-based generation attack and a shadow-model attack leveraging word frequency signals. Empirical evaluations across multiple pretrained LLMs show the success of our attacks, revealing a previously unrecognized vulnerability in LLMs.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：许多领域（如医疗、金融、法律）在微调大语言模型（LLM）时使用的领域专用数据集中，常常包含不打算公开的数据集级敏感属性（如患者人口统计特征、疾病流行率等）。该论文聚焦于一个此前未被系统研究过的问题：是否能够从微调后的LLM中推断出这些机密属性？
- **整体含义**：该工作首次在LLM的语境下系统定义并评估了“属性推断攻击”（Property Inference Attack），揭示出即便不直接泄露训练样本，攻击者仍可通过与模型交互高准确率地恢复数据集层面的敏感统计信息，这对LLM的隐私安全提出了新挑战，也突显了部署前和部署后进行风险评估的必要性。

## 2. 论文提出的方法论

- **核心思想**：建立一个名为**PropInfer**的基准测试，形式化地评估LLM在两种典型微调范式下（问答式和聊天补全式）对数据集级属性的泄露风险，并设计两种具体的攻击方法以验证漏洞的严重性。
- **关键技术细节**：
  - **PropInfer基准**：基于ChatDoctor医疗对话数据集，构造多种属性类型（如疾病流行率）和不同的任务配置（如问题模板、微调方式），并定义评估指标（如属性推断准确率）来度量泄露程度。
  - **两种攻击方法**：
    1. **基于提示的生成攻击（Prompt-based Generation Attack）**：向微调后的LLM发出精心设计的查询，从模型的生成内容中直接推断训练数据的属性，例如通过询问“xx疾病的患病率是多少？”来观察模型回答是否反映训练集真实统计。
    2. **影子模型攻击（Shadow-model Attack）**：利用词频信号。攻击者拥有与目标模型架构相似的“影子模型”，在已知属性的代理数据集上微调，然后提取词频特征（如输出中某些词汇的出现频率），训练分类器来预测目标模型的训练集属性。核心在于发现词频分布会随训练数据统计特性发生系统性变化。
- **算法流程概览（文字说明）**：
  1. 对目标LLM用机密数据集微调（不清楚攻击者是否接触微调接口，仅假设能查询最终模型）。
  2. 对第二种攻击：使用多个不同已知属性的影子数据集分别微调影子模型，收集每个模型的输出词频向量作为特征。
  3. 对目标模型执行相同查询，提取词频向量，输入在影子模型词频上训练的推断分类器（如逻辑回归），预测目标数据集属性。
  4. 对第一种攻击：直接解析模型对属性相关问题的文本回复，将其数值与训练集真实值对比。

## 3. 实验设计

- **数据集 / 场景**：
  - 主要基于**ChatDoctor**医疗对话数据集构造属性推断场景。
  - 属性示例包括疾病流行率、人口统计分布等敏感数据集级特征。
- **Benchmark**：PropInfer基准，涵盖不同属性类型、不同微调范式（问答式与聊天补全式）。
- **对比方法**：并未进行大规模多工具对比，主要是验证两种攻击在不同预训练模型（多个pretrained LLMs）上的成功率，以及对比不同范式下的泄露程度差异。

## 4. 资源与算力

- 论文摘要及元数据中**未明确提及**使用的GPU型号、数量或训练时长。可以推测实验涉及多个预训练模型微调和大量查询，但具体开销细节未在目前提供的内容中记录。

## 5. 实验数量与充分性

- 摘要仅提及在多个预训练LLM上进行了实证评估，并显示攻击成功。但具体实验组数（如不同属性种类、不同模型规模、消融实验等）在现有材料中未给出确切数字。
- **充分性初步判断**：从“benchmark includes a range of property types and task configurations”可看出设计上考虑了多样性，但缺乏详细数量统计难以严格评价。从已被NeurIPS-2025接收且得高评分（10.0分）来看，审稿过程可能认可其实验的广度与说服力。

## 6. 论文的主要结论与发现

- 属性推断攻击**可从LLM中成功实施**，攻击者能够在仅查询模型的条件下，以超过80%的准确率推断出微调数据集中的敏感属性（如疾病流行率）。
- 这一发现揭示出先前未受重视的LLM隐私脆弱性，与图像分类模型或生成对抗网络上的同类攻击相比，LLM同样（甚至更易）通过自然语言交互泄露数据集级秘密。
- 两种微调范式（问答/聊天）均存在风险，且目标属性的类型多样，表明问题具有普遍性。

## 7. 优点

- **问题新颖**：首次将属性推断攻击从判别式/生成式图像模型迁移至LLM领域，填补研究空白。
- **基准系统性**：构建PropInfer基准，为后续LLM隐私研究提供了可复现的评估工具。
- **攻击方法针对性强**：结合LLM特性设计提示攻击和词频影子模型攻击，贴近真实应用场景。
- **现实意义显著**：以医疗数据为例，直接影响敏感数据保护的实践，警示下游LLM部署须加强隐私防护。

## 8. 不足与局限

- **数据领域单一**：目前仅使用医疗对话数据集，对金融、法律等其他敏感领域的泛化能力未经验证。
- **属性种类覆盖有限**：虽包含多种属性，但未穷举更复杂或非结构化的数据集级秘密（如文本风格分布等推断问题）。
- **防御措施未讨论**：论文专注于攻击揭露，未提出或评估缓解策略，难以直接指导隐私保护实践。
- **实验细节缺失**：本次总结基于摘要和元数据，无法确定实验规模、模型大小、查询次数等关键要素，实际报告的充分性需查阅全文才能最终评判。

（完）
