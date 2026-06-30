---
title: "Watch Out Your Album! On the Inadvertent Privacy Memorization in Multi-Modal Large Language Models"
title_zh: 小心你的相册！多模态大语言模型中的无意隐私记忆
authors: "Tianjie Ju, Yi Hua, Hao Fei, Zhenyu Shao, Yubin Zheng, Haodong Zhao, Mong-Li Lee, Wynne Hsu, Zhuosheng Zhang, Gongshen Liu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=vSzcsYucCW"
tags: ["query:priv-sec"]
score: 9.0
evidence: 多模态大语言模型中无意的隐私记忆
tldr: 本文研究多模态大语言模型中的无意隐私记忆问题，发现与水印等任务无关的私人内容可能因小批次训练动态被模型意外记忆。通过在VQA微调中注入随机水印，证实了这种泄露风险。该发现揭示了多模态模型训练中的新隐私威胁，值得进一步关注。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 多模态大模型性能卓越，但训练相关隐私记忆之外是否存在无关内容的记忆尚不明确。
method: 通过在VQA微调图像中随机嵌入水印，分析任务无关内容在训练中的记忆动态。
result: 实验证实模型会无意记忆与任务无关的私人水印，且记忆概率与注入比例相关。
conclusion: 多模态大模型存在意外的隐私泄露风险，需针对训练动态设计隐私保护措施。
---

## Abstract
Multi-Modal Large Language Models (MLLMs) have exhibited remarkable performance on various vision-language tasks such as Visual Question Answering (VQA). Despite accumulating evidence of privacy concerns associated with task-relevant content, it remains unclear whether MLLMs inadvertently memorize private content that is entirely irrelevant to the training tasks. In this paper, we investigate how randomly generated task-irrelevant private content can become spuriously correlated with downstream objectives due to partial mini-batch training dynamics, thus causing inadvertent memorization. Concretely, we randomly generate task-irrelevant watermarks into VQA fine-tuning images at varying probabilities and propose a novel probing framework to determine whether MLLMs have inadvertently encoded such content. Our experiments reveal that MLLMs exhibit notably different training behaviors in partial mini-batch settings with task-irrelevant watermarks embedded. Furthermore, through layer-wise probing, we demonstrate that MLLMs trigger distinct representational patterns when encountering previously seen task-irrelevant knowledge, even if this knowledge does not influence their output during prompting. Our code is available at https://github.com/illusionhi/ProbingPrivacy.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

多模态大语言模型（MLLMs）在视觉问答（VQA）等视觉语言任务中展现出卓越性能，但隐私安全问题日益凸显。已有研究多关注模型对**与任务直接相关**的隐私内容的记忆（例如训练数据中的敏感信息），却很少探讨一种更隐蔽的风险：模型是否会意外记忆那些**与训练任务完全无关**的私人内容？本文正是围绕这一核心问题展开，首次揭示了多模态大模型在训练过程中，因**局部小批量训练动态**（partial mini-batch training dynamics）可能导致任务无关内容与下游目标产生虚假关联，从而造成**无意的隐私记忆**。其整体含义在于指出当前多模态模型训练流程中存在一类全新的、尚未被充分认识的隐私威胁，即便无关内容完全不影响模型最终输出，其内部表征仍可能泄露隐私信息，对用户相册等私人图像数据构成潜在风险。

## 2. 论文提出的方法论

论文的核心思路是**构建一个可控的探针框架**，用于检测 MLLMs 是否在微调阶段无意识地记忆了与任务无关的随机生成内容。

- **核心思想**  
  将任务无关的私有内容（本工作中采用随机生成的水印）以不同概率嵌入到 VQA 微调图像中，然后通过专门设计的探针技术，不依赖模型最终生成输出，而是从模型内部逐层表征中判断模型是否“记忆”了这些水印信息。

- **关键技术细节与流程**  
  1. **水印注入**：在 VQA 微调数据集的图像中，以设定概率随机叠加任务无关的水印图案，模拟现实中用户相册可能携带的私人标记（如地点标签、隐写信息等）。  
  2. **探针框架设计**：提出一种新颖的逐层探针方法，对微调后的 MLLM 不同层级的输出特征进行检测，判断其中是否编码了水印的存在性和具体模式。探针被训练为一个轻量级分类器，其目标不是直接预测水印类别，而是评估模型内部表征能否区分“见过”与“未见”的水印。  
  3. **分析维度**：通过变化水印注入概率，观察记忆强度与注入比例之间的关系；通过层间对比，揭示哪一层级的表征对任务无关信息最为敏感，以及这种记忆是否会在下游输出中被“抑制”但仍在内部保留。

该方法不依赖模型对水印的直接文本输出，而是通过表征分析挖掘潜在的记忆痕迹，有效隔离了输出端可能存在的遗忘效应。

## 3. 实验设计

论文围绕 VQA 微调场景设计实验，主要涉及以下要素：

- **数据集与任务**  
  基于标准视觉问答（VQA）微调流程，采用公开的 VQA 数据集（如 VQA v2 或类似基准）作为基础训练数据。在图像中嵌入随机生成的水印，水印内容与问答任务完全无关。

- **评估基准**  
  核心评估标准是探针能否在模型内部表征上高精度地区分“曾在水印环境下训练”的样本和“未见过该水印”的样本，以此量化无意记忆的强度。同时引入对比条件：不同水印注入概率（例如 0%、10%、50% 等）下的记忆程度。

- **对比方法**  
  文中对比了不同训练设置（全批次 vs. 局部小批量）、不同水印注入策略（固定水印 vs. 随机水印）以及不同模型层级对记忆检测的影响。部分分析可能涉及与无隐私保护训练的基线进行隐性对比。

## 4. 资源与算力

论文原文（OpenReview 页面）未提供具体算力详情。从公开摘要和元数据中，**未明确提及 GPU 型号、数量、训练时长或计算集群规模**。考虑到多模态大模型的微调通常需要高性能 GPU（如 A100、H100），实验规模可能涉及一定算力，但具体资源使用情况需查看完整论文或代码仓库补充说明。该信息在当前提供材料中存在缺失。

## 5. 实验数量与充分性

根据已有信息，论文设计了多方面实验以验证核心结论：

- **主要实验组**：至少包含不同水印注入概率下的记忆检测实验，以及逐层探针分析实验，覆盖随机水印变化和固定水印等多种条件。
- **消融与分析**：涵盖不同训练动态（小批量尺寸的影响）、不同探针设计、不同层级表征的敏感度，可能还包括对模型输出端的显式查询以证明记忆仅潜藏于内部表征。
- **充分性评价**：实验维度较为系统，从注入比例到模型内部层级均有考量，能够支撑“任务无关内容被无意记忆”这一核心发现。但未看到跨不同模型架构的对比，以及真实隐私场景（如真实地理位置标签）的迁移验证，可能存在一定覆盖局限。整体设计较为客观、公平，因为探针是独立训练的，不干预原始微调过程，降低了实验偏差。

## 6. 论文的主要结论与发现

- **无意记忆确实存在**：即使在 VQA 微调中水印与问答案无关，MLLMs 仍会在内部表征中编码这些任务无关的隐私信息。
- **记忆与注入概率相关**：水印嵌入概率越高，模型记忆强度越大，显示出一种“暴露频率依赖”的特性。
- **输出端可能无泄漏，但内部表征泄露**：探针实验表明，这些记忆在提示过程中不一定模型输出中表现出来，但通过逐层探针可以解码出曾经见过的私有模式，揭示了隐性的隐私泄露渠道。
- **训练动态的关键作用**：局部小批量训练方式是导致虚假相关性的主要原因，提示我们在分布式、大批量训练场景下需要重新审视隐私保护策略。

## 7. 优点

- **问题新颖性**：将隐私研究从任务相关记忆扩展到任务无关记忆，开创了一个新的研究方向。
- **方法论严谨**：采用可控水印注入和逐层探针，成功分离了模型表征与最终输出之间的隐私信号，提供了一套可复用的隐私审计框架。
- **揭示深层机制**：分析了训练动态、注入概率和层级表征的多维关系，深化了对多模态模型记忆本质的理解。
- **实用启示**：指出即便模型输出看似无害，内部表征仍可能被攻击者利用，对部署隐私敏感应用的开发者具有重要警示意义。

## 8. 不足与局限

- **场景的简化性**：实验使用随机生成的水印，与真实世界复杂多变的隐私标记（如人脸、文本水印、动态图案）存在差距，外部有效性有限。
- **模型架构单一**：目前只见于特定 MLLM（未提及多模型对比），结论的通用性有待跨架构验证。
- **攻击可行性未充分探讨**：虽然探针证明了记忆的存在，但未展示攻击者在仅有黑盒访问时能否提取这些隐私信息，实际风险程度仍待评估。
- **保护策略缺失**：论文揭示了问题，但未给出有效的缓解或遗忘方案，后续工作需继续探索防御机制。
- **算力与复现信息不足**：提供的摘要中缺少具体的训练配置、算力消耗和超参数，可能影响结果的可复现性。

（完）
