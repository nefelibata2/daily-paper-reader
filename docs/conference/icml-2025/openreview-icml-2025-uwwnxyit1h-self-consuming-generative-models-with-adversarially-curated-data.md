---
title: Self-Consuming Generative Models with Adversarially Curated Data
title_zh: 对抗性数据管理下的自消耗生成模型
authors: "Xiukun Wei, Xueru Zhang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=UWWNxyIT1h"
tags: ["query:priv-sec"]
score: 7.0
evidence: 对抗性数据管理导致模型崩溃，揭示生成模型漏洞
tldr: 生成模型在自消耗训练循环中使用合成数据，对模型稳定性有风险。本文研究在数据管理中存在对抗性操作时，如何影响模型训练，发现对抗性数据可导致模型崩溃。此项研究对于理解生成模型在迭代训练中的安全漏洞具有重要意义，并为后续防御提供了基础。该工作揭示了即使在没有直接攻击的情况下，恶意数据注入也能破坏模型质量，强调了在生成模型部署中需考虑数据管道的安全性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 对抗性数据管理在自消耗循环中可能导致模型崩溃或训练不稳定。
method: 研究在自消耗训练循环中引入对抗性数据管理的影响。
result: 发现对抗性数据管理会加剧模型崩溃的脆弱性。
conclusion: 揭示了生成模型在对抗性数据下的安全漏洞，需要防御措施。
---

## Abstract
Recent advances in generative models have made it increasingly difficult to distinguish real data from model-generated synthetic data. Using synthetic data for successive training of future model generations creates “self-consuming loops,” which may lead to model collapse or training instability. Furthermore, synthetic data is often subject to human feedback and curated by users based on their preferences. Ferbach et al. (2024) recently showed that when data is curated according to user preferences, the self-consuming retraining loop drives the model to converge toward a distribution that optimizes those preferences. However, in practice, data curation is often noisy or adversarially manipulated. For example, competing platforms may recruit malicious users to adversarially curate data and disrupt rival models. In this paper, we study how generative models evolve under self-consuming retraining loops with noisy and adversarially curated data. We theoretically analyze the impact of such noisy data curation on generative models and identify conditions for the robustness and stability of the retraining process. Building on this analysis, we design attack algorithms for competitive adversarial scenarios, where a platform with a limited budget employs malicious users to misalign a rival’s model from actual user preferences. Experiments on both synthetic and real-world datasets demonstrate the effectiveness of the proposed algorithms.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
对抗性数据管理导致模型崩溃，揭示生成模型漏洞。

### 2. 核心内容
生成模型在自消耗训练循环中使用合成数据，对模型稳定性有风险。本文研究在数据管理中存在对抗性操作时，如何影响模型训练，发现对抗性数据可导致模型崩溃。此项研究对于理解生成模型在迭代训练中的安全漏洞具有重要意义，并为后续防御提供了基础。该工作揭示了即使在没有直接攻击的情况下，恶意数据注入也能破坏模型质量，强调了在生成模型部署中需考虑数据管道的安全性。

### 3. 对应检索需求
security vulnerabilities of generative models。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=UWWNxyIT1h](https://openreview.net/forum?id=UWWNxyIT1h)
