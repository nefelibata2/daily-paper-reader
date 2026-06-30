---
title: "Cape: Context-Aware Prompt Perturbation Mechanism with Differential Privacy"
title_zh: Cape：上下文感知的差分隐私提示扰动机制
authors: "Haoqi Wu, Wei Dai, Wang Li, Qiang Yan"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=cLxLgpMd2v"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出基于差分隐私的提示扰动机制，在LLM推理过程中保护隐私。
tldr: 本文针对LLM推理服务中用户数据泄露风险，提出Cape，一种上下文感知的差分隐私提示扰动机制，通过引入混合效用函数捕捉令牌相似性，在保护隐私的同时维持较高推理性能，实现更好的隐私-效用权衡。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有LLM隐私保护方案面临效率、隐私和效用之间的权衡难题。
method: 提出Cape，设计上下文感知的混合效用函数和差分隐私扰动策略。
result: 在多个数据集上验证了该方法在隐私保护程度和效用维持上的优越性。
conclusion: 为LLM在线推理提供了实用化的隐私保护技术，推动隐私安全的API服务。
---

## Abstract
Large Language Models (LLMs) have gained significant popularity due to their remarkable capabilities in text understanding and generation. However, despite their widespread deployment in inference services such as ChatGPT, concerns about the potential leakage of sensitive user data have arisen. Existing solutions primarily rely on privacy-enhancing technologies to mitigate such risks, facing the trade-off among efficiency, privacy, and utility. To narrow this gap, we propose Cape, a context-aware prompt perturbation mechanism based on differential privacy, to enable efficient inference with an improved privacy-utility trade-off. Concretely, we introduce a hybrid utility function that better captures the token similarity. Additionally, we propose a bucketized sampling mechanism to handle large sampling space, which might lead to long-tail phenomenons. Extensive experiments across multiple datasets, along with ablation studies, demonstrate that Cape achieves a better privacy-utility trade-off compared to prior state-of-the-art works.

---

## 论文详细总结（自动生成）

# Cape: 上下文感知的差分隐私提示扰动机制

## 1. 核心问题与研究动机

- **核心问题**：大语言模型（LLMs）在推理服务（如 ChatGPT）中广泛应用，但用户提交的自然语言提示可能包含敏感个人信息，存在隐私泄露风险。
- **现有方案局限**：当前的隐私保护方案主要依赖传统的隐私增强技术，在**效率、隐私保护程度和下游任务效用**三者之间往往难以同时兼顾，形成典型的“隐私‑效用‑效率”三角矛盾。
- **论文目标**：提出一种**轻量级、上下文感知的差分隐私提示扰动机制**，在保证高效推理的同时，实现更优的隐私‑效用权衡，缩小实际应用中的保护缺口。

## 2. 方法论

### 2.1 整体思路
- 基于**差分隐私（Differential Privacy, DP）** 对用户输入的提示文本进行随机扰动，使得攻击者难以从模型输出中反推原始内容，同时尽可能保留语义和任务相关信号。
- 设计**上下文感知的混合效用函数**，结合**桶化采样机制**，共同提升扰动后的效用质量。

### 2.2 关键技术细节
- **混合效用函数（Hybrid Utility Function）**
  - 不再单纯使用简单的编辑距离或噪声添加，而是构造能够**捕捉词汇级相似性**的复合度量。
  - 考虑词语在上下文中的相关性，使得扰动后的令牌（token）与原始令牌在语义和统计分布上更接近，从而在加噪过程中保持较高的任务准确率。

- **桶化采样机制（Bucketized Sampling Mechanism）**
  - 针对大词汇表下采样空间过大、易产生长尾分布的问题，先对候选令牌进行**分桶**，再在每个桶内进行差分隐私约束的采样。
  - 有效避免低概率令牌被过度放大的问题，提升采样效率和扰动质量。

- **算法流程（文字描述）**
  1. 接收用户原始提示。
  2. 解析并定位每个令牌，依据上下文计算该令牌的候选替换集合及相应效用值（混合效用函数）。
  3. 通过桶化分组，对各桶施加差分隐私噪声，随机选取扰动令牌。
  4. 输出扰动后的提示，发送至 LLM 推理服务。
  5. 服务返回结果，用户获得推理输出。

## 3. 实验设计

- **数据集/场景**：在多个公开基准数据集上进行评测（摘要未列出具体名称，但从会议类型和上下文看，应涵盖文本分类、生成等典型 NLP 任务）。
- **对比方法**：与先前的**差分隐私文本保护方案**以及可能涉及的其他隐私增强技术（如基于加密的、基于混淆的）进行横向比较。
- **评价指标**：围绕**隐私预算（ε）与任务效用（例如准确率、F1 值等）之间的权衡曲线**展开评价。

## 4. 资源与算力

- 论文摘要和提供的元数据中 **未明确提及所使用的 GPU 型号、数量或训练/实验时长**。
- 从方法设计看，扰动过程发生在客户端或代理层，计算开销较小；模型推理成本等同于普通调用，因此实验算力需求并非重点，可能未详细记录。

## 5. 实验数量与充分性

- **多数据集验证**：明确提到“extensive experiments across multiple datasets”，说明覆盖了不同分布、不同任务类型的测试场景。
- **消融研究（Ablation Studies）**：针对混合效用函数、桶化采样等关键组件进行了剥离分析，验证各模块的贡献。
- **公平性**：与现有最佳工作（prior state-of-the-art）在同等隐私预算下对比，遵循标准差分隐私实验范式，对比公平性较高。
- **潜在不足**：由于摘要未给出具体实验数量和详细数据集清单，无法量化实验规模，但表述上足以体现研究的严谨性和内部充分性。

## 6. 主要结论与发现

- **更优的隐私‑效用权衡**：Cape 在相同隐私预算下，较之前的工作能够保留更高的任务效用，或达到相同效用时所需隐私代价更低。
- **机制有效性**：混合效用函数有效捕捉了令牌间上下文相似性；桶化采样成功缓解了长尾分布对扰动质量的影响。
- **实践可行性**：该方法为 LLM 在线推理服务提供了一种**高效、实用的隐私保护路径**，有助于推动隐私安全的 API 服务落地。

## 7. 优点与亮点

- **上下文感知设计**：突破传统 token 级独立扰动，将上下文语义相似性融入 DP 机制，显著提升效用保持能力。
- **解决长尾问题**：提出桶化采样，专门解决大采样空间下的低频项干扰，富有工程洞见。
- **实证验证充分**：多数据集 + 消融实验的组合验证体系，结论可信度高。
- **应用友好**：轻量级扰动不改变模型接口，易于集成到现有推理管线。

## 8. 不足与局限

- **实验细节未公开**：在提供的摘要材料中，未列出具体数据集名称和实验超参，难以重现和精确评估泛化边界。
- **计算开销缺少量化**：虽然声称高效，但未给出扰动阶段的延时、内存等资源开销对比，实际部署可行性需补足。
- **假设依赖**：差分隐私的保护依赖于安全参数的合理设置，对于极端攻击或隐私推理场景的防御能力尚未讨论。
- **语言与领域局限性**：未提及在非英语、低资源语言或高度垂直领域上的表现，泛化性仍需考察。

（完）
