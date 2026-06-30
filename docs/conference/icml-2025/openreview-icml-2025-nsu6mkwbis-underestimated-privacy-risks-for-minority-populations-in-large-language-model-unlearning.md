---
title: Underestimated Privacy Risks for Minority Populations in Large Language Model Unlearning
title_zh: 被低估的隐私风险：大语言模型遗忘中的少数群体
authors: "Rongzhe Wei, Mufei Li, Mohsen Ghassemi, Eleonora Kreacic, Yifan Li, Xiang Yue, Bo Li, Vamsi K. Potluru, Pan Li, Eli Chien"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=NsU6MKwbis"
tags: ["query:priv-sec"]
score: 9.0
evidence: 大语言模型遗忘中少数群体的隐私风险
tldr: 大语言模型遗忘过程的隐私评估通常忽视数据子集的差异，本文发现少数群体面临低估的隐私风险。通过扩展成员推理攻击与遗忘评估框架，证明异常点与少数群体的隐私泄露更严重。标准随机采样评估掩盖了这种不平等，呼吁更细粒度的遗忘后隐私审计。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有 LLM 遗忘评估采用随机采样，可能忽略某些群体更高的隐私风险。
method: 通过设计针对性的成员推理攻击，对比遗忘模型与重训模型在不同子集上的隐私泄露。
result: 少数群体和异常点面临显著更高的隐私泄露，标准评估会低估实际风险。
conclusion: LLM 遗忘评估必须考虑群体差异，以确保公平且全面的隐私保护。
---

## Abstract
Large Language Models (LLMs) embed sensitive, human-generated data, prompting the need for unlearning methods. Although certified unlearning offers strong privacy guarantees, its restrictive assumptions make it unsuitable for LLMs, giving rise to various heuristic approaches typically assessed through empirical evaluations. These standard evaluations randomly select data for removal, apply unlearning techniques, and use membership inference attacks (MIAs) to compare unlearned models against models retrained without the removed data. However, to ensure robust privacy protections for every data point, it is essential to account for scenarios in which certain data subsets face elevated risks. Prior research suggests that outliers, particularly including data tied to minority groups, often exhibit higher memorization propensity which indicates they may be more difficult to unlearn. Building on these insights, we introduce a complementary, minority-aware evaluation framework to highlight blind spots in existing frameworks. We substantiate our findings with carefully designed experiments, using canaries with personally identifiable information (PII) to represent these minority subsets and demonstrate that they suffer at least 20\% higher privacy leakage across various unlearning methods, MIAs, datasets, and LLM scales. Our proposed minority-aware evaluation framework marks an essential step toward more equitable and comprehensive assessments of LLM unlearning efficacy.

---

## 论文详细总结（自动生成）

# 论文总结：《Underestimated Privacy Risks for Minority Populations in Large Language Model Unlearning》

## 1. 核心问题与整体含义
- **研究动机**：大型语言模型（LLM）在训练过程中会记忆大量敏感的人类生成数据，催生了“遗忘”（unlearning）技术的需求。现有的遗忘效果评估通常采用**随机采样**方式选择要删除的数据，然后比较遗忘模型与重新训练模型的成员推理攻击（MIA）表现。
- **核心问题**：这种均匀采样的评估方式可能**掩盖不同数据子集之间的隐私风险差异**。已有研究表明，异常点（outliers），尤其是与少数群体相关的数据，通常具有更高的记忆倾向，因而可能更难以被遗忘。
- **整体含义**：该论文指出，当前LLM遗忘的实证评估存在盲区——少数群体面临的隐私泄露风险被**系统性低估**。为了实现对所有个体都鲁棒的隐私保护，必须引入考虑群体差异的评估框架，从而推动更公平、更全面的遗忘能力测评。

## 2. 论文提出的方法论
- **核心思想**：在原有遗忘评估流程的基础上，补充一个**少数群体感知（minority-aware）的评估框架**，重点关注数据中的特定子集（如包含个人可识别信息PII的少数群体金丝雀样本），测量这些子集的隐私泄露程度。
- **关键技术细节**：
  - 构建**金丝雀样本**（canaries）：注入带有明确个人可识别信息的少数群体代表性数据，作为待遗忘的“少数子集”。
  - 采用**成员推理攻击**（MIA）量化隐私泄露：对比遗忘模型与完全重新训练模型在少数子集上的MIA成功率。
  - 计算**隐私泄露增量**：少数群体相较于随机采样平均隐私泄露的至少高出20%以上，作为风险低估的量化证据。
- **公式/算法流程**（文字概括）：
  1. 选定LLM和数据集，植入少数群体金丝雀样本。
  2. 执行某种LLM遗忘算法，生成遗忘模型。
  3. 针对遗忘模型和重训模型，分别对少数群体子集和随机采样子集执行MIA。
  4. 比较两组子集的MIA成功率差异，揭示少数群体隐私风险更高。
  5. 用此差异评估现有遗忘方法在公平性方面的不足。

## 3. 实验设计
- **数据集/场景**：摘要未列出具体数据集名称，但提到实验在多种数据集、多种LLM规模上进行，并利用含有PII的金丝雀样本模拟少数群体数据子集。
- **Benchmark**：以重新训练模型（不含被删除数据）作为隐私保护的理想上限，MIA攻击成功率越低表示隐私保护越好。
- **对比方法**：
  - **遗忘方法**：多种启发式LLM遗忘方法（具体名称未在摘要中给出）。
  - **评估攻击**：不同的成员推理攻击方法（MIA）。
  - **LLM规模**：不同参数规模的大语言模型。
  - **维度对比**：少数群体子集 vs. 随机采样子集的隐私泄露程度。

## 4. 资源与算力
- 摘要及元数据中**未明确提及**使用的GPU型号、数量、训练时长等算力信息。从实验覆盖多种LLM规模和数据集推断，计算资源需求较大，但具体细节缺失。

## 5. 实验数量与充分性
- **实验组数估计**：根据摘要描述，实验覆盖了**多种遗忘方法、多种MIA攻击、多个数据集、多种LLM规模**，因此实验组合数量较多，形成多维度交叉验证。
- **充分性与客观性**：
  - 足够充分：通过多变量控制（方法、攻击、模型规模）验证结论的稳健性，结果一致显示少数群体隐私泄漏至少高出20%，增强了发现的可信度。
  - 客观公平：采用了标准MIA基准和重新训练模型作为对照，并在相同条件下比较子集，评估体系公正。
  - 潜在局限：未披露具体数据集和遗忘方法名称，无法独立验证可复现性，但从摘要描述来看实验设计合理。

## 6. 主要结论与发现
- 现有LLM遗忘评估采用随机采样会**低估少数群体的隐私风险**。
- 包含少数群体特征（如异常值、PII金丝雀）的数据在遗忘后仍保留更高的成员推理攻击成功率，**隐私泄漏至少比平均水平高20%**。
- 这一发现强调，遗忘效果的评估必须**考虑群体差异**，否则会制造虚假的隐私安全感，对少数群体构成不公平的隐私威胁。
- 论文提出的少数群体感知评估框架是迈向更公平、更全面遗忘评估的关键一步。

## 7. 优点
- **问题识别深刻**：首次明确指出LLM遗忘评估中的群体公平性盲点，将隐私研究与公平性议题结合。
- **方法论简单有效**：在不改变原有遗忘和攻击框架的前提下，仅通过调整评估数据的采样策略，即可揭示隐形风险，易于实施和推广。
- **实验设计扎实**：跨方法、跨攻击、跨数据、跨模型规模的广泛实验，保证了结论的普遍性和鲁棒性。
- **现实意义强**：直接关乎少数群体用户的隐私保护，为后续隐私法规、审计提供新视角。

## 8. 不足与局限
- **摘要信息有限**：未提供数据集、遗忘算法、MIA方法的具体名称，难以评估方法的代表性和覆盖面。
- **金丝雀样本的局限性**：使用合成PII金丝雀可能无法完全复现真实少数群体数据的复杂分布，实际风险可能更高或结构不同。
- **攻击假设限制**：仅评估了基于MIA的隐私泄露，未覆盖其他攻击形式（如属性推理、模型反转），隐私风险的全景仍可能不完整。
- **资源未报告**：缺少计算开销分析，不易判断框架的实用性和推广成本。
- **仍属实证评估**：未提供理论保证，只是对现有遗忘方法在少数群体上的实证风险评估，本质上仍是经验性结论。

（完）
