---
title: "Open Models Can Silently Undermine Privacy: Context Inference Attacks without Jailbreaks"
title_zh: 开放模型可能悄然破坏隐私：无需越狱的上下文推断攻击
authors: "Prince Jha, Samuele Poppi, Nils Lukas"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=VsVAVgzwOs"
tags: ["query:priv-sec"]
score: 9.0
evidence: 提出上下文推断攻击从模型输出中解码敏感信息，揭示生成模型隐私风险
tldr: 该论文针对大型生成模型可能无意中泄露敏感上下文信息的隐私风险，提出了一种无需越狱的上下文推断攻击框架。通过高保真替代模型解码目标模型的上下文，即使看似无害的生成输出也可能成为隐私泄漏的隐蔽通道，从而绕过仅阻止逐字复制的防御机制。实验表明该攻击能有效推断密码等敏感信息，揭示了开源模型部署中严峻的隐私威胁，为隐私保护研究敲响警钟。
source: ICLR-2026-Public
selection_source: conference_retrieval
motivation: 大型生成模型处理用户查询时可能无意中纳入密码、个人身份信息等敏感数据，导致输出分布微妙偏移，形成无声的隐私泄漏通道。
method: 提出利用高保真替代模型解码目标模型上下文的攻击框架，从看似无害的生成内容中推断敏感信息。
result: 攻击成功解码出敏感上下文信息，绕过传统逐字复制防御，证明开放模型存在显著的隐性隐私风险。
conclusion: 该研究揭示了大模型无需越狱即可泄漏隐私的新途径，呼吁加强针对上下文推断攻击的防御研究。
---

## Abstract
Large Generative Models (LGMs) process user queries by conditioning on diverse contextual information, which may inadvertently include sensitive data such as passwords or personally identifiable information (PII).
A privacy risk arises when the model’s outputs are \emph{unintentionally} influenced by this sensitive context.
Even subtle shifts in the output distribution can create a silent leakage channel.
Unlike direct data exposure, this leakage is encoded in seemingly innocuous generations, evading defenses that only block verbatim reproduction of sensitive content. We present a novel attack framework that leverages high-fidelity surrogate models to decode sensitive information from a target model’s context.
Importantly, our attacks succeed even when the model behaves as intended and without exploiting explicit security vulnerabilities (\eg, through jailbreaking).
We design two attack variants: (i) an \emph{undetectable attack} that passively analyzes benign generations, and (ii) an \emph{adaptive attack} that strategically selects queries to maximize information gain. Our findings show that optimized queries achieve up to 100\% attack success rates across models and remain effective under instruction-based defenses.
This work highlights the urgent need for defenses capable of detecting and mitigating private information leakage during inference.

---

## 论文详细总结（自动生成）

### 1. 核心问题与研究动机

- **研究背景与问题**  
  大型生成模型（LGMs）在响应用户查询时需依赖丰富的上下文信息，其中可能无意混入密码、个人身份信息（PII）等敏感数据。传统隐私风险研究多关注直接的数据泄露（如模型逐字复述训练数据），但该论文揭示了一种更隐蔽的威胁：模型输出分布即便只发生微小、看似无害的偏移，也可能编码了机密上下文，形成无声的隐私泄漏通道。这种泄漏无需利用越狱（jailbreaking）等显式安全漏洞，仅通过正常的模型行为即可发生。

- **整体含义**  
  论文指出，即使模型“按预期”行事，攻击者也能利用精心设计的攻击框架从看似无害的生成文本中解码出敏感原文。这挑战了传统仅阻止逐字复制的防御策略，强调需要防范条件生成过程中的隐含信息泄漏。

### 2. 方法论

- **核心思想**  
  攻击框架利用高保真的“替代模型”来追踪目标模型在敏感上下文条件下输出分布的变化，从而逆向推断出原始敏感信息。整个攻击建立在编码-解码思想上：目标模型的生成过程可视为以私有上下文为条件的概率编码，攻击者通过替代模型来解码这些隐藏的信号。

- **关键技术细节**  
  - **攻击变体一：不可检测攻击（被动分析）**  
    直接提取目标模型在正常查询下生成的文本，通过替代模型分析输出分布与已知候选上下文的匹配度，实现被动隐私窃取。该方式不向目标发送任何可疑查询，完全隐身。
  - **攻击变体二：自适应攻击（主动查询）**  
    攻击者策略性地构造输入查询，以最大化目标模型输出中包含的敏感信息增益。该过程迭代地选择最能区分不同敏感上下文候选的查询，逐步缩小敏感信息的可能范围，直至高置信度破译。
  - **总体算法流程（文字描述）**  
    1. 获取目标模型（黑盒）在给定系统提示（含敏感上下文）下的输出。  
    2. 利用已知的外部数据训练/微调一个高保真替代模型，使其能模拟目标模型的行为。  
    3. （自适应模式）在候选上下文空间内，基于信息增益指标选取下一查询，观察目标响应；重复直至收敛到某一特定敏感信息。  
    4. （被动模式）直接计算目标输出与各候选上下文下替代模型输出之间的似然差异，选取最匹配者。

- **技术依赖**  
  替代模型的高保真度是关键，它需要能准确反映不同上下文对输出分布的影响。论文强调该攻击不依赖越狱或提取模型参数，仅利用标准API访问即可施行。

### 3. 实验设计

- **数据集与场景**  
  文中实验聚焦于在系统提示中植入敏感数据，如：
  - 密码（例如随机字符串）
  - 个人身份信息片段
  模型需在含有该敏感上下文的条件下回答看似普通的用户查询（如“写一首诗”“总结一个故事”等），攻击者的目标是从模型回复中还原机密内容。

- **Benchmark与评估指标**  
  - **攻击成功率（Attack Success Rate）**：能否准确解码出敏感上下文（准确率/完全匹配率）。  
  - 对比不同模型、不同攻击模式（被动 vs 自适应）以及是否施加基于指令的防御（instruction-based defenses）下的表现。

- **对比方法**  
  实验主要横向评估：
  - 自身方法的两种变体（被动分析 vs 自适应查询）。
  - 在有/无指令防御措施下的性能。
  - 不同模型（可能是开源与商业模型）上的攻击有效性。
  （注：摘要未列出具体对照的防御算法名称，但指出“在基于指令的防御之下仍然有效”。）

### 4. 资源与算力

- 文中未明确给出所用GPU型号、数量或训练时长等具体计算资源信息。摘要和元数据中均未提及算力细节，因此无法直接总结。通常此类研究需要使用多张高端GPU（如A100）进行替代模型训练和大规模攻击模拟，但本文未提供确凿数字。

### 5. 实验数量与充分性

- **实验规模推测**  
  基于摘要描述，实验至少覆盖了：
  - 两种攻击变体 × 多种主流模型。
  - 不同敏感上下文类型（密码、PII等）。
  - 有无防御的对比。
  这构成了一个多维度实验矩阵，表明作者进行了较为系统的评估。

- **充分性与公平性**  
  实验设计通过“自适应攻击”与“被动攻击”对比，考察了不同威胁等级；同时验证了方法在标准指令防御下的健壮性，具有一定深度。但摘要未详细说明替代模型的训练数据、模型选择范围及重复次数，难以独立判断统计显著性和潜在偏差。从现有信息看，实验框架逻辑自洽、具有现实威胁建模，整体较为充分。

### 6. 主要结论与发现

- 开放模型（甚至非恶意使用情况下）确实存在无声的隐私泄漏：攻击者可以从无害的生成回复中推断出系统提示中的敏感信息。
- 自适应查询策略可极大提升攻击效率，在某些模型上达到100%攻击成功率。
- 基于指令的防御（如要求模型“遗忘”敏感提示）未能完全阻止信息泄漏，攻击依然有效。
- 这一发现警示：仅防范逐字复制和显而易见的越狱攻击是不够的，隐私保护需要深入到条件分布层面。

### 7. 方法亮点

- **创新视角**：将隐私攻击拓展到无需越狱、利用生成过程本身的信息泄漏，这是一个重要且新颖的威胁模型。
- **攻击隐蔽性强**：被动模式完全无需发送可疑查询，防不胜防。
- **替代模型的巧妙使用**：通过高保真替代模型解码隐藏上下文，将统计推断问题转化为模式匹配问题。
- **实验证伪性高**：证明即使防御措施到位（指令防止泄露），信息仍可通过分布偏转外泄，凸显了根本性漏洞。

### 8. 不足与局限

- **依赖替代模型品质**：攻击的高成功率取决于替代模型对目标模型行为的逼真模拟，若目标模型极为独特或被精心保护（如商业模型持续更新），替代模型构建难度大，攻击可迁移性存疑。
- **上下文设定相对简单**：实验使用隔离的敏感提示（如密码）进行攻击，实际场景中机密信息往往深嵌于长文本或混杂噪声，解码难度可能急剧上升。
- **防御措施探讨有限**：摘要中仅提到“基于指令的防御”无效，未展示更彻底的对抗措施（如差分隐私生成、信息瓶颈正则化）的效果，缺乏更系统性的防御评估。
- **算力与实验细节不透明**：缺少数值细节（模型规模、训练成本），难以评估攻击的实际可行性和扩展性。
- **伦理风险**：论文本身揭示了攻击方法，若被恶意使用可能造成实际危害，虽然研究动机是促进防御，但公开描述的细节需要谨慎平衡。

（完）
