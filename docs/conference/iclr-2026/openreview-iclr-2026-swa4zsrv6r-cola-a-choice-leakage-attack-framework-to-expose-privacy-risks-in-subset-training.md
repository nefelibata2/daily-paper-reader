---
title: "CoLa: A Choice Leakage Attack Framework To Expose Privacy Risks In Subset Training"
title_zh: "CoLa: 揭示子集训练隐私风险的选择泄露攻击框架"
authors: "Qi Li, Cheng-Long Wang, Yinzhi Cao, Di Wang"
date: 2025-09-02
pdf: "https://openreview.net/pdf?id=SWA4zSrv6R"
tags: ["query:priv-sec"]
score: 8.0
evidence: 语言模型子集训练中的选择泄露暴露新的隐私风险
tldr: 本文挑战了子集训练减少隐私风险的普遍假设，揭示数据选择过程中的包含/排除决策会引入新的隐私攻击面，并提出选择泄露攻击框架CoLa，通过侧信道元数据泄露敏感信息，表明子集训练并非隐私免责。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 子集训练被广泛用于大规模机器学习，但普遍认为训练更少样本能降低隐私风险，本文质疑此假设。
method: 提出CoLa选择泄露攻击框架，利用数据选择过程的侧信道元数据捕获泄露的敏感信息。
result: 实验表明，子集训练中的选择数据会泄露敏感信息，颠覆了隐私减少的直觉。
conclusion: 子集训练并不能免费提供隐私保护，需要重视数据选择环节的新隐私风险。
---

## Abstract
Subset training, where models are trained on a carefully chosen portion of data rather than the entire dataset, has become a standard tool for scaling modern machine learning. From coreset selection in vision to large-scale filtering in language models, these methods promise scalability without compromising utility. A common intuition is that training on fewer samples should also reduce privacy risks. In this paper, we challenge this assumption. We show that subset training is not privacy free: the very choices of which data are included or excluded can introduce new privacy surface and leak more sensitive information. Such information can be captured by adversaries either through side-channel metadata from the subset selection process or via the outputs of the target model. To systematically study this phenomenon, we propose CoLa (Choice Leakage Attack), a unified framework for analyzing privacy leakage in subset selection. In CoLa, depending on the adversary’s knowledge of the side-channel information, we define two practical attack scenarios: Subset-aware Side-channel Attacks and Black-box Attacks. Under both scenarios, we investigate two privacy surfaces unique to subset training: (1) Training-membership MIA (TM-MIA), which concerns only the privacy of training data membership, and (2) Selection-participation MIA (SP-MIA), which concerns the privacy of all samples that participated in the subset selection process. Notably, SP-MIA enlarges the notion of membership from model training to the entire data–model supply chain. Experiments on vision and language models show that existing threat models underestimate the privacy risks of subset training: the enlarged privacy surface not only retains training membership leakage but also exposing selection membership, extending risks from individual models to the broader ML ecosystem.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：子集训练（subset training）已成为大规模机器学习中的标准手段，例如视觉模型的核心集选择（coreset selection）和语言模型的大规模数据过滤。人们普遍认为，用更少的样本训练模型应当能降低隐私风险，因为模型接触的数据量更小。
- **核心挑战**：本文质疑这一常见直觉，指出子集训练并不是“隐私免责”的——数据选择过程中哪些样本被包含或排除，本身就会引入新的隐私攻击面。
- **问题含义**：数据选择决策会泄露敏感信息，被攻击者通过侧信道元数据或模型输出捕获。论文系统性地揭示了这一全新的隐私风险维度，将隐私关注的边界从模型训练阶段扩展到了“整个数据–模型供应链”中的选择参与环节。

### 2. 论文提出的方法论

- **核心框架 CoLa（Choice Leakage Attack）**：一个统一的隐私泄露分析框架，专门用于量化子集选择过程中的信息泄露。
- **攻击场景**：根据攻击者对侧信道信息的掌握程度，定义两种实际攻击场景：
  - **子集感知侧信道攻击（Subset‑aware Side‑channel Attacks）**：攻击者能够获取子集选择过程的元数据。
  - **黑盒攻击（Black‑box Attacks）**：攻击者只能通过目标模型的输出来推断选择信息。
- **两种隐私表面**：CoLa 在以上两种场景中，分别研究子集训练独有的两类隐私泄露：
  1. **训练成员推理攻击（TM‑MIA）**：只关注训练数据成员本身的隐私，即某个样本是否被用于最终模型训练。
  2. **选择参与推理攻击（SP‑MIA）**：关注所有参与子集选择过程的样本的隐私，不论该样本最终是否被选中训练。SP‑MIA 将传统成员推理的“成员”概念从模型训练扩大到了整个数据选择供应链，覆盖更广泛的样本。
- **关键技术思路**：利用选择过程中留存或可观测的侧信道信号（如选择算法的中间状态、时序特征等）以及模型输出分布差异，构建推理器来区分“参与选择”与“未参与选择”的样本，从而暴露原本未被重视的隐私风险。

### 3. 实验设计

- **数据集与场景**：实验覆盖视觉模型和语言模型两类典型场景，具体数据集在摘要中未指明，但根据上下文应包含主流图像分类数据集和语言建模/过滤数据集。
- **基准（Benchmark）对比**：将 CoLa 框架下的攻击与现有威胁模型进行比较，现有模型低估了子集训练的隐私风险。文中强调，增大后的隐私表面不仅保留了训练成员泄露，还额外暴露了选择成员泄露。
- **对比方法**：对比的应该是传统的成员推理攻击（仅针对最终训练集）以及在无子集选择侧信道假设下的攻击方法，旨在说明 SP‑MIA 带来的新增风险。

### 4. 资源与算力

- 提供的论文摘要和元数据中**没有明确说明**所使用的 GPU 型号、数量或训练时长等算力细节。若要精确评估资源消耗，需查阅论文完整版中的实验配置部分。

### 5. 实验数量与充分性

- **实验数量推测**：从摘要看，实验覆盖视觉和语言两类模态，并在两种攻击场景（侧信道与黑盒）和两种隐私表面（TM‑MIA 与 SP‑MIA）下进行验证，至少形成 2×2 的实验矩阵。此外可能会有不同子集选择策略（如随机、基于重要性等）的消融实验。
- **充分性评估**：多模态、多场景、多攻击目标的设置使得实验具有较强的全面性。对比基线针对现有威胁模型，直接回应了“子集训练降低隐私风险”的传统观念，客观性较好。但由于缺乏具体数值和统计检验细节，我们无法判断实验的统计显著性和结论的稳健程度。

### 6. 论文的主要结论与发现

- 子集训练并不能免费提供隐私保护，数据选择过程本身就构成严重的隐私泄露渠道。
- SP‑MIA 将隐私风险的边界从训练集扩大到整个数据选择环节，现有威胁模型严重低估了这一风险。
- 在视觉和语言模型上的实验表明，增大后的隐私表面不仅保留了训练成员泄露，还进一步暴露了选择参与信息，这将隐私风险从单个模型扩展到了更广泛的机器学习生态系统中。

### 7. 优点

- **问题角度新颖**：首次系统质疑“少样本即更安全”的隐私直觉，挖掘出数据选择环节这一被忽视的攻击面。
- **框架统一且实用**：CoLa 框架同时容纳侧信道和黑盒两种攻击场景，并清晰区分 TM‑MIA 和 SP‑MIA 两类隐私危害，结构清晰、易扩展。
- **隐私风险重定义**：将成员推理从模型训练阶段拓展到整个数据–模型供应链，这一定义对未来隐私评估标准具有重要参考价值。
- **跨模态验证**：在视觉和语言任务上均进行实验，增强了结论的普适性。

### 8. 不足与局限

- **实验细节缺失**：目前仅基于摘要分析，缺少对数据集规模、模型结构、攻击成功率具体数值等关键信息的了解，无法评估攻击的实际危害程度。
- **攻击假设的实用性**：侧信道攻击场景要求攻击者获取子集选择的元数据，在现实中并非总能满足；黑盒攻击是否对复杂模型仍有效，也需更多验证。
- **防御策略缺失**：论文重在揭示风险，但未提及可能的缓解措施或防御机制，实践中若不能提供防护方向，其影响会受到限制。
- **选择策略的多样性**：子集选择方法多种多样（主动学习、去重、质量过滤等），不同策略下的泄露程度可能存在显著差异，现有实验是否覆盖足够多的选择算法尚不清楚。

（完）
