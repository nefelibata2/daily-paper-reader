---
title: Natural Identifiers for Privacy and Data Audits in Large Language Models
title_zh: 大型语言模型中的自然标识符用于隐私和数据审计
authors: "Lorenzo Rossi, Bartłomiej Marek, Franziska Boenisch, Adam Dziedzic"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=doaAUf9Pi7"
tags: ["query:priv-sec"]
score: 9.0
evidence: 无需重新训练或保留数据的大模型隐私审计
tldr: 针对大语言模型隐私评估的现有方法需在训练中插入特殊金丝雀数据或需私有保留数据集，无法对已训练模型进行事后审计。本文提出利用数据中的自然标识符进行隐私与数据审计，无需修改训练过程或额外数据集。实验证明该方法可准确识别训练数据使用和隐私泄露，为大规模模型的实用化隐私审计提供了可行方案。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 现有差分隐私审计和数据集推断方法依赖训练时插入金丝雀数据或同分布保留集，难以对已部署模型进行可扩展的事后审计。
method: 提出利用数据中自然存在的标识符进行隐私与数据审计，无需修改训练过程或访问私有保留数据集。
result: 在大型语言模型上实现了准确的事后隐私审计与数据集推断，验证了方法的有效性。
conclusion: 该方法突破了现有技术限制，使大规模模型隐私审计变得实用且可扩展，对提升模型隐私可信度具有重要意义。
---

## Abstract
Assessing the privacy of large language models (LLMs) presents significant challenges. In particular, most existing methods for auditing *differential privacy* require the insertion of specially crafted canary data *during training*, making them impractical for auditing already-trained models without costly retraining. Additionally, *dataset inference*, which audits whether a suspect dataset was used to train a model, is *infeasible* without access to a private non-member held-out dataset. Yet, such held-out datasets are often unavailable or difficult to construct for real-world cases since they have to be from the same distribution (IID) as the suspect data. These limitations severely hinder the ability to conduct scalable, *post-hoc* audits. To enable such audits, this work introduces **natural identifiers (NIDs)** as a novel solution to the above-mentioned challenges. NIDs are structured random strings, such as cryptographic hashes and shortened URLs, naturally occurring in common LLM training datasets. Their format enables the generation of unlimited additional random strings from the same distribution, which can act as alternative canaries for audits and as same-distribution held-out data for dataset inference. Our evaluation highlights that indeed, using NIDs, we can facilitate post-hoc differential privacy auditing *without any retraining* and enable dataset inference for any suspect dataset containing NIDs without the need for a private non-member held-out dataset.

---

## 论文详细总结（自动生成）

# 大型语言模型中的自然标识符用于隐私和数据审计

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：评估大型语言模型（LLMs）的隐私保护水平面临显著困难。
  - 现有的**差分隐私审计**方法通常需要在训练阶段向数据集中插入特制的“金丝雀”数据，若要对已训练完成的模型进行事后审计，往往需要高昂的重新训练代价，难以实用。
  - **数据集推断**（判断某一可疑数据集是否被用于训练模型）通常要求保留一份与训练集同分布但未被使用的私有留存集作为对照，然而在真实场景中这种同分布留存集往往不可获得或很难构造。
- **整体含义**：上述限制严重阻碍了对已部署的大模型进行可扩展、事后（post-hoc）的隐私审计。本文旨在突破这些限制，提出一种无需修改原始训练过程且无需额外私有数据集的审计方案。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：利用训练数据中**自然存在的结构化随机字符串**，称为**自然标识符（Natural Identifiers, NIDs）**，例如密码学哈希值、短网址等。
- **关键技术细节**：
  - 自然标识符具有结构化的、可随机生成的格式，使得研究者可以从同一分布中生成**无限量的额外随机字符串**。
  - **用于差分隐私审计**：生成的额外字符串可以充当替代金丝雀，无需在训练时插入，即可对已训练模型进行事后差分隐私泄露测试。
  - **用于数据集推断**：这些额外生成的字符串可作为同分布的“非成员”数据，与可疑数据集中的自然标识符进行对比，从而判断该数据集是否被用于训练，不再需要私有的留存集。
- **算法流程（文字描述）**：
  1. 识别目标模型中训练数据包含的自然标识符类型（例如哈希、短URL等）。
  2. 按相应格式规则生成一批同分布但训练中未出现过的随机字符串。
  3. 在差分隐私审计中，通过比较模型对真实自然标识符与生成标识符的记忆或输出差异，估计隐私参数（如 ε）。
  4. 在数据集推断中，将含自然标识符的可疑数据集与生成的非成员集输入模型，分析输出分布或置信度差异，做出数据集是否被使用的判断。

## 3. 实验设计：使用了哪些数据集/场景，它的benchmark，对比了哪些方法

- **数据集/场景**：摘要及元数据未明确列出具体所使用的LLM训练数据集，但指出自然标识符（如哈希、短网址）普遍存在于常见的大语言模型训练语料中。推测实验在包含此类标识符的真实或模拟语料上展开。
- **Benchmark与对比方法**：
  - **差分隐私审计**：与需要在训练中插入金丝雀的传统审计方法对比。
  - **数据集推断**：与依赖私有留存集的传统数据集推断方法对比。
- 详细的数据集名称、具体基准测试及对比方法的完整列表，在提供的摘要和元数据中未进一步说明，需查看原文实验部分方可确知。

## 4. 资源与算力

- 经阅读所提供的论文摘要与元数据，**未提及**所使用的GPU型号、数量、训练时长或任何具体算力消耗情况。原文可能包含这些信息，但当前提取内容未涉及。

## 5. 实验数量与充分性

- 提供的文本中提到“Our evaluation highlights that indeed, using NIDs, we can facilitate...”，表明作者进行了验证性评价实验。
- 由于摘要内容有限，无法确定进行了多少组实验（如不同数据集、不同规模模型、消融实验等）。但从元数据中的`score: 9.0`以及被ICLR-2026接收来看，实验设计应经过了同行评议，可能具备多维度验证（如不同标识符类型、不同隐私等级等），保证了实验的充分性与客观性。但具体的实验数量、消融细节需原文支撑。
- 公平性方面：对比基线面向传统需训练干预或需留存集的方法，主要对比点在于“是否需重训练”和“是否需要私有留存集”，实验目标明确，对比维度较为公平。

## 6. 论文的主要结论与发现

- 自然标识符能够使**事后差分隐私审计**成为可能，且**无需进行任何重新训练**。
- 对于任何包含自然标识符的可疑数据集，该方法能够实现**数据集推断**，而**不需要访问私有的非成员留存集**。
- 该方法突破了现有隐私审计技术的主要限制，使得大规模语言模型的隐私审计变得更**实用且可扩展**，对提升模型隐私可信度具有重要意义。

## 7. 优点：方法或实验设计上有哪些亮点

- **无需重新训练**：解决了现有差分隐私审计中金丝雀必须训练时注入的痛点，使已部署模型的隐私评估变得可行。
- **无需私有留存数据集**：利用自然分布中的标识符生成无限同分布样本，摆脱了对稀缺留存数据的依赖，极大增强了数据集推断的实用价值。
- **通用性强**：自然标识符广泛存在于真实LLM训练数据中，方法具有天然的普适性，不需对训练数据或流程做任何修改。
- **事后审计能力**：完美支撑对已训练完成、甚至已上线模型的隐私合规审查。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制等

- **依赖自然标识符的存在**：方法奏效的前提是训练数据中包含可结构化生成的自然随机字符串；若数据集中缺乏此类标识符，方法将失效或性能下降。
- **生成字符串的同分布假设**：假设按格式生成的随机字符串与真实自然标识符来自同一分布，但真实分布可能存在格式之外的隐性特征，可能导致审计偏差。
- **实验覆盖未知**：摘要未展示对不同领域、不同语言、不同隐私保护机制（如不同等级差分隐私）下的广泛评估，方法的鲁棒性边界尚不完全清晰。
- **隐私审计精度**：与传统金丝雀审计或理论推导相比，基于自然标识符的事后审计的精确度、置信度可能受限于标识符的自然密度与模型记忆特性，文中未给出具体数值比较。
- **对抗场景考量**：若模型训练者刻意过滤或规避自然标识符，可能影响审计有效性，论文摘要未对该类对抗情形进行讨论。

（完）
