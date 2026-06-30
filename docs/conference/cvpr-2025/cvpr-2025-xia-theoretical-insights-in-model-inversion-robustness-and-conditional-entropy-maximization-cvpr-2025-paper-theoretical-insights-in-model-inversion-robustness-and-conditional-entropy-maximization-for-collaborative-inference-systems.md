---
title: Theoretical Insights in Model Inversion Robustness and Conditional Entropy Maximization for Collaborative Inference Systems
title_zh: 协同推理系统中模型反演鲁棒性与条件熵最大化的理论洞察
authors: "Xia, Song, Yu, Yi, Yang, Wenhan, Ding, Meiwen, Chen, Zhuo, Duan, Ling-Yu, Kot, Alex C., Jiang, Xudong"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Xia_Theoretical_Insights_in_Model_Inversion_Robustness_and_Conditional_Entropy_Maximization_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 8.0
evidence: 针对协同推理中模型反演攻击的隐私保护理论方法
tldr: 针对协同推理中通过中间特征泄露原始数据的模型反演攻击，本文从理论层面分析任务无关冗余，并提出条件熵最大化方法来增强反演鲁棒性。通过最大化条件熵，在不影响任务性能的前提下有效混淆中间特征，从而保护隐私。实验证明该方法能显著降低重建攻击的成功率，为隐私保护协同推理提供了可量化的优化框架。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xia-theoretical-insights-in-model-inversion-robustness-and-conditional-entropy-maximization-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 770, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xia-theoretical-insights-in-model-inversion-robustness-and-conditional-entropy-maximization-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1623, \"height\": 611, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xia-theoretical-insights-in-model-inversion-robustness-and-conditional-entropy-maximization-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 675, \"height\": 536, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xia-theoretical-insights-in-model-inversion-robustness-and-conditional-entropy-maximization-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1798, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-xia-theoretical-insights-in-model-inversion-robustness-and-conditional-entropy-maximization-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 821, \"height\": 411, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xia-theoretical-insights-in-model-inversion-robustness-and-conditional-entropy-maximization-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 687, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xia-theoretical-insights-in-model-inversion-robustness-and-conditional-entropy-maximization-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 882, \"height\": 704, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-xia-theoretical-insights-in-model-inversion-robustness-and-conditional-entropy-maximization-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 875, \"height\": 699, \"label\": \"Table\"}]"
motivation: 协同推理中，编码的中间特征仍可能被模型反演攻击还原原始数据，现有混淆方法缺乏对任务无关冗余的数学量化，难以理论指导防御设计。
method: 理论建模任务无关冗余，提出基于条件熵最大化的优化框架，在训练中最大化中间特征相对于敏感属性的条件熵，以增强反演鲁棒性。
result: 实验证明，该方法在多个数据集上显著降低了模型反演重建的准确率，同时保持下游任务性能，优于现有噪声添加等启发式防御。
conclusion: 本研究为隐私保护协同推理提供了可量化的理论工具，首次建立条件熵与反演鲁棒性的直接联系，为设计可证明的隐私防御开辟了新路径。
---

## Abstract
By locally encoding raw data into intermediate features, collaborative inference enables end users to leverage powerful deep learning models without exposure of sensitive raw data to cloud servers. However, recent studies have revealed that these intermediate features may not sufficiently preserve privacy, as information can be leaked and raw data can be reconstructed via model inversion attacks (MIAs). Obfuscation-based methods, such as noise corruption, adversarial representation learning, and information filters, enhance the inversion robustness by obfuscating the task-irrelevant redundancy empirically. However, methods for quantifying such redundancy remain elusive, and the explicit mathematical relation between this redundancy and worst-case robustness against inversion has not yet been established. To address that, this work first theoretically proves that the conditional entropy of inputs given intermediate features provides a guaranteed lower bound on the reconstruction mean square error (MSE) under any MIA. Then, we derive a differentiable and solvable measure for bounding this conditional entropy based on the Gaussian mixture estimation and propose a conditional entropy maximization (CEM) algorithm to enhance the inversion robustness. Experimental results on four datasets demonstrate the effectiveness and adaptability of our proposed CEM; without compromising the feature utility and computing efficiency, integrating the proposed CEM into obfuscation-based defense mechanisms consistently boosts their inversion robustness, achieving average gains ranging from 12.9% to 48.2%. Code is available at \href https://github.com/xiasong0501/CEM https://github.com/xiasong0501/CEM .

---

## 论文详细总结（自动生成）

### 1. 检索相关性
针对协同推理中模型反演攻击的隐私保护理论方法。

### 2. 核心内容
针对协同推理中通过中间特征泄露原始数据的模型反演攻击，本文从理论层面分析任务无关冗余，并提出条件熵最大化方法来增强反演鲁棒性。通过最大化条件熵，在不影响任务性能的前提下有效混淆中间特征，从而保护隐私。实验证明该方法能显著降低重建攻击的成功率，为隐私保护协同推理提供了可量化的优化框架。

### 3. 对应检索需求
privacy risks in generative models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Xia_Theoretical_Insights_in_Model_Inversion_Robustness_and_Conditional_Entropy_Maximization_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Xia_Theoretical_Insights_in_Model_Inversion_Robustness_and_Conditional_Entropy_Maximization_CVPR_2025_paper.html)
