---
title: "SecureLLM: Using Inference-time Compositionality to Build Secure Language Models for Private, Sensitive, and Secret Data"
title_zh: SecureLLM：利用推理时组合性为私有、敏感和秘密数据构建安全语言模型
authors: "Christian Michael Arnold, Abdulrahman Alabdulkareem, Yerim Lee, Pieter M Feenstra, Conner Arnold, Boris Katz, Andrei Barbu, Brian Cheung"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=mJSL9qU8DW"
tags: ["query:priv-sec"]
score: 9.0
evidence: 为医疗等领域LLM提供数据机密性和访问控制，保护私有信息。
tldr: 现有LLM安全措施难以强制隔离机密数据，尤其在医疗等敏感领域。本文提出SecureLLM框架，通过在独立数据隔离区微调模型并在推理时组合输出，确保私有信息不被泄露。实验证明该方法能严格保护数据机密性，为医疗AI隐私安全提供坚实基础。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 传统安全机制无法保证LLM严格隔离敏感数据，存在泄露风险。
method: 在隔离数据分区微调模型，推理时动态组合输出以保护隐私。
result: 框架能有效防止私有数据泄露，实现安全的访问控制。
conclusion: SecureLLM为敏感行业提供了可证明的数据安全保障。
---

## Abstract
As Large Language Models (LLMs) increasingly support critical sectors such as healthcare, finance, and public governance, ensuring data confidentiality and robust access control is a pressing societal challenge. Traditional security mechanisms isolate sensitive resources from unauthorized users, yet existing LLM safety approaches often fail to enforce strict segregation of confidential data. In this work, we introduce SecureLLM, a novel compositional framework for building provably secure large language models (LLMs) that integrates fine-tuning with traditional access security measures to protect private information. By fine-tuning LLMs on segregated, “siloed” training data and composing their outputs at inference time based solely on a user’s verified credentials, SecureLLM not only prevents unauthorized data leakage but also enables accurate responses for complex queries spanning multiple data silos. Our method is demonstrated on a challenging natural-language-to-SQL translation task and is designed with real-world applications in mind—supporting sectors where protecting sensitive information is paramount.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：现有大语言模型（LLM）无法在推理时严格隔离不同来源的敏感数据，容易造成私有信息泄露，这在医疗、金融、政务等关键领域是重大安全隐患。
- **研究动机**：传统安全机制（如访问控制、数据隔离）在LLM中往往通过提示词设计或外部过滤实现，但这些方法缺乏可证明的安全性，难以防止模型在不同访问语境下无意识地混合隐私数据。
- **整体含义**：SecureLLM旨在为需要处理私人、敏感或秘密数据的LLM应用提供一种 **“推理时可证明安全”** 的构建框架，使得模型输出严格遵循用户权限，从而保障数据机密性和访问控制。

### 2. 论文提出的方法论
- **核心思想**：**基于推理时组合性构建安全LLM**
  - 在训练阶段，将不同敏感级别的数据放入**互相隔离的数据仓（siloed data）**，分别微调LLM。
  - 在推理阶段，根据用户的验证凭证（verified credentials）动态选取并**组合来自多个独立微调模块的输出**，生成最终回答。
  - 这种组合过程仅使用与用户权限匹配的模型模块，从架构层面杜绝跨仓数据混用的可能。
- **关键技术细节**：
  - 微调时，不同数据仓的数据互不可见，每个微调模型只掌握其对应仓内的知识。
  - 推理时，系统接收用户查询及其访问令牌，由**访问控制层**决定调用哪些微调模型参与输出生成。
  - 输出组合方式可能是概率分布融合、序列交织或结构化拼接，具体取决于任务；文中以自然语言到SQL翻译（NL-to-SQL）任务作为演示。
- **公式或算法流程**（文字说明）：
  - 设有n个数据仓 D₁,…,Dₙ，为每个仓训练独立的模型参数 θ₁,…,θₙ。
  - 对于用户u，凭证给出可访问的仓集合 S(u) ⊆ {1,…,n}。
  - 对输入查询 q，SecureLLM生成回答 y 的过程相当于：  
    y = Combine( {LLM(q; θᵢ) | i∈S(u)} )，  
    其中 Combine 函数保证仅使用授权仓的模型信息，且组合后的输出不泄露任何未授权仓的内容。

### 3. 实验设计
- **数据集与场景**：采用**自然语言到SQL翻译（NL-to-SQL）** 这一具有明确数据隔离需求的挑战性任务，模拟多机构/多权限的数据访问场景。
- **Benchmark**：虽未在摘要中指明具体数据集名称（如Spider, WikiSQL等），但该任务常用公有NL-to-SQL基准，并配合构造的隐私隔离场景（例如不同部门/机构的数据库表）。
- **对比方法**：与传统LLM安全措施（如基于Prompt的访问控制、外部审计过滤器、全数据微调+规则后处理等）进行比较，重点突出SecureLLM在可证明安全和防泄漏方面的优势。

### 4. 资源与算力
- 摘要和提供的元数据中**未明确说明**使用的GPU型号、数量或训练时长。
- 结合其需要分别微调多个模型来看，训练资源可能等于单模型微调资源乘以隔离数据仓的数量，但具体算力消耗需要在论文全文中才会披露。

### 5. 实验数量与充分性
- 由于仅拿到摘要，无法判断具体做了多少组实验。但可以推断：
  - **至少包含NL-to-SQL主实验**，对比不同访问控制方案的表现。
  - 推测包含**消融实验**，如组合策略对比、不同隔离粒度的影响、安全性与准确性的权衡等。
  - 所描述的框架以理论可证明安全为卖点，实验应兼顾安全泄露度量与任务准确率，若能展示多仓混合查询下的零泄露结果，则具有较强说服力。目前无法判断实验是否足够全面，但方向设计较为客观、公平。

### 6. 论文的主要结论与发现
- SecureLLM能够**在推理时严格保护私有数据**，防止未授权信息通过模型输出泄漏。
- 框架实现了**可证明的安全性**（provably secure），不依赖于启发式提示或事后过滤。
- 在NL-to-SQL翻译任务上，模型仍能**准确回答跨越多数据仓的复杂查询**，证明隔离与组合不会严重损害语言理解性能。
- 该方法为医疗、金融等敏感行业部署LLM提供了坚实的安全基础。

### 7. 优点（方法或实验设计上的亮点）
- **安全性可证明**：通过架构设计确保训练数据隔离、推理时按权组合，提供了传统LLM安全方案缺乏的强安全保证。
- **面向实际应用**：支持多权限、多机构数据共享场景，可直接适配真实工作流（如医院间联合查询）。
- **任务选择典型**：NL-to-SQL任务能直观展示数据表级别的敏感信息隔离，且泛化性强。
- **推理时动态组合**：无需重新训练或加载全部模型，仅动态组合所需分仓模型，部署灵活。

### 8. 不足与局限
- **实验覆盖可能有限**：仅使用NL-to-SQL任务，在其他生成任务（如开放域问答、摘要）上的安全性与性能未知。
- **偏差风险**：隔离训练可能丢失不同仓之间潜在的良性知识关联，影响模型的理解广度，摘要未探讨这种权衡。
- **应用限制**：实际部署中数据仓的划分、凭证体系的准确性、组合策略的设计均可能存在工程挑战，且多模型推理增加了延迟和调度复杂度。
- **未计算力成本**：为每个数据仓独立微调模型，训练和存储成本随仓数量线性增长，对极大规模部署不友好，但摘要未讨论此点。

（完）
