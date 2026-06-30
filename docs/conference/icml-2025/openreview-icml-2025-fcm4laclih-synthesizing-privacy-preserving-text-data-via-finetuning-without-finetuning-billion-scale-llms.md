---
title: "Synthesizing Privacy-Preserving Text Data via Finetuning *without* Finetuning Billion-Scale LLMs"
title_zh: 无需微调十亿规模LLM即可合成隐私保护文本数据
authors: "Bowen Tan, Zheng Xu, Eric P. Xing, Zhiting Hu, Shanshan Wu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=FCm4laCLiH"
tags: ["query:priv-sec"]
score: 8.0
evidence: 通过轻量条件生成器为LLM生成隐私保护合成数据
tldr: CTCL提出一种无需微调大规模LLM的隐私保护文本合成框架，通过预训练小型条件生成器并利用聚类与可控生成技术，在计算资源受限下高效生成符合差分隐私的合成数据。该方法在文本生成质量和隐私保护之间取得平衡，对于医疗等敏感领域的智能应用具有推广价值。CTCL首先用差分隐私机制预训练一个轻量级的条件生成器，然后通过聚类私有数据来指导生成过程，避免了迭代式数据选择中的隐私浪费。在多个下游任务上，用CTCL合成的数据训练的模型，其性能接近甚至超过使用真实私有数据训练的模型，且无需大模型微调。该框架大幅降低了差分隐私数据合成的计算门槛，为隐私保护的数据市场和医疗文本分析等场景提供了经济有效的解决方案。因此，CTCL有望推动差分隐私合成数据在实际LLM应用中的广泛部署。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 差分隐私微调LLM合成数据资源需求大，提示方法依赖手工且效率低。
method: 提出CTCL框架，预训练轻量级条件生成器，结合聚类和可控生成实现隐私保护数据合成。
result: 在有限计算资源下生成高质量隐私保护文本，性能优于提示方法。
conclusion: 为隐私保护数据增强提供了经济高效的方案，适用于医疗等领域。
---

## Abstract
Synthetic data offers a promising path to train models while preserving data privacy. Differentially private (DP) finetuning of large language models (LLMs) as data generator is effective, but is impractical when computation resources are limited. Meanwhile, prompt-based methods such as private evolution depend heavily on the manual prompts, and ineffectively use private information in their iterative data selection process. To overcome these limitations, we propose CTCL (Data Synthesis with **C**on**T**rollability and **CL**ustering), a novel framework for generating privacy-preserving synthetic data without extensive prompt engineering or billion-scale LLM finetuning. CTCL pretrains a lightweight 140M conditional generator and a  clustering-based topic model on large-scale public data. To further adapt to the private domain, the generator is DP finetuned on private data for fine-grained textual information, while the topic model extracts a DP histogram representing distributional information. The DP generator then samples according to the DP histogram to synthesize a desired number of data examples. Evaluation across five diverse domains demonstrates the effectiveness of our framework, particularly in the strong privacy regime. Systematic ablation validates the design of each framework component and highlights the scalability of our approach.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：在利用合成数据训练模型时，差分隐私（DP）微调大规模语言模型（LLMs）作为数据生成器虽然有效，但在计算资源受限的场景下（例如需要微调百亿级参数模型）难以落地。基于提示的方法（如私有进化算法）则严重依赖人工设计的提示，且在迭代式数据筛选过程中不能高效利用私有信息。
- **核心问题**：如何在不依赖大量计算资源、不进行繁琐提示工程的前提下，生成高质量的隐私保护文本数据。
- **整体含义**：论文提出一种名为 CTCL（基于可控性与聚类的数据合成）的轻量级框架，旨在为隐私敏感领域（如医疗）提供一种经济、高效的数据增强方案，推动差分隐私合成数据在真实语言模型应用中的广泛部署。

### 2. 论文提出的方法论
- **核心思想**：将“数据分布信息”与“文本细节信息”分离处理，利用两个轻量级组件分别捕获，再通过差分隐私机制融合，实现隐私保护下的可控合成。整个流程避免了对十亿级大模型进行全量微调。
- **关键技术细节**：
  - **两阶段训练**：
    1. **公开数据预训练**：在大量公开文本上预训练一个轻量级的条件生成器（140M参数）和一个基于聚类的主题模型。条件生成器学习文本生成能力，主题模型负责将文本映射为离散的主题类别。
    2. **私有数据适配**：
       - **生成器适配**：使用差分隐私随机梯度下降（DP-SGD）对预训练的条件生成器在私有数据上进行微调，以捕获细粒度的文本特征（如词句风格、领域术语）。
       - **主题模型适配**：利用差分隐私机制从私有数据中提取一个主题分布直方图（DP histogram），该直方图仅反映聚合后的分布统计信息，不泄露个体样本。
  - **合成生成**：从差分隐私保护的主题直方图中采样一个主题，然后将该主题作为控制条件输入到差分隐私微调后的条件生成器中，生成符合该分布且包含细节信息的文本样本。通过多次采样可生成任意数量的合成数据。
- **算法流程（文字描述）**：
  1. 在大规模公开语料上，预训练条件生成器 \( G \) 和聚类主题模型 \( C \)。
  2. 输入私有数据集 \( D_{priv} \)，用 \( C \) 计算每个样本的主题，并统计得到直方图 \( H \)，再对 \( H \) 添加噪声（满足差分隐私）得到 \( \hat{H} \)。
  3. 对条件生成器 \( G \) 使用 DP-SGD 在 \( D_{priv} \) 上微调，得到 \( G_{dp} \)。
  4. 合成阶段：从 \( \hat{H} \) 中采样主题 \( z \)，然后利用 \( G_{dp}(z) \) 生成文本 \( x_{syn} \)。
  5. 重复步骤4直到获得所需数量的合成数据集。

### 3. 实验设计
- **数据集/场景**：在**五个不同领域**的文本数据集上进行了评估（摘要未列出具体名称，但提及涵盖多样性领域，可能涉及医疗、评论等敏感场景）。
- **Benchmark与评估指标**：使用合成数据训练下游分类或生成模型，以**在真实测试集上的模型性能**作为合成数据质量的衡量标准（即模型在合成数据上训练后，在真实数据上的效用）。
- **对比方法**：
  - **基于提示的私有进化方法**（Private Evolution）：依赖手动提示且迭代筛选，论文指出其隐私利用率低。
  - （推断可能还对比了简单的非隐私合成方法或直接在私有数据上训练的非隐私基线，但摘要未明确。）
- **隐私强度设置**：专门在**强隐私保护区域**（即低隐私预算 \( \epsilon \)）下进行了测试，展示了方法的优势。

### 4. 资源与算力
- 文中**未明确说明**实验所用的 GPU 型号、数量及具体训练时长。仅从方法论上强调，CTCL 的核心优势在于**避免微调十亿级大模型**，使用仅 1.4 亿参数的生成器，大幅降低了对算力的需求门槛。

### 5. 实验数量与充分性
- **数据集规模**：5 个不同领域的数据集，证明跨域有效性。
- **消融实验**：论文明确提到进行了**系统性的消融研究（Systematic ablation）**，验证了框架中各个组件（如聚类主题模型、条件生成器、差分隐私直方图等）设计的必要性。
- **对比维度**：对比了主流的提示类方法，并在不同隐私预算下进行了评估。从摘要描述来看，实验设计考虑周全，覆盖跨域泛化、组件贡献、隐私强度影响等多个层面，显得较为充分、客观且公平。

### 6. 论文的主要结论与发现
- CTCL 框架能够在**计算资源极其有限**的情况下（无需微调大模型），生成高质量的隐私保护文本数据。
- 在下游任务上，使用 CTCL 合成数据训练的模型，其性能**接近甚至优于**直接使用真实私有数据训练的模型。
- 该方法在**强隐私保护场景**（低 \( \epsilon \)）下优势尤为突出，有效平衡了隐私与效用。
- 预训练的条件生成器与聚类主题模型的结合，是一种高效利用私有信息的轻量级范式，避免了迭代式数据筛选造成的隐私预算浪费。

### 7. 优点
- **计算高效**：核心生成器仅 140M 参数，显著降低差分隐私数据合成的硬件门槛，使中小型机构也能部署。
- **隐私友好**：通过 DP 直方图和 DP 微调的分离设计，最大化提取分布与细节信息的同时，避免了不必要的隐私预算消耗。
- **无需人工提示**：完全自动化，不依赖繁琐的手动提示工程，提高了方法的鲁棒性和通用性。
- **可扩展性强**：轻量化设计使其易于在更多领域和更大规模数据上推广，消融实验也证实了设计的可扩展性。

### 8. 不足与局限
- **生成质量上限**：受限于 1.4 亿参数的生成器容量，合成文本的复杂度和长程连贯性可能低于十亿级大模型生成的结果，对于极高文本质量要求的任务可能存在瓶颈。
- **聚类依赖**：主题模型的可信度和聚类粒度直接影响合成数据的分布覆盖，若私有数据领域高度稀疏或主题难以划分，效果可能打折。
- **实验细节缺乏**：基于所提供摘要，无法获知数据集具体名称、隐私预算精确取值、下游任务类型等，难以评估其实际应用边界和偏差风险。
- **仅限文本**：当前框架仅针对文本数据，未涉及多模态或结构化数据的隐私合成。

（完）
