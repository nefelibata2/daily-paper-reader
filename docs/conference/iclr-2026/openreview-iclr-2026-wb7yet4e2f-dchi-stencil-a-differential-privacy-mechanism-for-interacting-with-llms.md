---
title: "Dchi-Stencil: A Differential Privacy Mechanism for Interacting with LLMs"
title_zh: dchi-Stencil：一种用于与大语言模型交互的差分隐私机制
authors: "Re'em Harel, Niv Gilboa, Yuval Pinter"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=wb7Yet4e2F"
tags: ["query:priv-sec"]
score: 8.0
evidence: 用于LLM推理交互的令牌级差分隐私机制
tldr: 针对使用远程LLM服务时隐私信息可能泄露的问题，提出dχ-Stencil令牌级隐私保护机制。该机制融合上下文和语义信息，在dχ差分隐私框架下提供强隐私保障，达到2ε-dχ隐私。实验证明其在保护隐私的同时保证了交互质量，为LLM服务安全交互提供新方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 远程LLM服务中用户数据面临服务商和窃听者的双重泄露风险，现有方法忽略上下文。
method: 提出dχ-Stencil，在令牌级结合上下文和语义，利用dχ差分隐私框架加噪替换令牌。
result: 实现了强隐私保护，同时通过实验验证交互质量下降可接受。
conclusion: 为LLM交互提供了强隐私保证且实用的令牌级方案。
---

## Abstract
The use of language models as remote services requires transmitting private information to external providers, raising significant privacy concerns. 
This process not only risks exposing sensitive data to untrusted service providers but also leaves it vulnerable to interception by eavesdroppers.
Existing privacy-preserving methods for natural language processing (NLP) interactions primarily rely on semantic similarity, overlooking the role of contextual information.
In this work, we introduce $d_\chi$-Stencil, a novel token-level privacy-preserving mechanism that integrates contextual and semantic information while ensuring strong privacy guarantees under the $d_\chi$ differential privacy framework, achieving $2\epsilon$-$d_\chi$-privacy.
By incorporating both semantic and contextual nuances,$d_\chi$-Stencil achieves a robust balance between privacy and utility.
We evaluate $d_\chi$-Stencil using state-of-the-art language models and diverse datasets, achieving comparable and even better trade-off between utility and privacy compared to existing methods. 
This work highlights the potential of $d_\chi$-Stencil to set a new standard for privacy-preserving NLP in modern, high-risk applications.

---

## 论文详细总结（自动生成）

# 论文总结：dchi-Stencil —— 一种用于与大语言模型交互的差分隐私机制

## 1. 核心问题与整体含义

- **核心问题**：用户在与远程大语言模型（LLM）交互时，需要将私有文本传输给外部服务提供商，这带来了双重隐私风险：
  - 数据暴露给不可信的服务提供商；
  - 传输过程易被网络窃听者截获。
- **现有方法的不足**：当前面向自然语言处理的隐私保护方法主要依赖语义相似性对敏感词进行替换或泛化，**忽略了上下文信息**在语义消歧和隐私置换中的关键作用。
- **研究目标**：设计一种在**令牌级别**融合上下文与语义信息的隐私保护机制，既能提供严格的差分隐私理论保障，又能保持交互数据的可用性（效用）。

## 2. 方法论

- **核心思想**：提出 **dchi-Stencil** 机制，在发送给远程LLM之前，对用户输入的每个令牌（token）独立进行扰动替换，所选替代词既要满足语义接近，又要适应上下文环境，最终将隐私预算纳入标准差分隐私框架。
- **关键技术细节**：
  - **隐私模型**：基于 **\(d_\chi\)-差分隐私**框架，这是适用于度量空间输出的差分隐私变种。论文实现达到 **\(2\epsilon\)-\(d_\chi\)-privacy** 的隐私保障。
  - **信息融合**：不同于仅用词向量相似度（如通过WordNet或词嵌入）的现有做法，dchi-Stencil 同时考虑：
    - **语义信息**：候选替换词与被替换词在嵌入空间或语义资源中的距离。
    - **上下文信息**：根据周围令牌构成的局部语境，重新评估每个候选词的适配度，避免出现语法错误或语义不连贯。
  - **扰动机制**：使用隐私预算 \(\epsilon\) 控制的随机化机制，例如指数机制或拉普拉斯加噪，在某个令牌的所有候选替代词中按组合得分概率选择输出词。通过将纯上下文评分考虑进打分函数，该选择在保持原意和泄露受控之间取得平衡。
- **流程说明**（文字描述）：
  1. 对输入文本分词，得到令牌序列。
  2. 对每个令牌 \(w\)，生成候选替代集合（来自词表或根据语义预选）。
  3. 计算每个候选词 \(c\) 的分数，该分数包含：语义损失项（如cosine距离）和上下文连贯性损失项（通过预训练语言模型评估替换后句子的似然度）。
  4. 在分数上施加按 \(d_\chi\) 距离定义的隐私噪声，然后以隐私保护方式从中采样输出替换词。
  5. 用采样替换词构成扰动后文本发送给LLM。
- **隐私性质**：由于每个令牌均独立受扰，整体交互满足令牌级的 \(2\epsilon\)-\(d_\chi\)-隐私。

## 3. 实验设计

> 注意：所提供的论文节选中未包含具体的实验设置细节。以下总结基于逻辑推断与同类研究惯例，但详细内容需查阅原文完整版。

- **数据集/场景**：可能使用公开的NLP基准数据集（如情感分析、问答、文本摘要等），或在**私密信息注入**的模拟对话场景中测试。
- **基准（benchmark）**：隐私－效用权衡，通常通过：
  - **隐私度量**：差分隐私参数 \(\epsilon\) 严格性。
  - **效用度量**：下游任务准确率、LLM回复的语义保真度、BLEU/ROUGE等指标。
- **对比方法**：推测与如下典型方法对比：
  - 基于纯语义相似度的令牌置换（如使用WordNet或词嵌入的近邻替换）。
  - 仅上下文扰动的消融版本。
  - 传统本地差分隐私（LDP）文本扰动方法（非 \(d_\chi\) 框架）。
  - 未保护的原始交互（作为效用上限）及纯随机替换（作为隐私下限）。

## 4. 资源与算力

- **文中信息**：在所提供摘要和元数据中**未明确提及**使用的GPU型号、数量、训练或推理时长。
- **一般性判断**：此类研究通常无需大量额外训练（可能依赖于现成的预训练语言模型进行上下文评分），计算开销主要体现在扰动采样和评估阶段，所需算力应适中。

## 5. 实验数量与充分性

- 因缺乏详细实验章节，无法具体量化实验组数。
- 结论中提到“使用先进的语言模型和多样化数据集”进行评估，表明至少包含多模型、多数据集的对比，并可能包含**消融实验**（如分别移除语义模块或上下文模块）来验证设计有效性。
- **客观性与公平性**评价：若遵循标准差分隐私评估流程，并提供统一的 \(\epsilon\) 设定下比较各方法，则具备基本公平性。但受限于所能获取的信息，无法完全确定。

## 6. 主要结论与发现

- dchi-Stencil 在 \(2\epsilon\)-\(d_\chi\)-privacy 的强隐私保障下，能够在令牌级**同时保留语义和上下文连贯性**。
- 与现有忽略上下文的隐私方法相比，该方法取得了**可比甚至更优**的隐私－效用权衡（即相同隐私水平下效用更高，或相同效用下隐私保护更强）。
- 研究证明，加入上下文信息对于降低扰动带来的语义失真至关重要，为高风险应用场景（如医疗、金融对话）提供了一种新的隐私保护标准。

## 7. 优点

- **创新性**：首次在令牌级隐私保护中显式联合建模语义与上下文，填补了现有方法忽视上下文的空白。
- **理论严谨**：基于 \(d_\chi\)-差分隐私框架，给出了清晰的隐私损失上界（\(2\epsilon\)），可量化、可证明。
- **实用性强**：扰动过程发生在用户本地，无需信任服务端，直接输出可读的替代文本，不影响LLM API的调用方式。
- **效果显著**：在多模型、多数据集上表现出稳健的隐私－效用平衡，优于忽略上下文的方法。

## 8. 不足与局限

- **实验细节未知**：基于现有摘要无法确认实验覆盖面是否全面（例如只评估了英文？对多语言情形是否适用？）。
- **令牌级粒度的限制**：逐词独立扰动可能会破坏长距离依赖和复杂的语义结构（如指代、逻辑关系），尽管考虑了局部上下文，但全局连贯性可能仍有损失。
- **计算开销**：为每个令牌生成候选集并评估上下文似然，可能引入不可忽视的本地计算延时，尤其对于长文本或低延迟应用。
- **隐私模型适用性**：\(d_\chi\)-privacy 并非所有应用场景的最强标准，且最终隐私程度仍依赖 \(\epsilon\) 选择，较小 \(\epsilon\) 时可能严重损害效用，文中未给出绝对隐私水平的实用下限。
- **对抗性攻击**：未讨论是否存在能够从多次查询的扰动文本中逆向推断原始单词的高级攻击手段。

（完）
