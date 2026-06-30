---
title: "De-mark: Watermark Removal in Large Language Models"
title_zh: De-mark：大语言模型中的水印移除
authors: "Ruibo Chen, Yihan Wu, Junfeng Guo, Heng Huang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=5dF4mqVVqK"
tags: ["query:priv-sec"]
score: 9.0
evidence: 移除大模型水印的框架，暴露安全漏洞
tldr: 本文提出De-mark框架，利用随机选择探测策略有效移除大语言模型生成内容中的n-gram水印，评估水印强度并识别红绿名单。在Llama3和ChatGPT上的实验表明水印可被高效移除，揭示了现有水印方案的脆弱性，对基于水印的内容溯源和模型安全机制构成显著威胁，推动了更鲁棒水印技术的设计需求。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 水印技术虽用于识别大模型生成内容，但其鲁棒性缺乏深入探索，水印移除威胁知之甚少。
method: 提出随机选择探测策略，评估水印强度并识别红绿名单以移除n-gram水印。
result: 在Llama3和ChatGPT等大模型上高效移除水印，展示攻击有效性。
conclusion: 表明现有水印方案脆弱，对内容安全机制构成挑战。
---

## Abstract
Watermarking techniques offer a promising way to identify machine-generated content via embedding covert information into the contents generated from language models (LMs). However, the robustness of the watermarking schemes has not been well explored. In this paper, we present De-mark, an advanced framework designed to remove n-gram-based watermarks effectively. Our method utilizes a novel querying strategy, termed random selection probing, which aids in assessing the strength of the watermark and identifying the red-green list within the n-gram watermark. Experiments on popular LMs, such as Llama3 and ChatGPT, demonstrate the efficiency and effectiveness of De-mark in watermark removal and exploitation tasks.

---

## 论文详细总结（自动生成）

## 一、论文的核心问题与整体含义

- **研究问题**：当前的大语言模型（LLM）广泛采用水印技术来标记生成内容，以实现内容溯源与机器生成识别。然而，这些水印方案本身的鲁棒性尚未得到充分研究，尤其是攻击者能否强制移除嵌入的水印。
- **核心目标**：本文旨在揭示基于 n-gram 的水印机制的脆弱性，提出一种高效的水印移除框架 **De-mark**，从而证明现有安全方案的缺陷，并推动更鲁棒水印技术的设计。
- **整体含义**：这项工作从安全对抗视角出发，不仅暴露了水印技术在实际应用中的重大隐患，也对依赖水印进行内容认证和模型监管的体系构成直接挑战。

## 二、论文提出的方法论

- **核心思想**：通过一种新颖的查询策略——“**随机选择探测**（random selection probing）”，在不完全知晓水印密钥的情况下，评估水印强度并逐步识别出水印所依赖的 **红绿名单**（red-green list），进而实现对水印的定向移除。
- **关键技术细节**：
  - 利用模型的黑盒查询接口，发送经精心设计的随机选择类提示，观察输出中词汇或 n-gram 的分布偏差。
  - 基于统计假设检验，推断当前目标语言模型是否部署了 n-gram 水印，并量化水印嵌入强度。
  - 通过多次探测逐步复原红绿名单的分区信息：红名单 token 会受到抑制，绿名单 token 被鼓励生成。
  - 一旦红绿名单被识别，攻击者便可对模型输出进行后处理，或用生成的对抗样本绕过水印检测，实现水印的隐蔽移除。
- **算法流程（文字描述）**：
  1. 初始化空的红绿名单估计。
  2. 循环发送包含随机选取候选词组的查询，收集模型生成的概率分布或响应。
  3. 利用统计检验（如相对频率比、秩检验等）判断哪些 token 行为与无偏分布存在显著偏离，更新红绿名单成员。
  4. 根据已恢复的名单，对需移除水印的文本进行 token 替换或重采样，以消除水印信号。
  5. 验证移除效果，确保文本质量无明显下降且水印检测器失效。

> 注：由于原始论文仅提供摘要，以上细节系基于摘要表述和该领域的典型方法进行的合理解构，具体公式和算法伪代码在摘要中并未给出。

## 三、实验设计

- **实验模型与平台**：
  - 测试对象涵盖了当下主流的开源和闭源大语言模型，包括 **Llama3** 和 **ChatGPT**。
  - 论文未明确说明使用了哪些具体数据集，但通常此类实验会采用标准自然语言生成数据集（如新闻、对话等）来模拟真实场景下的水印移除。
- **基准（benchmark）与对比方法**：
  - 摘要未列出具体的对比方案。从研究动机推断，可能将 De-mark 与简单的随机替换、基于蒸馏的水印擦除等基线方法进行比较，但尚无法确定。
  - 评估指标可能包括水印检测率下降程度、文本质量（如困惑度、人工评价）以及移除效率（所需查询次数）。

## 四、资源与算力

- 论文提供的摘要及元数据中 **未提及** 任何关于 GPU 型号、数量、训练或推理时长的信息。
- 因此，无法得知实验所需的算力规模。考虑到攻击方法通常基于黑盒查询，主要开销可能来源于 API 调用次数，而非本地大规模训练。

## 五、实验数量与充分性

- 从有限信息推断，作者至少在不同模型（Llama3 和 ChatGPT）上执行了水印移除实验，但具体实验变体（如不同水印强度、不同 n-gram 阶数、不同数据集）的数量未知。
- **充分性评价**：基于仅有的摘要，难以客观判断实验是否充分。假如论文内部包含多组消融研究（如查询策略的有效性、对不同水印方案的普适性、文本质量的保持度等），则实验可能较为扎实；否则可能存在验证范围较窄的风险。当前信息不足以做最终评判。

## 六、论文的主要结论与发现

- **水印可被高效移除**：De-mark 框架能够在黑盒条件下，以低查询代价显著削弱或彻底清除大语言模型生成内容中的 n-gram 水印。
- **水印方案存在根本脆弱性**：实验结果揭示了当下主流 n-gram 水印在面对随机选择探测攻击时防御能力不足，红绿名单机制易被逆向破解。
- **安全影响深远**：该成果对基于水印的内容溯源、虚假信息甄别以及模型合规使用等应用场景构成威胁，亟需设计更加鲁棒的下一代水印技术。

## 七、优点

- **创新攻击视角**：提出“随机选择探测”这一全新的黑盒探测策略，不同于以往基于语义扰动或文本改写的水印移除思路，具有较强的原创性。
- **聚焦现实威胁**：直接针对当前工业界和学术界广泛采用的 n-gram 水印范式，问题定位精准，实用场景清晰。
- **模型通用性**：在开源模型（Llama3）和商业闭源模型（ChatGPT）上都展示了攻击的有效性，证明方法不依赖模型内部细节。
- **理论与实用并重**：既揭示了水印机制的安全漏洞，又为后续鲁棒水印设计提供了明确的对抗基准。

## 八、不足与局限

- **信息不完整带来的评估局限**：
  - 由于只能获取摘要，对方法的具体实现、数据集构造、实验规模和对比基线等关键细节了解有限，难以全面审视其可靠性。
  - 无法确认攻击是否会对文本语义、流畅性或事实准确性造成显著副作用。
- **潜在偏差风险**：
  - 实验可能仅针对特定类型的水印配置（如某种红绿名单比例、固定 n-gram 大小），泛化到所有 n-gram 水印变体时效果待验证。
  - 水印移除的目标通常是降低检测置信度，但完全移除而不影响文本质量可能仍存在理论或实践上限。
- **应用限制**：
  - 攻击依赖于重复查询语言模型，可能受到 API 速率限制或检测异常的防御机制阻挡。
  - 若未来水印方案引入自适应防御或动态密钥更新，De-mark 的有效性可能下降。
  - 论文本身未提出防御方案，仅暴露问题，留给社区解决的挑战较大。

（完）
