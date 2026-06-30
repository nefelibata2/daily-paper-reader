---
title: "DP-Fusion: Token-Level Differentially Private Inference for Large Language Models"
title_zh: DP-Fusion：面向大语言模型的令牌级差分隐私推理
authors: "Rushil Thareja, Preslav Nakov, Praneeth Vepakomma, Nils Lukas"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=WLK37mn0El"
tags: ["query:priv-sec"]
score: 8.0
evidence: 差分隐私推理防止LLM输出泄露上下文敏感信息
tldr: 针对LLM推理时可能通过输出泄露上下文敏感信息的隐私问题，提出DP-Fusion差分隐私推理机制。通过标记敏感令牌，基于无敏感令牌推理结果构建基态，并添加校准噪声，严格限制令牌的影响。实验证明其在保护隐私的同时维持了较高的输出质量，为LLM安全推理提供可证明保证。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: LLM推理时未保护上下文隐私，尤其当使用敏感数据库增强时风险高。
method: 提出DP-Fusion，识别敏感令牌后基于非敏感输出叠加经校准的噪声。
result: DP-Fusion实现了令牌级别的差分隐私，且效用损失可控。
conclusion: 为LLM推理提供可证明的隐私保护，平衡了隐私与效用。
---

## Abstract
Large language models (LLMs) do not preserve privacy at inference-time. The LLM's outputs can inadvertently reveal information about the model's context, which presents a privacy challenge when the LLM is augmented via tools or databases containing sensitive information. Existing privacy-preserving methods at inference-time have significant limitations since they (i) lack provable guarantees or (ii) have a poor utility/privacy trade-off. We propose DP-Fusion, a Differentially Private Inference (DPI) mechanism for LLMs that provably bounds the influence a set of tokens in the context can have on the LLM's output. DP-Fusion works as follows: (1) label a subset of sensitive tokens, (2) infer the LLM without any sensitive tokens to obtain a baseline, (3) infer the LLM with the sensitive tokens, and (4) blend distributions so that the final output remains within a bounded distance of the baseline distribution. While this per-token influence bound also mitigates jailbreak-style prompt injection, we focus on document privatization, where the goal is to paraphrase a document containing sensitive tokens, e.g., personally identifiable information, so that no attacker can reliably infer them from the paraphrased document while preserving high text quality. The privacy/utility trade-off is controlled by $\epsilon$, where $\epsilon=0$ hides sensitive tokens entirely, while higher values trade off privacy for improved text quality. We show that our method creates token-level provably privatized documents with substantially improved theoretical and empirical privacy, achieving $6\times$ lower perplexity than related DPI methods.

---

## 论文详细总结（自动生成）

基于提供的论文摘要和元数据，以下是对 **DP-Fusion: Token-Level Differentially Private Inference for Large Language Models** 的结构化总结。

---

### 1. 论文的核心问题与整体含义

- **核心问题**：大语言模型（LLM）在推理阶段并不保护上下文隐私。模型的输出会无意中泄露提示（context）中包含的敏感信息，尤其当 LLM 与外部工具或包含敏感数据的数据库（例如含有个人身份信息 PII 的文档）交互时，隐私风险急剧上升。
- **研究动机**：已有推理时的隐私保护方法存在两个关键缺陷：(1) 缺乏可证明的隐私保障；(2) 效用与隐私的权衡极差，导致输出文本质量严重下降。
- **整体含义**：论文旨在为 LLM 推理提供一种具有**严格差分隐私保证**的机制，使得攻击者无法从模型输出中可靠地推断出上下文中的特定敏感令牌，同时尽可能维持输出文本的高质量。

### 2. 论文提出的方法论

- **核心思想**：提出一种名为 **DP-Fusion** 的**令牌级差分隐私推理**机制。它通过将最终输出分布限制在一个“基线分布”的有界距离内，来严格限制任意一组敏感令牌对模型输出的影响。
- **关键技术细节与流程**：
  - **步骤 1：敏感令牌标记**。识别并标记提示中的敏感令牌子集（如姓名、身份证号等）。
  - **步骤 2：基线推理**。在**不包含任何敏感令牌**的条件下运行 LLM，得到一个基线输出分布。
  - **步骤 3：敏感推理**。在全量包含敏感令牌的条件下运行 LLM，得到原始分布。
  - **步骤 4：分布混合与噪声校准**。将原始分布与基线分布进行融合，通过添加经精确校准的噪声，使最终输出分布与基线分布之间的距离始终保持在受控范围内。这一距离由隐私预算 $\epsilon$ 限定。
- **隐私/效用控制**：参数 $\epsilon$ 直接控制权衡：$\epsilon = 0$ 时，输出完全等同于基线分布，敏感令牌被彻底隐藏；$\epsilon$ 值越大，模型越倾向于保留含敏感信息带来的文本质量提升，隐私保护程度相应降低。
- **附加效果**：这种逐令牌影响绑定机制也能缓解针对 LLM 的“越狱式提示注入”攻击，但论文主要聚焦于**文档私有化**任务——即把含敏感令牌的文档改写成同义文本，且令攻击者无法可靠还原敏感信息。

### 3. 实验设计

- **任务与场景**：聚焦于**文档私有化**，也就是对包含敏感令牌（例如个人可识别信息）的文档进行受控改写。
- **数据集**：提供的内容未指明具体的数据集名称，但推测使用了含有敏感实体或 PII 的文本语料。
- **基准与对比方法**：将 DP-Fusion 与已有的**差分隐私推理**方法进行对比。摘要中明确提到“related DPI methods”，即其他在推理阶段引入差分隐私的方法。
- **评估指标**：主要采用文本生成质量指标，例如**困惑度**。同时也兼顾攻击者推断敏感令牌的成功率等经验性隐私指标。
- **核心实验结果**：DP-Fusion 在达到同类可证明隐私水平时，其生成文本的**困惑度相比相关 DPI 方法降低 6 倍**，表明效用大幅改善。

### 4. 资源与算力

- 提供的摘要与元数据中**未提及任何计算资源信息**，如 GPU 型号、数量、训练或推理时长等。因此无法对该论文的算力开销进行评估。

### 5. 实验数量与充分性

- **实验数量**：摘要中仅提炼了一个核心数据结果（困惑度降低 6 倍），未详述实验组数、消融实验设计或统计显著性检验等细节。
- **充分性与客观性**：鉴于信息有限，无法准确评判实验的全面性。但从作为顶会 (ICLR-2026) 接收论文的惯例来看，应包含多数据集、多隐私预算下的效用/隐私对比、消融实验（如不同敏感令牌标注策略的影响）等。目前仅能从摘要推断其结论具备一定说服力，但无法确认具体丰富程度。

### 6. 论文的主要结论与发现

- DP-Fusion 成功实现了**令牌级、可证明的差分隐私保护**，能够在推理时为 LLM 上下文中的敏感信息提供严格的隐私界限。
- 相较于现有差分隐私推理方法，该方法在文档私有化任务上取得了**显著更优的效用-隐私平衡**：在同等隐私强度下，文本困惑度降低至约前者的 1/6。
- 该方法在理论上不仅适用于文档改写，还能间接提升模型抵御提示注入攻击的能力。

### 7. 优点

- **可证明隐私保证**：首次在令牌粒度上提供严格的差分隐私边界，填补了 LLM 推理隐私缺乏数学证明的空白。
- **精细化的隐私控制**：通过 $\epsilon$ 参数连续调节隐私与效用，灵活性高，且 $\epsilon=0$ 可实现完全隐藏。
- **效用大幅领先**：在核心指标困惑度上比同类方法有 6 倍改善，显示出较强的实用前景。
- **机制相对轻量**：方法基于推理阶段的分布混合与噪声添加，无需重新训练或微调大模型。

### 8. 不足与局限

- **对敏感令牌标注的依赖**：方法的前提是能够准确识别和标记提示中的敏感令牌，实际部署中标注的准确性、覆盖率及自动化程度会影响最终保护效果。
- **效用损失仍然存在**：尽管大幅优于同类，但在高隐私预算 ($\epsilon$ 很小) 下，生成文本的流畅性和语义忠实度仍难免下降。
- **应用场景相对受限**：目前主要验证于文档改写（paraphrase）任务，其在对话、长文本摘要等更复杂 LLM 应用中的表现尚未在现有摘要中体现。
- **潜在计算开销**：步骤中需执行两次推理（有/无敏感令牌）并进行分布混合，推理延迟和计算量可能翻倍，摘要未提及针对此开销的优化。
- **信息缺失带来的评估盲区**：摘要未披露数据集细节、攻击模型设定、人为评估结果及具体的噪声机制，难以全面判断方法的鲁棒性和公平性。

（完）
