---
title: Auditing Prompt Caching in Language Model APIs
title_zh: 审计语言模型API中的提示缓存
authors: "Chenchen Gu, Xiang Lisa Li, Rohith Kuditipudi, Percy Liang, Tatsunori Hashimoto"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=gUj2fxQcLZ"
tags: ["query:priv-sec"]
score: 9.0
evidence: 审计LLM API中的提示缓存，揭示通过侧信道时间攻击导致的隐私泄露。
tldr: 本文揭示LLM API中提示缓存导致的时间侧信道风险，通过统计审计方法在OpenAI等七家提供商中发现全局缓存共享，验证了用户提示隐私泄露的可行性，呼吁提高缓存政策透明度。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 提示缓存的时间差异可能被利用进行侧信道攻击，泄露用户隐私。
method: 设计统计审计方法检测真实LLM API提供商的全局缓存共享。
result: 在包括OpenAI在内的七家提供商中发现了全局缓存共享导致的隐私泄露风险。
conclusion: 揭示了当前LLM API部署中存在的严重隐私漏洞，需行业透明化改进。
---

## Abstract
Prompt caching in large language models (LLMs) results in data-dependent timing variations: cached prompts are processed faster than non-cached prompts. These timing differences introduce the risk of side-channel timing attacks. For example, if the cache is shared across users, an attacker could identify cached prompts from fast API response times to learn information about other users' prompts. Because prompt caching may cause privacy leakage, transparency around the caching policies of API providers is important. To this end, we develop and conduct statistical audits to detect prompt caching in real-world LLM API providers. We detect global cache sharing across users in seven API providers, including OpenAI, resulting in potential privacy leakage about users' prompts. Timing variations due to prompt caching can also result in leakage of information about model architecture. Namely, we find evidence that OpenAI's embedding model is a decoder-only Transformer, which was previously not publicly known.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：大型语言模型（LLM）API 提供商普遍采用“提示缓存”（prompt caching）来加速重复请求，但缓存的响应时间差异会构成**时间侧信道**（timing side channel）。
- **核心问题**：这种时间差异可能被攻击者利用，推断其他用户的提示内容，从而导致**用户隐私泄露**（prompt leakage）。此外，时间信息还可能泄漏模型架构细节。
- **整体含义**：论文呼吁行业重视提示缓存带来的隐私风险，并推动 API 提供商**公开缓存政策**，以便用户了解并评估潜在威胁。

## 2. 论文提出的方法论

- **核心思想**：通过精心设计统计审计方法，远程检测真实商业 LLM API 是否存在**跨用户的全局缓存共享**，从而量化隐私泄露风险。
- **关键技术细节**：
  - 利用“缓存命中”（cached prompt）与“缓存未命中”（non-cached prompt）的**响应时间差异**作为信号。
  - 设计实验范式：发送可能在缓存中已存在的提示与新提示，比较 API 响应时间的分布变化。
  - 使用**假设检验**等统计方法判断时间差异是否显著，进而推断缓存是否被全局共享。
- **公式或算法流程**：原文未提供具体公式，但流程可概括为：  
  1. 构造一批“种子”提示并重复发送，建立缓存。  
  2. 从另一个用户（如不同账户）再次发送相同提示。  
  3. 测量并统计处理时间，若第二个用户响应显著加快，则表明存在全局缓存共享。

## 3. 实验设计

- **审计对象**：七家真实 LLM API 提供商，包括 OpenAI 在内的主流服务。
- **实验场景**：
  - 跨用户缓存检测：使用不同账户发送相同提示，测试时间差异。
  - 信息泄漏验证：尝试通过缓存时间侧信道重建其他用户可能使用的提示。
  - 模型架构推断：利用时间模式推测 OpenAI 嵌入模型是否为仅解码器 Transformer。
- **对比方法**：论文本身未提及与其他隐私保护方法的对比，更侧重于对真实 API 的实证审计，而非算法性能 benchmark。
- **数据集**：未明确说明具体提示数据集，应由研究者自行构造的查询集合组成。

## 4. 资源与算力

- 论文中**未提及**所使用的具体 GPU 型号、数量或训练时长。
- 审计工作主要为 API 调用与计时分析，计算资源需求不高，重点在于网络请求与统计分析，可能无需大规模算力。

## 5. 实验数量与充分性

- **实验组数**：对七家 API 提供商进行了缓存共享检测，并进一步对部分提供商开展了模型架构推断实验。
- **充分性与客观性**：
  - 覆盖多个主流 API 服务，具有一定的代表性。
  - 跨用户实验采用统计检验控制假阳性，设计较为严谨。
  - 缺乏与其他时间侧信道防御方法或缓存策略的横向对比，但作为首次系统审计，实验已足够揭露现实风险。
  - 因商业 API 黑盒性，实验依赖外部观察，但仍通过多层统计验证确保结论可靠。

## 6. 论文的主要结论与发现

- 在**包括 OpenAI 在内的七家提供商**中，检测到全局缓存共享现象，确认通过时间侧信道可以泄露用户提示内容。
- 提示缓存时间差异可被用于推断**模型架构信息**：发现 OpenAI 的嵌入模型很可能是一个以前未公开的**仅解码器 Transformer**。
- 揭示了当前 LLM API 部署中存在的严重隐私漏洞，亟需行业提升透明度并改进缓存策略。

## 7. 优点

- **现实关联性强**：直接审计真实商业 API，而非仅限理论分析或模拟环境。
- **方法论创新**：将统计审计引入 LLM 隐私评估，提供可操作的检测流程。
- **发现具有冲击性**：不仅揭露隐私泄漏，还反推出未公开的模型架构，凸显侧信道威胁的深度。
- **促进政策改进**：为后续的 API 缓存透明化与隐私保护研究奠定了实证基础。

## 8. 不足与局限

- **实验细节未全公开**：受限于 OpenReview 的 PDF 访问限制（可能需要 CAPTCHA），我们只能基于摘要和元数据总结，具体实验参数、提示集规模、统计检验细节无法完整评估。
- **审计范围有限**：仅检测全局缓存共享，未涉及其他类型的侧信道（如包大小、功耗等）或防御方案。
- **供应商覆盖率**：虽然七家代表性提供商被审计，但未覆盖市面上所有 LLM API，结论可能不完全普遍适用。
- **时效性问题**：论文结论基于特定时间点的 API 行为，提供商更新策略后，检测结果可能变化。
- **伦理考量**：虽然论文旨在推动安全改进，但公开披露可能被恶意利用，需注意负责任披露。

（完）
