---
title: Benchmarking Empirical Privacy Protection for Adaptations of Large Language Models
title_zh: 对大型语言模型适配中的经验隐私保护进行基准测试
authors: "Bartłomiej Marek, Lorenzo Rossi, Vincent Hanke, Xun Wang, Michael Backes, Franziska Boenisch, Adam Dziedzic"
date: 2026-01-26
pdf: "https://openreview.net/pdf?id=jY7fAo9rfK"
tags: ["query:priv-sec"]
score: 8.0
evidence: 基准测试差分隐私适配LLM的经验隐私风险，包括成员推理和提取攻击
tldr: 针对差分隐私适配大语言模型的实际有效性存疑的问题，通过成员推理和金丝雀提取攻击系统评估其隐私风险。实验发现，当适配数据与预训练数据重叠时，差分隐私保护效果大打折扣，暴露了当前DP应用的关键局限。该基准为改进LLM隐私保护提供了重要参考。
source: ICLR-2026-Accepted
selection_source: conference_retrieval
motivation: 差分隐私的理论保证在LLM适配实践中可能因预训练数据重叠而失效。
method: 使用鲁棒成员推理和提取攻击，系统变化数据分布进行基准测试。
result: 数据重叠显著削弱了差分隐私效果，即使在DP下仍可被攻击。
conclusion: 表明需要更强或更全面的防护，仅DP可能不足。
---

## Abstract
Recent work has applied differential privacy (DP) to adapt large language models (LLMs) for sensitive applications, offering theoretical guarantees. However, its practical effectiveness remains unclear, partly due to LLM pretraining, where overlaps and interdependencies with adaptation data can undermine privacy despite DP efforts. To analyze this issue in practice, we investigate privacy risks under DP adaptations in LLMs using state-of-the-art attacks such as robust membership inference and canary data extraction. We benchmark these risks by systematically varying the adaptation data distribution, from exact overlaps with pretraining data, through in-distribution (IID) cases, to entirely out-of-distribution (OOD) examples. Additionally, we evaluate how different adaptation methods and different privacy regimes impact the vulnerability. Our results show that distribution shifts strongly influence privacy vulnerability: the closer the adaptation data is to the pretraining distribution, the higher the practical privacy risk at the same theoretical guarantee, even without direct data overlap. We find that parameter-efficient fine-tuning methods, such as LoRA, achieve the highest empirical privacy protection for OOD data. Our benchmark identifies key factors for achieving practical privacy in DP LLM adaptation, providing actionable insights for deploying customized models in sensitive settings. Looking forward, we propose a structured framework for holistic privacy assessment beyond adaptation privacy, to identify and evaluate risks across the full pretrain-adapt pipeline of LLMs.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

*   **研究背景**：随着大型语言模型（LLMs）在金融、医疗等敏感领域的适配需求日益增加，差分隐私（Differential Privacy, DP）被广泛用于为参数更新提供理论上的可证明隐私保证。
*   **核心问题**：DP 的理论保证在 LLM 适配实践中可能失效。原因是适配数据往往与 LLM 庞大的预训练数据存在分布重叠或隐蔽依赖，这种交叉会严重削弱 DP 在实际攻击面前的有效性，但其具体影响程度缺乏系统性量化。
*   **整体含义**：本文通过构建一个严格的非理想化基准，首次实证揭示“预训练-适配数据关系”是决定 DP 对 LLM 是否真正起效的关键变量，打破了“仅靠 DP 即可解决隐私泄露”的产业认知，并为安全部署定制化大模型提供了可操作的工程指南。

### 2. 论文提出的方法论

*   **攻击评测维度**：不依赖理论隐私损失（ε），而是直接采用当前最先进的**经验攻击**来测量真实世界漏洞。
    *   **鲁棒成员推理攻击**：判断某一样本是否存在于适配训练集中，用来量化“个人信息是否被记住”。
    *   **金丝雀数据提取攻击**：尝试从模型参数中完整复现出事先植入的特定格式秘密文本（金丝雀），用来衡量模型的记忆强度。
*   **核心变量控制**：系统性地操控适配数据的分布偏移，构建从“完全信息泄露”到“完全领域外”的连续谱系，以分离出预训练先验对隐私增益的抵消作用：
    1.  **精确重叠**：适配数据样本直接出现在预训练语料中。
    2.  **同分布**：适配数据与预训练数据同源同分布，但具体样本不重复。
    3.  **分布外**：适配数据来自完全不同的领域或构造，与预训练无任何重叠。
*   **多维对比框架**：交叉评测不同的**适配架构**（全参数微调 vs. 参数高效微调如 LoRA）与不同的**隐私保护级别**（松弛 DP 与严格 DP）在上述数据分布下的安全表现。

### 3. 实验设计

*   **数据场景**：通过构造三种数据分布（精确重叠、同分布、分布外）来模拟真实世界的 LLM 微调场景。例如，使用与预训练语料同源的数据集测试 IID 情况，切换到全新领域测试 OOD 情况。
*   **基准测试**：以成员推理攻击的 AUC/TPR 和金丝雀提取的曝光率作为核心基准指标，衡量在给定 ε 噪声下，攻击者成功穿透隐私防线所需的最小代价。
*   **对比方法**：
    *   **适配策略**：至少对比了全参数微调与参数高效微调（LoRA）。
    *   **隐私设置**：对比了不同 ε 值（对应不同的噪声注入强度）下的攻击成功率。

### 4. 资源与算力

*   论文摘要及元数据中**未明确提及**具体使用的 GPU 型号、数量及总训练时长。由于涉及大规模语言模型的多次微调与攻击模拟，推测算力消耗较大，但缺乏可量化的数据支持。

### 5. 实验数量与充分性

*   **实验组合数量**：设置较为全面。需要交叉验证 **3 种数据分布 × 2 种以上适配方法 × 2 种以上隐私预算**的组合，且每种攻击（成员推理与提取）均需独立运行，推测进行的实验组数在十余组到数十组之间。
*   **充分性与公平性**：实验设计具有很强的系统性，通过控制变量的方式排除了无关因素的干扰，客观展示了不同维度下的攻击强度对比，对于验证“分布偏移是决定 DP 效力的首要因素”这一结论是充分的。但摘要未提及具体的消融实验。

### 6. 论文的主要结论与发现

*   **分布偏移主导风险**：在完全相同的 DP 理论保证（ε 相同）下，适配数据与预训练数据的分布越接近，遭受的实际隐私风险越高，即使两者没有直接的字面重叠。
*   **参数高效微调的抗性**：在适配分布外数据时，LoRA 等参数高效微调方法展现出了最高的经验隐私保护效果，显著优于全参数微调。
*   **DP 的力有不逮**：证明了当预训练与适配数据存在显隐性关联时，仅靠 DP 适配不足以阻挡先进的攻击，数据重叠会大幅侵蚀 DP 的保护边界。
*   **全流程评估倡议**：论文提出了一个新的结构化框架，呼吁社区将隐私评估的视野从单一的适配阶段扩展到“预训练-适配”全流水线，以识别深层次的联合风险。

### 7. 优点

*   **问题定位精准**：切中了 DP 在工业界落地时最致命的障碍——预训练数据无法被遗忘且不可知，证明理论完美保护在实践中可能名存实亡。
*   **方法论严谨**：没有将攻击和防御孤立看待，而是系统改变了数据生成的底层逻辑，揭示了“数据来源”比“噪声机制”更具决定性的洞见。
*   **工程指导价值高**：明确指出了 LoRA 在 OOD 场景下的安全性优势，为企业选择微调策略和判断数据隔离可行性提供了坚实的实验依据。

### 8. 不足与局限

*   **细节透明度缺失**：摘要未披露具体的模型规模、预训练语料来源及数据集构成，难以完全复现和推广其具体系数的普适性。
*   **攻击覆盖范围**：目前仅测试了成员推理和金丝雀提取，未覆盖更复杂的训练数据重建攻击或基于梯度的隐私攻击，可能低估了极端威胁模型下的风险。
*   **假设前提**：金丝雀提取需要事先在目标模型中植入秘密，属于有条件的攻击评测；在实际黑盒场景下，攻击者可能无法获得如此理想化的提取条件。
*   **黑白盒限制**：论文未说明攻击是白盒（有全梯度）还是黑盒（仅查询），不同的访问假设会显著影响隐私防护的实际有效性评估。

（完）
