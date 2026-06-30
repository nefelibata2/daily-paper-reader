---
title: Privacy-Preserving LLM Interaction with Socratic Chain-of-Thought Reasoning and Homomorphically Encrypted Vector Databases
title_zh: 基于苏格拉底链式推理与同态加密向量数据库的隐私保护LLM交互
authors: "Yubeen Bae, Minchan Kim, Jaejin Lee, Sangbum Kim, Jaehyung Kim, Yejin Choi, Niloofar Mireshghallah"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=GzdVJEE3IW"
tags: ["query:priv-sec"]
score: 9.0
evidence: 利用苏格拉底推理和同态加密实现对医疗记录等敏感数据的隐私保护LLM查询。
tldr: 用户使用远程大模型时需权衡隐私与性能。本文提出苏格拉底链式推理与同态加密向量数据库结合的方法：先让不受信任的LLM生成子查询，再对加密医疗数据执行语义搜索，全程不泄露隐私。实验显示该方法在保护隐私的同时保持了较高的回答质量，为个人医疗助手等应用提供可行方案。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: 发送敏感数据到不可信LLM存在隐私泄露风险，本地模型性能不足。
method: 苏格拉底CoT生成子查询，同态加密实现加密向量的语义搜索。
result: 方法在不暴露数据前提下保持高答案质量，延迟可接受。
conclusion: 为医疗等敏感领域的隐私保护LLM应用提供新范式。
---

## Abstract
Large language models (LLMs) are increasingly used as personal agents, accessing sensitive user data such as calendars, emails, and medical records. Users currently face a trade-off: They can send private records—many of which are stored in remote databases—to powerful but untrusted LLM providers, increasing their exposure risk. Alternatively, they can run less powerful models locally on trusted devices. We bridge this gap: Our Socratic Chain-of-Thought Reasoning first sends a generic user query to a powerful, untrusted LLM, which generates a Chain-of-Thought (CoT) prompt and detailed sub-queries without accessing user data. Next, we embed these sub-queries and perform encrypted sub-second semantic search using our Homomorphically Encrypted Vector Database across one million entries of a single user's private data. This represents a realistic scale of personal documents, emails, and records accumulated over years of digital activity. Finally, we feed the CoT prompt and the decrypted records to a local language model and generate the final response. On the LoCoMo long-context QA benchmark, our hybrid framework—combining GPT-4o with a local Llama-3.2-1B model—outperforms using GPT-4o alone by up to 7.1 percentage points. This demonstrates a first step toward systems where tasks are decomposed and split between untrusted strong LLMs and weak local ones, preserving user privacy.

---

## 论文详细总结（自动生成）

# 论文总结：基于苏格拉底链式推理与同态加密向量数据库的隐私保护LLM交互

## 1. 核心问题与整体含义
- **研究动机**：大型语言模型（LLMs）越来越多地作为个人代理，需要访问用户的日历、邮件、医疗记录等敏感数据。当前用户面临两难：要么将私密数据发送给强大但不可信的远端LLM提供商（隐私泄露风险高），要么在本地可信设备上运行性能较弱的模型（能力不足）。
- **整体含义**：论文提出一种混合框架，将任务在“不可信但强大的LLM”与“可信但弱小的本地模型”之间进行拆分，既保护用户数据隐私，又能利用大模型的高质量推理能力，为医疗等敏感场景下的隐私保护LLM应用提供可行方案。

## 2. 方法论
- **核心思想**：通过**苏格拉底式链式推理（Socratic CoT）** 与**同态加密向量数据库**的结合，实现在不暴露原始数据的情况下完成复杂查询。
- **关键技术流程**：
  1. **子查询生成**：将用户的通用查询发送给不可信的强大LLM（如GPT-4o），让其生成包含思路的链式推理提示（CoT prompt），并从中分解出详细的子查询。此时LLM不接触任何用户私有数据。
  2. **加密语义搜索**：将子查询通过嵌入模型转为向量，然后使用**同态加密向量数据库**在单个用户的多达一百万条私有数据（模拟个人多年数字活动积累的文档、邮件、记录）上进行密文下的语义搜索。该搜索能在亚秒级完成，全程数据保持加密。
  3. **本地生成最终回答**：将搜索出的加密记录解密后，与之前生成的CoT提示一同输入到本地小型语言模型（如Llama-3.2-1B），由本地模型合成最终回复。
- **公式/算法**：摘要未给出具体公式，但流程可概括为：Query → LLM生成CoT与子查询 → Embed(子查询) → 同态加密检索Top-K → 解密记录 + CoT → 本地LLM生成答案。

## 3. 实验设计
- **数据集**：使用了**LoCoMo长上下文问答基准**（long-context QA benchmark）。
- **对比方法**：
  - 单独使用强大的远端模型GPT-4o（有隐私风险的基础方案）。
  - 提出的混合框架：GPT-4o + 本地Llama-3.2-1B模型（隐私保护方案）。
- **评估指标**：摘要仅提及“性能”比较，具体指标未说明（推测为问答准确率等）。

## 4. 资源与算力
- 文中未明确提及所使用的GPU型号、数量或训练时长。摘要只说明了使用的模型（GPT-4o 和 Llama-3.2-1B）以及同态加密检索的延迟特点（亚秒级），但未给出具体硬件配置。

## 5. 实验数量与充分性
- 从摘要看，明确提及的实验数量有限：仅在LoCoMo一个基准上进行了混合框架与纯GPT-4o的对比。未提及消融实验、不同数据集、多种基础模型组合或多用户规模扩展等。因此，从公开摘要来看，实验覆盖度和充分性较为有限，难以全面评估方法的稳健性和公平性。更详细的内容需要查阅全文。

## 6. 主要结论与发现
- 提出的混合框架在LoCoMo长上下文QA上，**比单独使用GPT-4o的性能高出最多7.1个百分点**。
- 该方案在完全无需将用户数据暴露给不可信LLM的情况下，保持了高回答质量，证明了“强-弱模型拆分、隐私保护协作”范式的初步可行性。
- 实现了在百万级个人私有数据上的加密语义搜索，且延迟可接受（亚秒），解决了实际规模下的效率问题。

## 7. 优点
- **隐私保护与效用的平衡**：巧妙地利用同态加密阻断数据泄露路径，同时用强模型生成高质量推理提纲，弱模型负责集结信息，避免了本地模型单独处理时能力不足的缺陷。
- **现实规模验证**：在一百万条记录上进行了加密检索实验，贴近个人多年数字生活的实际数据量，证明了可扩展性。
- **方法论新颖**：“苏格拉底式”推理将思考过程与数据分离，再结合密态检索，为隐私敏感的LLM应用提供了新范式。

## 8. 不足与局限
- **实验覆盖单一**：仅在LoCoMo一个基准上进行了评估，缺乏在更多样化的隐私QA数据集（如医疗、财务等专业领域）上的验证。
- **系统组件较多**：涉及同态加密、向量数据库、大模型调用和本地模型，端到端延迟和部署复杂度未详细分析，可能存在工程挑战。
- **安全性假设限制**：虽然数据在云端加密，但子查询本身可能包含间接敏感信息，且本地模型处理解密数据的环境安全未讨论；也未考虑如模型窃取、边信道等其他攻击面。
- **扩展性边界未知**：当数据规模进一步扩大到千万级或多用户并发时，同态加密检索的延迟是否仍为亚秒级，未提供证据。
- **对比基线不足**：仅与GPT-4o单独使用对比，未与其它隐私保护技术（如差分隐私、安全多方计算等）进行横向比较，难以全面说明优势。

（完）
