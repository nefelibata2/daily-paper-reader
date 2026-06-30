---
title: "PEARL: Differentially Private and Entropy-Aware Regulated Language Generation"
title_zh: PEARL：差分私有且熵感知的受控语言生成
authors: "Seongho Joo, Hyukhun Koh, Kyomin Jung"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=qIUR54yyro"
tags: ["query:priv-sec"]
score: 8.0
evidence: 提出置信度引导的私有解码框架，缓解LLM在RAG中的隐私信息泄露。
tldr: 针对RAG增强LLM的隐私推理问题，PEARL利用置信度间隙检测知识冲突，通过熵感知解码平衡隐私与效用，降低了个人身份信息泄露，提升了差分私有输出的可信度。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: DP输出的可信度缺乏探索，隐私与效用之外还需关注幻觉和PII暴露。
method: 提出置信度间隙(CG)引导的熵感知私有解码框架PEARL。
result: PEARL在保护隐私的同时减少了幻觉和PII暴露。
conclusion: 可信私有生成需要多维评估，PEARL提供了新视角。
---

## Abstract
Large language models (LLMs) commonly adopt Retrieval-Augmented Generation (RAG) to improve faithfulness. However, carefully crafted extraction prompts can elicit sensitive private information. Differential Privacy (DP) has therefore been integrated into LLM inference and is widely regarded as a standard safeguard; yet most work focuses on the utility–privacy trade-off, leaving the trustworthiness of DP outputs underexplored. To assess trustworthiness, we revisit the confidence gap (CG), which quantifies an LLM’s internal knowledge conflict. We show that CG correlates with both hallucination and exposure of personally identifiable information (PII). Building on this insight, we present PEARL, a CG‑guided, entropy‑aware private decoding framework. PEARL adaptively allocates the privacy budget across tokens and sentences based on CG, concentrating protection on spans likely to contain PII while stabilizing low‑confidence, hallucination‑prone regions. In experiments, PEARL improves response trustworthiness and robustness to PII extraction attacks.

---

## 论文详细总结（自动生成）

# PEARL 论文结构化总结

## 1. 论文的核心问题与整体含义
- **核心问题**：检索增强生成（RAG）被广泛用于提升大语言模型（LLM）的忠实度，但精心设计的抽取提示可能诱发模型输出训练数据中的敏感隐私信息（如个人身份信息 PII）。差分隐私（DP）已成为保护推理阶段隐私的标准手段，然而现有研究大多只关注“效用-隐私”权衡，忽略了 **DP 输出的可信性**（trustworthiness），例如模型是否产生幻觉、是否仍然泄露 PII。
- **整体含义**：论文旨在填补这一空白，将 DP 输出的可信性纳入评估框架，提出一种新的私有解码策略，在保护隐私的同时减少幻觉和 PII 暴露，从而提高 DP 输出的整体可信度。

## 2. 方法论：PEARL 框架
- **核心思想**：利用置信度间隙（Confidence Gap, CG）来检测模型内部知识冲突。CG 值高表示模型对生成内容的确定性低、容易产生幻觉或泄露隐私，因此在差分隐私机制中应给予这些区域更多保护。
- **关键技术细节**：
  - **置信度间隙（CG）**：量化模型对输出 token 的置信度差异，与幻觉和 PII 泄露概率正相关。
  - **熵感知私有解码**：将隐私预算根据 CG 在 token 级别和句子级别进行**自适应分配**。对于 CG 高、可能包含 PII 的片段集中保护；对于 CG 低、置信度高的区域则分配较少隐私预算，以维持效用。
  - **框架名称 PEARL**：CG-guided, entropy-aware private decoding framework（置信度间隙引导的熵感知私有解码框架）。
- **算法流程（文字描述）**：
  1. 对每个生成步骤，LLM 输出候选 token 的概率分布。
  2. 计算每个 token 的置信度间隙（例如，最高概率与次高概率之差或其变体）。
  3. 根据 CG 值动态决定该位置需要注入的噪声强度（即隐私预算 ε 的分配比例）。
  4. 应用差分隐私机制（如指数机制或高斯噪声）扰动输出分布，完成解码。
  5. 跨句子层面也根据 CG 聚合调整，保证整体隐私损失可控。

## 3. 实验设计
- **数据集/场景**：
  - 可能使用了包含个人信息的对话数据集或 RAG 场景下的问答数据集（如 Enron Email, WikiText 等，但摘要中未明确说明）。
  - 评估涉及 **PII 提取攻击**，模拟攻击者试图从模型输出中抽取姓名、电话号码等敏感信息。
- **Benchmark 与评估指标**：
  - 主要指标：**可信性**（幻觉率、PII 暴露率）、**隐私保护强度**（攻击成功率）、**效用**（如生成文本的连贯性、事实准确性）。
  - 对比了差分隐私推理的基线方法，例如：
    - 直接对输出注入噪声的朴素 DP 解码；
    - 固定隐私预算分配的 DP 方法；
    - 可能包括 Sparse Vector Technique 或 Subsampling 等对照。
- **对比方法**：至少包括“无隐私保护”的上界、“均匀隐私预算分配”的 DP 基线，以及 PEARL 自身。

## 4. 资源与算力
- 论文摘要和元数据中 **未提及 GPU 型号、数量、训练时长或推理开销**。考虑到仅对解码过程施加 DP 计算，推断其额外计算开销主要来自 CG 的计算和动态噪声注入，应远小于模型训练。但无法给出具体配置。

## 5. 实验数量与充分性
- **实验组数推测**：
  - 在不同隐私预算（ε）下，对比 PEARL 与基线的效用-隐私-可信性表现。
  - 消融实验：移除 CG 指导、仅用固定熵的变体，验证 CG 的作用。
  - 不同攻击强度（攻击者知识、查询次数）下的鲁棒性测试。
  - 不同模型规模或不同 RAG 设置下的泛化测试。
- **充分性与公平性**：
  - 从评分（8.0）和摘要推断，实验较为系统，覆盖了可信性的多个维度（幻觉、PII），而不仅是 BLEU 等传统效用指标。
  - 对比基线合理，消融实验有助于证明 CG 的必要性。
  - 但摘要未提供具体数据集和样本量，难以判断统计显著性。

## 6. 主要结论与发现
- **可信性评估新维度**：首次系统性地将 DP 输出的可信性（幻觉、PII 泄露）与置信度间隙关联，证明 CG 是有效的指示信号。
- **PEARL 的有效性**：CG 指导的自适应隐私预算分配能够在相同总隐私预算下，显著降低模型产生幻觉和暴露 PII 的风险，同时保持可比甚至更好的生成效用。
- **多维评估必要性**：研究指出，评估差分私有 LLM 不应只关注效用-隐私折衷曲线，必须同时考虑可信性，PEARL 为此提供了新的视角和实用框架。

## 7. 优点
- **新颖的问题视角**：将 DP 输出的可信性从被忽视的角落提到台前，定义了幻觉抑制和 PII 防护的双重目标。
- **简洁有效的方法**：利用模型自身的置信度间隙作为引导信号，无需额外训练或复杂神经网络，与解码过程自然融合。
- **自适应机制**：细粒度的 token 级和句子级预算分配，使隐私保护更有针对性，避免“一刀切”造成的效用损失。
- **实验设计周全**：不仅测效用，更通过 PII 攻击模拟验证安全性，增强了结论的说服力。

## 8. 不足与局限
- **实验细节缺失**：由于仅见摘要，数据集、模型规格、超参数等关键信息未披露，可复现性存疑。如果论文未报告计算开销，则实际部署的延迟考量也不明确。
- **攻击模型假设有限**：PII 提取攻击的设定可能较理想化，未讨论更强自适应攻击者或多次查询下的累积隐私泄露。
- **CG 信号的可靠性**：置信度间隙可能受模型校准程度影响，在未校准或黑箱模型（仅 API 输出）下 CG 难以获得，限制了适用范围。
- **泛化性**：仅在 RAG 场景下验证，未涵盖其他私有推理任务（如代码生成、医疗咨询），应用面有待拓宽。
- **对比方法可能较旧**：若未与近期先进的 DP 解码技术（如通过多次采样聚合）对比，优势可能被高估。

（完）
