---
title: "StealthInk: A Multi-bit and Stealthy Watermark for Large Language Models"
title_zh: StealthInk：一种多比特隐形大语言模型水印
authors: "Ya Jiang, Chuxiong Wu, Massieh Kordi Boroujeny, Brian Mark, Kai Zeng"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=dktpDfUTtj"
tags: ["query:priv-sec"]
score: 4.0
evidence: 提出了用于LLM生成文本的多比特水印，可嵌入溯源数据
tldr: 为解决现有LLM水印在文本分布保持和信息嵌入能力上的不足，本文提出StealthInk隐形多比特水印方案，能在保持原始文本分布的前提下嵌入溯源数据，如用户ID和时间戳。实验证明，该方案支持快速可追溯性，无需访问模型API，在隐蔽性和信息容量间取得了良好平衡，为AI生成内容的版权保护和来源验证提供了实用工具。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有LLM水印方法或破坏文本分布，或仅支持零比特检测，无法嵌入溯源信息。
method: 提出StealthInk，一种在保持原始文本分布的同时，将多比特溯源数据嵌入LLM生成文本的隐形水印方案。
result: 实验表明StealthInk可实现多比特信息嵌入，且不影响文本质量，支持快速追踪。
conclusion: 该方案为LLM生成内容溯源提供了有效手段，兼顾了水印的隐蔽性和信息容量。
---

## Abstract
Watermarking for large language models (LLMs) offers a promising approach to identifying AI-generated text. Existing approaches, however, either compromise the distribution of original generated text by LLMs or are limited to embedding zero-bit information that only allows for watermark detection but ignores identification. We present StealthInk, a stealthy multi-bit watermarking scheme that preserves the original text distribution while enabling the embedding of provenance data, such as userID, TimeStamp, and modelID, within LLM-generated text. This enhances fast traceability without requiring access to the language model's API or prompts.  We derive a lower bound on the number of tokens necessary for watermark detection at a fixed equal error rate, which provides insights on how to enhance the capacity. Comprehensive empirical evaluations across diverse tasks highlight the stealthiness, detectability, and resilience of StealthInk, establishing it as an effective solution for LLM watermarking applications.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
提出了用于LLM生成文本的多比特水印，可嵌入溯源数据。

### 2. 核心内容
为解决现有LLM水印在文本分布保持和信息嵌入能力上的不足，本文提出StealthInk隐形多比特水印方案，能在保持原始文本分布的前提下嵌入溯源数据，如用户ID和时间戳。实验证明，该方案支持快速可追溯性，无需访问模型API，在隐蔽性和信息容量间取得了良好平衡，为AI生成内容的版权保护和来源验证提供了实用工具。

### 3. 对应检索需求
security threats and defenses for large language models。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=dktpDfUTtj](https://openreview.net/forum?id=dktpDfUTtj)
