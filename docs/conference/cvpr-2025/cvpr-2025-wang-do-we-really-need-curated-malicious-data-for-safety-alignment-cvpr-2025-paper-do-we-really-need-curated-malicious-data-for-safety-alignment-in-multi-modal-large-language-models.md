---
title: Do We Really Need Curated Malicious Data for Safety Alignment in Multi-modal Large Language Models?
title_zh: 我们真的需要精心策划的恶意数据来实现多模态大语言模型的安全对齐吗？
authors: "Wang, Yanbo, Guan, Jiyang, Liang, Jian, He, Ran"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_Do_We_Really_Need_Curated_Malicious_Data_for_Safety_Alignment_CVPR_2025_paper.pdf"
tags: ["query:priv-sec"]
score: 7.0
evidence: 研究多模态大模型的安全对齐，发现对齐差距主要源于数据分布偏差而非图像内容
tldr: 现有多模态大模型依赖语言模块的安全对齐，对于多模态输入存在安全漏洞。本文通过对比实验发现，对齐差距主要由数据分布偏差导致，并非图像内容本身，在安全分布数据上预训练即可有效缩小差距，无需精心构造恶意数据，为多模态安全对齐提供了新认识。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-do-we-really-need-curated-malicious-data-for-safety-alignment-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1807, \"height\": 815, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-do-we-really-need-curated-malicious-data-for-safety-alignment-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 771, \"height\": 578, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-do-we-really-need-curated-malicious-data-for-safety-alignment-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1804, \"height\": 693, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-do-we-really-need-curated-malicious-data-for-safety-alignment-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 900, \"height\": 689, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-do-we-really-need-curated-malicious-data-for-safety-alignment-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1621, \"height\": 659, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-do-we-really-need-curated-malicious-data-for-safety-alignment-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 858, \"height\": 352, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-do-we-really-need-curated-malicious-data-for-safety-alignment-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 853, \"height\": 388, \"label\": \"Table\"}]"
motivation: MLLM安全对齐依赖语言模块，缺乏针对视觉输入的安全机制，存在攻击漏洞。
method: 通过对比实验分析对齐差距来源，检验数据分布偏差与图像内容的影响。
result: 发现数据分布偏差是主因，图像内容影响有限；在安全数据上预训练可补足对齐。
conclusion: 为多模态安全对齐提供了高效路径，强调数据分布优化而非恶意数据收集。
---

## Abstract
Multi-modal large language models (MLLMs) have made significant progress, yet their safety alignment remains limited. Typically, current open-source MLLMs rely on the alignment inherited from their language module to avoid harmful generations. However, the lack of safety measures specifically designed for multi-modal inputs creates an alignment gap, leaving MLLMs vulnerable to vision-domain attacks such as typographic manipulation. Current methods utilize a carefully designed safety dataset to enhance model defense capability.However, it is unknown what is actually learned in the high-quality dataset.Through comparison experiments, we find that the alignment gap primarily arises from data distribution biases, while image content, response quality, or the contrastive behavior of the dataset makes little contribution to boosting multi-modal safety. To further investigate this and identify the key factors in improving MLLM safety, we propose finetuning MLLMs on a small set of benign instruct-following data with responses replaced by simple, clear rejection sentences.Experiments show that, without the need for labor-intensive collection of high-quality malicious data, model safety can still be significantly improved, as long as a specific fraction of rejection data exists in the finetuning set, indicating the security alignment is not lost but rather obscured during multi-modal pretraining or instruction fine-tuning. Simply correcting the underlying data bias is enough to address the vision domain safety gap.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
研究多模态大模型的安全对齐，发现对齐差距主要源于数据分布偏差而非图像内容。

### 2. 核心内容
现有多模态大模型依赖语言模块的安全对齐，对于多模态输入存在安全漏洞。本文通过对比实验发现，对齐差距主要由数据分布偏差导致，并非图像内容本身，在安全分布数据上预训练即可有效缩小差距，无需精心构造恶意数据，为多模态安全对齐提供了新认识。

### 3. 对应检索需求
security threats and defenses for large language models。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Wang_Do_We_Really_Need_Curated_Malicious_Data_for_Safety_Alignment_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Wang_Do_We_Really_Need_Curated_Malicious_Data_for_Safety_Alignment_CVPR_2025_paper.html)
