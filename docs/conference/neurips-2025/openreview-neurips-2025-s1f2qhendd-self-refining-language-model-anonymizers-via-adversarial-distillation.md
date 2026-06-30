---
title: Self-Refining Language Model Anonymizers via Adversarial Distillation
title_zh: 通过对抗蒸馏实现自改进语言模型匿名器
authors: "Kyuyoung Kim, Hyunjun Jeon, Jinwoo Shin"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=S1F2qhendd"
tags: ["query:priv-sec"]
score: 9.0
evidence: SEAL通过对抗蒸馏训练小模型进行隐私保护文本匿名化，对抗基于LLM的隐私推断
tldr: 大语言模型能从文本中推断个人隐私，引发严重泄露风险。SEAL提出对抗蒸馏框架，利用大模型匿名器与推断模型对抗，生成高质量训练数据，再通过自改进训练将匿名能力蒸馏至小模型，摆脱对昂贵外部API的依赖。实验表明SEAL小模型匿名效果接近甚至优于GPT-4级别的大模型，且成本低、隐私安全性更高。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有LLM匿名化方法依赖外部API，存在成本高和敏感数据再泄露风险。
method: 通过大模型匿名器与推断模型对抗产生训练对，再蒸馏训练小模型，并结合自改进增强性能。
result: SEAL训练的小模型匿名效果媲美大模型，且推理时无需外部调用，隐私安全性提升。
conclusion: SEAL为高效、隐私安全的文本匿名化提供了可部署的小模型方案。
---

## Abstract
Large language models (LLMs) are increasingly used in sensitive domains, where their ability to infer personal data from seemingly benign text introduces emerging privacy risks. While recent LLM-based anonymization methods help mitigate such risks, they often rely on proprietary models (e.g., GPT-4), raising concerns about cost and the potential exposure of sensitive data to untrusted external systems. To address this, we introduce $\textit{SElf-refining Anonymization with Language model}$ (SEAL), a novel distillation framework for training small language models (SLMs) to perform effective anonymization without relying on external models at inference time. SEAL leverages adversarial interactions between an LLM anonymizer and an inference model to collect trajectories of anonymized texts and inferred attributes, which are then used to distill anonymization and critique capabilities into SLMs through supervised fine-tuning and preference learning. The resulting models learn both to anonymize text and to evaluate their outputs, enabling iterative improvement of anonymization quality via self-refinement. Experiments on SynthPAI, a dataset of synthetic personal profiles and text comments, demonstrate that SLMs trained with SEAL achieve substantial improvements in anonymization capabilities. Notably, 8B models attain a privacy-utility trade-off comparable to that of the GPT-4 anonymizer and, with self-refinement, even surpass it in terms of privacy protection. These results highlight the effectiveness of our adversarial distillation framework for training SLMs as efficient anonymizers.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：大语言模型（LLM）能够从看似无害的文本中推断出个人敏感属性（如年龄、性别、位置等），引发严重的隐私泄露风险。现有基于LLM的文本匿名化方法虽然有效，但通常依赖专有外部模型（如GPT-4），这不仅成本高昂，还可能将敏感数据暴露给不受信任的第三方。
- **整体含义**：论文旨在提出一种脱离对外部大模型依赖、能在本地运行且保持高匿名效果的小模型训练框架，以降低部署成本与隐私再泄露风险，推动文本匿名化技术走向实用化。

### 2. 论文提出的方法论
- **核心思想**：通过对抗蒸馏与自改进机制，将大规模匿名模型的匿名能力转移到小型语言模型（SLM）中，使小模型在推理时无需调用外部API即可完成高质量文本匿名化。
- **关键技术细节**（基于摘要与元数据）
  - **对抗数据构建**：利用一个LLM匿名器与一个隐私推断模型进行对抗交互，产生“匿名化文本—推断属性”轨迹对，作为高质量训练数据。
  - **能力蒸馏**：通过监督微调和偏好学习，将匿名化能力和自我评价（critique）能力同时蒸馏到小模型中，使小模型不仅能匿名文本，还能评估自己的输出质量。
  - **自改进（Self-Refinement）**：利用蒸馏得到的自我评估能力，让模型在推理时对自己的输出进行迭代优化，逐步提升匿名化质量。
  - **算法流程**（文字说明）：
    1. 对抗交互阶段：LLM匿名器生成匿名文本，推断模型尝试恢复被隐藏的属性；收集多轮匿名和推断结果。
    2. 蒸馏训练阶段：将收集的轨迹作为训练数据，通过监督学习训练SLM的匿名生成能力；通过偏好学习训练SLM的评价能力。
    3. 自改进阶段：推理时，SLM先生成匿名文本，再用自身评价模块判断隐私保护是否充分，若不充分则进行修正，循环迭代直至满意。
- **公式**：未提供，摘要中无具体公式描述。

### 3. 实验设计
- **数据集**：**SynthPAI**，一个由合成个人资料和文本评论组成的数据集（synthetic personal profiles and text comments）。根据题目推测，该数据集专门设计用于评估个人信息推断与匿名化的效果。
- **评测基准（benchmark）**：主要衡量 **隐私-效用权衡（privacy-utility trade-off）**，即匿名化后文本在多大程度上隐藏了真实属性，同时又保留了文本的原本用途（如语义、可读性等）。
- **对比方法**：
  - 基线匿名化模型：GPT-4级别的匿名器（可能作为最强参照）。
  - 其他未具体说明的方法（摘要中未列出具体对比对象，但提到SLMs trained with SEAL取得显著提升，并与GPT-4匿名器比较）。

### 4. 资源与算力
- **文中提及情况**：给定内容中 **未明确说明** 所使用的GPU型号、数量、训练时长等算力细节。仅知训练的是8B参数规模的小模型，但具体硬件配置未披露。

### 5. 实验数量与充分性
- **估计实验组数**：基于摘要，至少包含以下层面的实验：
  - 不同规模小模型（重点报告了8B模型）的匿名性能对比。
  - 与GPT-4匿名器的直接对比。
  - 自改进（self-refinement）的消融实验（有/无自改进）。
- **充分性与公平性评价**：摘要称“SLMs trained with SEAL achieve substantial improvements”，且能够与GPT-4媲美甚至超越。由于仅提供了摘要，无法判断是否进行了多维度消融、不同数据分布、不同推断模型的全面评估。但给出的结论暗示实验设计较为系统，验证了小模型在对抗蒸馏框架下的有效性。公平性方面，对比的是顶级商业模型，条件较为严苛。

### 6. 论文的主要结论与发现
- 通过SEAL训练的小语言模型（8B规模）能达到与GPT-4匿名器 **可比甚至更优** 的隐私-效用权衡。
- 加入自改进机制后，小模型在隐私保护方面 **超越了** GPT-4匿名器。
- 框架摆脱了推理时对外部API的依赖，显著降低了成本和数据外泄风险，使隐私保护的文本匿名化更加安全、高效。
- **实验证明**：对抗蒸馏与自改进相结合，是训练小型高效匿名器的有效途径。

### 7. 优点
- **方法创新**：首次将对抗蒸馏引入隐私文本匿名化的小模型训练，且结合了自我评估与迭代改进。
- **实用性强**：最终生成的是可本地部署的小模型，无需调用外部昂贵服务，解决了成本和隐私二次泄露的痛点。
- **性能突出**：在8B参数规模下即可匹敌甚至超过GPT-4级别大模型，实现了高效的隐私-效用平衡。
- **自改进能力**：赋予了小模型自我修正的能力，无需外部指导即可在推理时提升匿名质量。

### 8. 不足与局限
- **数据依赖性**：实验基于合成数据集SynthPAI，真实世界文本的复杂性和多样性可能带来性能差距，泛化性尚待验证。
- **对抗蒸馏的稳定性**：依赖初始LLM匿名器和推断模型的能力，如果起始大模型本身存在偏差或性能不足，可能限制最终小模型的上限。
- **隐私推断类型**：摘要未明确攻击模型能够推断的属性类别数量，可能仅覆盖有限的几个隐私属性，面对更广泛的推断任务是否有效未知。
- **小模型容量限制**：8B模型或许已经不小，对于更轻量级的部署场景（如1B以下），SEAL是否还能保持高性能未讨论。
- **资源开销未知**：训练过程中的算力消耗、所需对抗迭代轮次等细节缺失，可能训练本身仍需较大计算资源。

（完）
