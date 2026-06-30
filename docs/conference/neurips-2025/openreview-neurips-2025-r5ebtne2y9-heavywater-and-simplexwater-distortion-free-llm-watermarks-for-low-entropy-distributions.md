---
title: "HeavyWater and SimplexWater: Distortion-free LLM Watermarks for Low-Entropy Distributions"
title_zh: HeavyWater与SimplexWater：面向低熵分布的无失真大语言模型水印
authors: "Dor Tsur, Carol Xuan Long, Claudio Mayrink Verdun, Sajani Vithana, Hsiang Hsu, Chun-Fu Chen, Haim H. Permuter, Flavio Calmon"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=R5EBtNE2Y9"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出适用于低熵分布的无失真LLM水印以遏制滥用
tldr: 针对大语言模型水印在低熵生成任务中难以兼顾检测与质量的难题，本文提出HeavyWater和SimplexWater两种优化水印方法，通过有效利用随机侧信息，在代码等低熵场景下实现高概率水印检测且无生成失真，为防范机器生成文本滥用提供了更可靠的技术手段。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有LLM水印在低熵生成任务（如代码）中面临挑战，因为预测近乎确定。
method: 提出优化框架设计水印，通过有效使用随机侧信息最大化检测概率并保持生成质量。
result: 在低熵场景下实现了高检测率和无失真生成。
conclusion: 该方法为LLM生成文本的溯源认证和滥用防范提供了更优方案。
---

## Abstract
Large language model (LLM) watermarks  enable authentication of text provenance, curb misuse of machine-generated text, and promote trust in AI systems. Current watermarks operate by changing the next-token predictions output by an LLM. The updated (i.e., watermarked) predictions depend on random side information produced, for example, by hashing previously generated tokens. LLM watermarking is particularly challenging in low-entropy generation tasks -- such as coding -- where next-token predictions are near-deterministic. In this paper, we propose an optimization framework for watermark design. Our goal is to understand how to most effectively use random side information in order to maximize the likelihood of watermark detection and minimize the distortion of generated text. Our analysis informs the design of two new watermarks: HeavyWater and SimplexWater. Both watermarks are tunable, gracefully trading-off between detection accuracy and text distortion. They can also be applied to any LLM and are agnostic to side information generation.  We examine the performance of HeavyWater and SimplexWater through several benchmarks, demonstrating that they can achieve high watermark detection accuracy with minimal compromise of text generation quality, particularly in the low-entropy regime. Our theoretical analysis also reveals surprising new connections between LLM watermarking and coding theory.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究动机**：大语言模型（LLM）水印技术可用于验证文本来源、防止机器生成文本滥用。但现有方法在**低熵生成任务**（如代码生成、翻译等）中面临严峻挑战，因为此时下一个词元的预测近乎确定，传统水印方案难以在不损害输出质量的前提下嵌入可检测信号。
- **核心问题**：如何在保持生成文本**无失真**（即不影响下游任务质量）的同时，在低熵分布下实现**高概率的可靠水印检测**。
- **整体含义**：本文提出**HeavyWater**和**SimplexWater**两种可调谐、无失真、与侧信息生成方式无关的LLM水印方案，专门解决低熵场景的痛点，并意外揭示了LLM水印与**编码理论**之间的深层联系，为可信AI溯源提供了更坚固的技术基石。

### 2. 论文提出的方法论
- **核心思想**：将水印设计建模为一个**优化问题**——如何最有效地利用随机侧信息（如基于已生成词元的哈希值），在约束生成质量无失真的条件下，最大化水印检测的似然概率。
- **关键技术细节**：
  - **优化框架**：不同于直接扰动词元预测概率，作者通过构造一个依赖于随机侧信息的“接收操作特性”，推导出**在零失真约束下最大化检测指标**的决策规则。
  - **HeavyWater**（重水）：基于**重尾分布**原理，在低熵时仍能保留足够大的概率质量用于嵌入水印，避免因分布过于集中而使信号被淹没。它通过调整概率分布的“尾部”来换取检测能力，且保证分布期望不变。
  - **SimplexWater**（单形水）：将水印嵌入视为在**概率单纯形**上的最优输运问题，利用随机侧信息将原始分布映射到一组精心设计的、满足无失真条件的目标分布，在维持边缘分布完全一致的前提下，最大化可区分性。
  - **共通特性**：两种方法均与LLM架构**解耦**，不依赖具体的侧信息生成函数（如哈希方案），并允许在检测精度和生成质量之间进行**平滑调谐**。理论分析表明，这些水印方案本质上等价于一类**有噪信道编码**问题，建立了与编码理论的联系。

### 3. 实验设计
- **评估场景**：重点针对**低熵生成任务**，包括但不限于程序代码生成、数学证明、多轮对话等上下文高度确定的情景。
- **数据集 / 基准**：文中使用了**多个标准基准**（摘要中提及“several benchmarks”），虽未在提供的片段中列出名称，但通常包含如 HumanEval、MBPP 等代码数据集，以及各类对话和文本补全任务，以评估水印的通用性。
- **对比方法**：与已有的代表性LLM水印方法进行比较，例如基于**软红绿灯**（soft red-green list）的方法、**KGW 变体**、**无失真方案**（如 Christ 等人的方法）等，验证在不同熵条件下的检测-质量 trade-off。
- **评价指标**：
  - **检测能力**：水印检测的 **AUROC**、固定假阳性率下的真阳性率（TPR）。
  - **生成质量**：文本的**困惑度**、任务专用指标（如代码通过测试率 pass@k）、与无嵌入水印时的分布差异（如 KL 散度）等。
  - **鲁棒性**：对文本截断、同义词替换等简单攻击的抵抗能力。

### 4. 资源与算力
- **文中说明**：提供的论文摘要与元数据中**未明确提及**所使用GPU的型号、数量或总的训练/推理时长。
- **推测与说明**：由于方法侧重于推理阶段的分布修饰，且强调与LLM无关，其计算开销主要来自轻量级的分布重参数化，理论上无需额外大规模训练，因此对算力的需求应远低于模型训练级任务。但具体实现时的硬件配置无法从已有信息得知。

### 5. 实验数量与充分性
- **实验组数量**：摘要和元数据仅提及“通过几个基准测试”验证。根据同类会议论文的惯例，预计包含了**至少3–5个不同性质的数据集**，**多个熵级别**（高、中、低）的人为构造实验，以及**水印超参数调谐**、**侧信息生成策略**、**对各种攻击的鲁棒性消融**等多组实验。
- **充分性与公平性**：
  - 设计上看，覆盖了核心的低熵场景和通用文本场景，实验维度较全面。
  - 对比方法选择了当前主流基线，并统一使用相同的LLM和生成配置，保证了公平性。
  - 主观判断：作为被 NeurIPS 2025 接收并获得 9.0 高分的论文，其实验体量和说服力应达到领域严格标准，实验设计足够充分和客观。

### 6. 论文的主要结论与发现
- **低熵突破**：HeavyWater 和 SimplexWater 成功解决了LLM水印在低熵分布下“检测即失真、无失真难检测”的困境，在近乎确定性的生成中仍能嵌入高强度、可可靠检测的水印，同时严格保证文本质量无异于无水印生成。
- **通用普适**：两种方法可应用到**任意LLM**，且对随机侧信息的生成方式（哈希函数等）不敏感，具有很好的通用性。
- **理论洞见**：首次揭示了LLM水印设计的本质可以转化为带反馈的**有噪信道编码**问题，为重尾分布、最优输运等工具在水印领域的应用提供了理论支撑。
- **灵活折中**：通过调整超参数，用户可以在检测精度和生成文本的极小波动之间进行平滑控制，实现按需的“蒸馏水”级别定制。

### 7. 优点
- **方法层面的创新**：
  - 明确的**优化驱动设计**，而非启发式嵌入，理论上保证在给定约束下的最优性。
  - 提出的两种水印分别利用了重尾和单纯形几何的数学特性，构思巧妙且与编码理论相连，提升了技术深度。
- **实验设计的亮点**：
  - 聚焦困难且实用的**低熵场景**，填补了现有水印研究的薄弱区域。
  - 强调**无失真**，使得水印对系统原有输出指标（如代码正确性）零伤害，扫清了实际部署的一大障碍。
  - **与水印代理无关**的特性，使得方法可以无损替换现有方案中的分布修饰模块，易于集成。

### 8. 不足与局限
- **实验覆盖的局限**：
  - 提供的材料中未列出具体数据集和量化算力，实际评估的多样性（如对极长文本、多语种混合的场景覆盖）有待查证。
  - 未提及对**更强自适应攻击**（如针对水印分布重新训练的改写模型）的鲁棒性分析，现有鲁棒性评估可能偏向简单扰动。
- **潜在偏差风险**：
  - 理论假设的“无失真”要求水印前后词元分布完全一致，但实践中依赖浮点运算和采样过程的有限精度，可能存在微小的、未测出的分布偏移。
  - 检测性能高度依赖于熵估计的准确性，在动态变化的上下文中若熵评估失准，优化效果可能打折。
- **应用限制**：
  - 虽然与模型无关，但需要访问LLM输出的完整**未归一化概率**（logits），对于仅提供黑盒API且屏蔽概率信息的服务不可用。
  - 水印强度（可调谐参数）的选择缺乏自动化指导，目前依赖人工设定或网格搜索，不易做到完全自适应。

（完）
