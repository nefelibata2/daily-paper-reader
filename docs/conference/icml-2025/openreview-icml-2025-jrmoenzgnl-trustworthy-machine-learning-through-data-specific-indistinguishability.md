---
title: Trustworthy Machine Learning through Data-Specific Indistinguishability
title_zh: 通过数据特定不可区分性实现可信机器学习
authors: "Hanshen Xiao, Zhen Yang, G. Edward Suh"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=JRMoeNZgNl"
tags: ["query:priv-sec"]
score: 7.0
evidence: 可证明的记忆化和数据投毒信任保证，适用于LLM隐私
tldr: 本文提出数据特定不可区分性框架，通过精心设计的随机化机制，为训练模型提供可证明的信任保证，涵盖记忆化、数据投毒和版权等问题。该框架可应用于大语言模型，为解决数据隐私和安全挑战建立了严格的理论和方法基础。该框架区别于传统输入无关的随机化，能根据数据差异调整保护强度，在多项信任度量上实现更优的效用-信任权衡。实验在记忆化抑制、投毒防御和版权保护任务上验证了其有效性，并展示在图像和文本生成模型上的适用性。该成果为构建可审计的AI系统提供了数学工具，有助于LLM开发者满足隐私法规和伦理要求。因此，数据特定不可区分性有望成为可信AI的通用构件，推动隐私和安全保障技术的标准化。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 当前AI可信性概念如记忆化、数据投毒等缺乏统一可证明保证框架。
method: 提出数据特定不可区分性(DSI)框架，通过最优多元高斯机制提供可证明信任保证。
result: 能有效限制数据对模型影响的差异，保障多种信任属性。
conclusion: 为LLM隐私和安全提供了理论基础的保障方法。
---

## Abstract
This paper studies a range of AI/ML trust concepts, including memorization, data poisoning, and copyright, which can be modeled as constraints on the influence of data on a (trained) model, characterized by the outcome difference from a processing function (training algorithm). In this realm, we show that provable trust guarantees can be efficiently provided through a new framework termed Data-Specific Indistinguishability (DSI) to select trust-preserving randomization tightly aligning with targeted outcome differences, as a relaxation of the classic Input-Independent Indistinguishability (III). We establish both the theoretical and algorithmic foundations of DSI with the optimal multivariate Gaussian mechanism. We further show its applications to develop trustworthy deep learning with black-box optimizers. The experimental results on memorization mitigation, backdoor defense, and copyright protection show both the efficiency and effectiveness of the DSI noise mechanism.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
可证明的记忆化和数据投毒信任保证，适用于LLM隐私。

### 2. 核心内容
本文提出数据特定不可区分性框架，通过精心设计的随机化机制，为训练模型提供可证明的信任保证，涵盖记忆化、数据投毒和版权等问题。该框架可应用于大语言模型，为解决数据隐私和安全挑战建立了严格的理论和方法基础。该框架区别于传统输入无关的随机化，能根据数据差异调整保护强度，在多项信任度量上实现更优的效用-信任权衡。实验在记忆化抑制、投毒防御和版权保护任务上验证了其有效性，并展示在图像和文本生成模型上的适用性。该成果为构建可审计的AI系统提供了数学工具，有助于LLM开发者满足隐私法规和伦理要求。因此，数据特定不可区分性有望成为可信AI的通用构件，推动隐私和安全保障技术的标准化。

### 3. 对应检索需求
Papers central to 请帮我查找与大模型隐私安全、医学AI隐私与安全、生成模型隐私安全、RAG安全有关的论文, especially work that connects or combines: privacy issues and solutions for large language models; security threats and defenses for large language models; security measures for medical AI systems; privacy risks in generative models; security vulnerabilities of generative models; security aspects of retrieval augmented generation; comprehensive survey of privacy and security issues in large AI models; privacy preserving techniques for medical AI and generative models; security threats and mitigation strategies in retrieval augmented generation.

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=JRMoeNZgNl](https://openreview.net/forum?id=JRMoeNZgNl)
