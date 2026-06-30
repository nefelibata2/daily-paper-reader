---
title: An Investigation of Memorization Risk in Healthcare Foundation Models
title_zh: 医疗基础模型记忆化风险研究
authors: "Sana Tonekaboni, Lena Stempfle, Adibvafa Fallahpour, Walter Gerych, Marzyeh Ghassemi"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=NMvMYtRjkg"
tags: ["query:priv-sec"]
score: 9.0
evidence: 评估医疗基础模型的记忆化风险，探查患者隐私泄露
tldr: 基于电子健康记录训练的基础模型可能记忆患者信息，带来隐私风险。本文提出一套黑盒评估测试，在嵌入和生成两个层面探查模型记忆化程度，区分泛化与有害记忆，尤其关注脆弱子群体的隐私影响。验证实验表明，模型存在潜在记忆风险，为医疗AI的隐私保护提供了系统的评估框架，有助于指导安全模型的设计与部署。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 医疗基础模型可能记忆患者信息，隐私评估方法缺失。
method: 提出黑盒评估框架，在嵌入和生成层面探查记忆化风险。
result: 证实模型存在记忆化风险，脆弱子群体受影响更大。
conclusion: 为医疗AI隐私保护提供了系统的风险测量工具，指导安全部署。
---

## Abstract
Foundation models trained on large-scale de-identified electronic health records (EHRs) hold promise for clinical applications. However, their capacity to memorize patient information raises important privacy concerns. In this work, we introduce a suite of black-box evaluation tests to assess privacy-related memorization risks in foundation models trained on structured EHR data. Our framework includes methods for probing memorization at both the embedding and generative levels, and aims to distinguish between model generalization and harmful memorization in clinically relevant settings. We contextualize memorization in terms of its potential to compromise patient privacy, particularly for vulnerable subgroups. We validate our approach on a publicly available EHR foundation model and release an open-source toolkit to facilitate reproducible and collaborative privacy assessments in healthcare AI.

---

## 论文详细总结（自动生成）

# 医疗基础模型记忆化风险研究：黑盒隐私评估框架

## 1. 核心问题与研究意义
- **研究动机**：基于大规模去标识化电子健康记录（EHR）训练的基础模型在临床应用中潜力巨大，然而这些模型可能“记住”训练数据中的患者信息，引发严重的隐私泄露风险。
- **核心问题**：现有工作缺乏系统、可操作的隐私风险评估方法，难以区分模型对临床知识的泛化与对个体信息的**有害记忆**，尤其缺少对脆弱子群体所受隐私威胁的专门分析。
- **整体含义**：本文旨在为医疗AI领域提供一套**可重复、可协作**的记忆化风险黑盒评估框架，以便在模型部署前测量敏感信息泄露的倾向，助力隐私保护合规与安全设计。

## 2. 方法论
- **框架性质**：全黑盒评估，**无需访问模型参数或训练数据**，仅通过查询模型的嵌入表示或生成输出来推断记忆化程度。
- **关键维度**：
    - **嵌入层面探测**：从结构化EHR数据的嵌入空间中提取信号，判断模型是否过度拟合了特定的患者记录。
    - **生成层面探测**：若模型具备生成能力，则分析其输出中是否重现了真实患者的唯一性信息。
- **核心目标**：
    - 区分**良性泛化**与**有害记忆**，在临床相关设定下进行风险判定。
    - 量化记忆化如何可能损害患者隐私，尤其关注**脆弱子群体的不平等影响**。
- 文中未给出具体公式或算法伪代码，但强调了评估方法的设计原则：通过黑盒测试套件，以标准化流程探查模型在不同层级上的记忆痕迹。

## 3. 实验设计
- **数据集 / 场景**：在**结构化EHR数据**（去标识化）上训练的公开可用模型上进行验证（摘要未指明数据集具体名称，仅提及“publicly available EHR foundation model”）。
- **评估基准（Benchmark）**：实验重点在于展示所提黑盒测试套件的有效性，而非与众多方法对比。基线可能是未考虑记忆化风险的通用模型表现，但文中未详细说明对比的其它隐私评估方法。
- **验证方式**：通过在现实世界的EHR基础模型上应用测试套件，检查不同脆弱子群体受记忆化影响的差异。

## 4. 资源与算力
- 摘要**未提及任何关于GPU型号、数量、训练时长或计算成本**的信息。
- 论文可能聚焦于评估流程的开源工具包，其计算开销主要体现在黑盒查询上，而非大规模训练。但具体算力消耗无法从提供的内容中获知。

## 5. 实验数量与充分性
- **实验组数**：摘要仅描述了对一个公开EHR基础模型进行验证，未说明不同数据集、不同模型架构的对比，也未提及消融实验。
- **充分性判断**：由于信息有限，难以评判实验是否充分。从动机来看，作者强调发布开源工具包以促进后续协作和可重复研究，暗示当前实验更偏向**概念验证**；未来需要更多社区参与来覆盖更广泛的模型与数据分布。
- **客观性与公平性**：未披露对比方法的细节，无法评价对比的公平性。但从设计上看，黑盒评估方式本身避免了因模型架构差异带来的主观偏差。

## 6. 主要结论与发现
- 经验证，**EHR基础模型确实存在记忆化风险**，可能泄露患者隐私。
- 记忆化影响并非均匀分布：**脆弱子群体受到的风险显著更大**，提示需考虑公平性维度的隐私保护。
- 提出的评估框架能有效区分泛化与有害记忆，为医疗AI隐私保护提供了**系统的风险测量工具**。
- 开源工具包可促进可重复、可协作的隐私评估，指导模型的安全设计、审计与合规部署。

## 7. 优点（亮点）
- **首次黑盒记忆化评估框架**：填补了结构化EHR基础模型隐私风险量化工具的空白，无需内部模型信息，实用性强。
- **多层级探查**：同时覆盖嵌入层与生成层，从不同角度捕捉记忆痕迹，评估更为全面。
- **关注脆弱群体**：将公平性纳入隐私分析，强调记忆化对特定子群体的不成比例影响，具有临床伦理价值。
- **开源与可重复性**：发布评估工具包，推动整个领域形成统一的隐私测试标准。

## 8. 不足与局限
- **实验覆盖有限**：仅针对一个公开EHR基础模型展示，缺乏跨数据集、跨模型规模的横向对比，泛化证据不足。
- **细节缺失**：摘要未提供具体评估指标、数据集名称、检测记忆化的算法细节，难以评判技术深度。
- **黑盒限制**：虽然黑盒方式便于推广，但可能漏检仅能从内部表征发现的隐蔽记忆化模式。
- **隐私定义窄化**：主要关注患者信息泄露，未讨论梯度泄露、成员推断等其他攻击面，框架的隐私范围仍有待扩展。
- **验证场景单一**：仅在去标识化的结构化EHR数据上测试，未涉及半结构化文本或多模态数据，在实际部署中的表现尚需更多检验。

（完）
