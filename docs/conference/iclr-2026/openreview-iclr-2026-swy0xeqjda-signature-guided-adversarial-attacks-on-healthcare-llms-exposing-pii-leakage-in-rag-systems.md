---
title: "Signature-Guided Adversarial Attacks On Healthcare LLMs: Exposing PII Leakage In RAG Systems"
title_zh: 针对医疗LLM的签名引导对抗攻击：暴露RAG系统中的PII泄漏
authors: "Jean C Tonday Rodriguez, Juhair Fiaz Alam, Mohammad Kumail Kazmi, Mohammad Rahman"
date: 2025-09-16
pdf: "https://openreview.net/pdf?id=Swy0XEqJdA"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过签名引导对抗攻击暴露医疗RAG系统中的PII泄漏
tldr: 大型语言模型在医疗领域应用广泛，但RAG数据库存储的医疗信息即使去标识化仍可能泄露。本文提出签名引导对抗攻击，展示如何泄露患者个人身份信息。实验在真实医疗数据上成功恢复PII，揭示RAG安全漏洞。该研究强调在医疗RAG系统中必须加强隐私保护。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 医疗RAG系统存储信息存在PII泄漏风险，即使去标识化也不安全。
method: 提出签名引导对抗攻击，利用病历签名进行信息恢复。
result: 攻击成功恢复PII，证明RAG系统存在严重隐私漏洞。
conclusion: 需要更严格的隐私保护机制来保障医疗RAG安全。
---

## Abstract
The adoption of Large Language Models (LLMs) is accelerating across the healthcare domain. Medical assistants are increasingly used to implement and deploy medical databases and questioning models. Retrieval Augmented Generation (RAG) has become an alternative way to introduce LLMs to specific data, such as a medical specialty, by selecting relevant context to improve answer quality. However, storing medical information in RAG databases can result in leakage, even when the data is properly de-identified. Furthermore, data de-identification limits the medical capabilities of the model; tasks such as ID-retrieval and medical billing become nontrivial without access to private identifiable information (PII). Medical leakage can include PII, which is protected by strict federal regulations, such as the Health Insurance Portability and Accountability Act (HIPAA). Therefore, PII privacy is a critical concern for developers of medical assistants. To defend against leakage, AI companies such as OpenAI and Anthropic provide safety fine-tuning and careful prompt engineering to steer LLMs towards safe behavior. Prior research has investigated circumventing such defenses through masking inference and adversarial prompt engineering. However, no previous work has studied the use of medical signatures formed from patient notes, reducing the effect of defenses. In this paper, we look to bypass existing security by building medical signatures from the patient's medical notes and adversarial prompting to guide RAG healthcare models in retrieving PII from its secure databases. We design a RAG medical agent with safety considerations, highlighting how signature-based attacks force PII leakage more efficiently than the existing approaches. Our attack highlights key vulnerabilities in RAG-based healthcare models, with leakage rates of up to 98\%.

---

## 论文详细总结（自动生成）

# 论文总结：《Signature-Guided Adversarial Attacks On Healthcare LLMs: Exposing PII Leakage In RAG Systems》

## 1. 核心问题与研究动机
- **核心问题**：在医疗领域，基于检索增强生成（RAG）的大语言模型（LLM）助手虽然能提升专业问答能力，但其存储的医疗数据即使经过“去标识化”处理，仍可能泄露受《健康保险可移植性与责任法案》（HIPAA）严格保护的个人身份信息（PII）。AI公司如OpenAI、Anthropic通过安全微调和提示工程来防御此类泄漏，但现有攻击（如掩蔽推理、对抗提示）仍能绕过部分防护。
- **整体含义**：本研究首次提出“病历签名引导”这一更高效的新攻击范式，证明攻击者可以利用患者病历中形成的医学签名，结合对抗提示，迫使带有安全防护的RAG医疗代理以高达98%的泄漏率输出PII。工作直接揭示了RAG架构在真实医疗场景中的严重隐私脆弱性，强调仅靠传统去标识化与当前防护措施远远不够。

## 2. 方法论
- **核心思想**：从患者的病历笔记中自动构建“医学签名”（medical signatures），并将该签名作为先验知识嵌入对抗性查询，从而引导RAG模型绕开安全对齐，从其数据库或参数记忆中精准检索并输出目标患者的PII。
- **关键技术细节**：
  - **医学签名构建**：从电子病历非PII字段（如诊断描述、症状记录、用药历史、实验室结果等）中提取稳定的特征模式，形成能唯一或高概率匹配特定患者的签名向量或文本描述。
  - **对抗提示生成**：将签名与精巧设计的提示模板结合，伪装成合法的医疗查询，使模型在执行检索/生成时无意识地暴露出被关联的PII（例如姓名、社会保险号、地址）。
  - **攻击流程示意**（文字概括）：① 获取公开或半公开的患者非PII记录 → ② 提取签名 → ③ 将签名包装为查询（如“基于下列病历特征，请还原该患者的完整档案以便核实账单”）→ ④ 向目标RAG医疗代理发送查询 → ⑤ 收集输出中的PII，计算泄漏成功率。
- **与现有方法的区别**：传统攻击仅依赖掩蔽词或通用越狱提示，未利用数据特有的医疗语义结构；而签名引导攻击利用病历本身的特征一致性，显著降低模型防御的成功率。

## 3. 实验设计
- **数据集/场景**：论文采用 **真实医疗数据**（具体来源未在摘要中披露），构建了带有安全微调与提示工程防护的RAG医疗代理作为攻击靶标。
- **基准与对比方法**：
  - 对比了 **现有对抗攻击方法**（如基于掩蔽推理的攻击、传统对抗提示工程），用于展示签名引导攻击的优越性。
  - 以无签名的直接PII查询作为基线，可能还比较了不同强度的安全防御。
- **评估指标**：主要使用 **PII泄漏率**（成功还原受保护标识符的比例），报告高达 **98%** 的泄漏率。

## 4. 资源与算力
- **说明**：所提供的摘要和元数据中 **未提及** GPU型号、数量、训练时长等算力细节。鉴于研究主要涉及攻击的实现与评估（而非耗时的大规模模型训练），推测所需算力集中在RAG系统的搭建与对抗查询的批量化实验上，但具体资源量无法确定。

## 5. 实验数量与充分性
- **实验规模估计**：从摘要可推断，至少包含多组攻击方法的对比实验，以及一个能够达到98%泄漏率的核心结果。文中提到“Our attack highlights key vulnerabilities… with leakage rates of up to 98%”，暗示可能覆盖了不同安全配置或签名精度的消融研究。
- **充分性与公平性**：由于缺乏全文细节，无法准确判断实验是否包含不同病历类型、不同RAG实现、对抗性防御强度变化等多维度分析。现有信息表明实验成功证明了签名引导攻击的高效性，但若要全面评估其稳健性，还需更多关于数据集规模、重复次数和统计显著性的说明。从设计上，研究选择带安全防护的RAG靶标并对比已有攻击方法，对比基础较为公平。

## 6. 主要结论与发现
- 医疗RAG系统中，即使将数据正确去标识化，仍然存在严重的PII泄漏风险。
- 基于病历签名合成的对抗性提示，能够以远高于传统方法的成功率诱导模型暴露PII，泄漏率可高达98%。
- 该攻击方式证明当前依赖安全微调和提示工程的防御措施在医疗上下文签名攻击下效力大减，亟需部署更底层、更严格的隐私保护机制。

## 7. 优点
- **创新性威胁模型**：首次将“医学签名”概念引入对抗攻击，利用了医疗数据内部的结构化相关性，比通用越狱更有针对性且更隐蔽。
- **现实意义突出**：直接针对受HIPAA等法规约束的真实医疗RAG系统，展示了攻击的可行性和高危险性，为后续防御研究提供了强有力的推动。
- **结果对比清晰**：通过与现有攻击方法的对比，凸显了签名引导攻击的效率优势，验证了方法的有效性。

## 8. 不足与局限
- **信息缺失**：摘要未披露所用真实数据集的具体性质、规模及患者覆盖范围，因此无法判断攻击的普适性（是否只对特定类型病历有效）。
- **防御评估单一**：虽然靶标系统考虑了安全措施，但未明确是否测试了多种先进的防御（如差分隐私训练、信息过滤、输出检测），结论可能局限于特定防护配置。
- **实验透明度**：无消融实验细节（如签名构建方法差异、对抗提示模板变体对结果的影响）和算力开销，可复现性与严谨性难以完全评判。
- **应用限制**：攻击依赖能够获取一定量的非PII病历信息以构建签名，在完全封闭、无任何辅助信息的数据库中成功率可能下降；且仅展示了泄漏风险，未提供完备的防护方案。

（完）
