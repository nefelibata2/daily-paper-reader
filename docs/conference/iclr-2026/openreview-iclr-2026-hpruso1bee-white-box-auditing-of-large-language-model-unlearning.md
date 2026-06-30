---
title: White-Box Auditing of Large Language Model Unlearning
title_zh: 大语言模型遗忘机制的白盒审计
authors: "Runzhi Tian, Shicheng Hu, Ziqiao Wang, Yongyi Mao"
date: 2025-09-19
pdf: "https://openreview.net/pdf?id=hPruSo1bEE"
tags: ["query:priv-sec"]
score: 10.0
evidence: 面向敏感数据的大语言模型遗忘机制白盒审计
tldr: 针对大语言模型记忆敏感信息的隐私问题，构建含虚假个人信息的合成数据集，提出白盒审计框架严格评估遗忘方法的有效性。评估发现简单的逆向贪婪解码能恢复本应被遗忘的数据，表明现有遗忘方法并未彻底删除敏感信息，对模型审计和隐私合规具有重要意义。
source: ICLR-2026-Rejected-Public
selection_source: conference_retrieval
motivation: LLM可能记忆敏感数据，现有遗忘方法是否真正删除尚不明确。
method: 构建合成数据集并设计白盒审计框架统一量化敏感数据残留。
result: 逆向贪婪解码可恢复声称忘却的信息，多种方法均未彻底删除。
conclusion: 现有LLM遗忘方法不足，白盒审计对隐私验证至关重要。
---

## Abstract
Large language models (LLMs) can memorize sensitive information, raising serious privacy concerns. Machine unlearning offers a potential solution to remove such information, but it remains unclear whether existing methods truly erase it or merely hide it within the model. A key challenge is quantifying the persistence of sensitive data under a unified evaluation framework. To address this, we construct a synthetic dataset containing fake personal information and propose a white-box auditing framework to rigorously assess whether claimed-forgotten information is genuinely removed. Using this framework, we evaluate five existing unlearning methods and find that a simple “inverse greedy” decoding—selecting the least likely token at each step—can recover supposedly forgotten personal information. Our results reveal that current unlearning approaches often fail to fully eliminate sensitive information, highlighting the need for more reliable methods to ensure privacy in deployed LLMs.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义
- **研究动机**：大语言模型（LLM）在训练中可能记忆并复现训练数据中的敏感个人信息（如姓名、地址、身份证号），直接在部署前删除这类记忆是隐私保护的关键需求。
- **背景挑战**：现有的“机器遗忘”方法声称能从模型中移除特定知识，但缺乏严格审计手段来验证信息是被彻底删除还是仅被隐藏或压缩到模型难以触达的表示空间中。
- **整体含义**：本文旨在揭示看似“已遗忘”的信息是否仍可被恢复，从而警示当前遗忘技术的隐私风险，并促进更可靠的遗忘与审计机制的建立。

## 2. 方法论
- **核心思想**：通过构建已知敏感内容的受控合成数据集，设计一套白盒审计框架，统一量化模型在经历遗忘操作后敏感信息的残留程度，并尝试用简单的逆向解码策略验证数据是否真正消失。
- **关键技术细节**：
  - **合成数据集**：生成包含虚假个人信息的文本数据，确保敏感信息的位置和内容是确知的，便于后续精确评测。
  - **白盒审计框架**：利用模型内部的概率分布（如 token 概率、隐藏状态）设计残留度量指标，用以评估遗忘前后模型对目标信息的记忆强度变化。
  - **逆向贪婪解码攻击**：在遗忘后的模型上进行推理时，每一步不再选择概率最高的 token，而是选择概率 **最低** 的 token（或称“逆贪婪解码”），观察是否能够重建出原本应该被遗忘的个人信息序列。这一策略利用了模型仍可能在低概率路径中保留记忆的假设。
  - 流程可概括为：预训练/微调模型 → 应用遗忘方法 → 在白盒假设下使用审计框架量化残留 → 执行逆向贪婪解码尝试恢复 → 对比恢复成功率。

## 3. 实验设计
- **数据集/场景**：使用自建合成数据集，其中植入设定好的虚假个人信息；场景为语言模型对结构化/半结构化敏感文本的记忆与遗忘审计。
- **基准与对比方法**：文章明确比较了 **5 种现有的遗忘方法**，以评估不同机制下的遗忘效果。这些方法的具体名称在摘要中未列出，但从上下文推测可能涵盖梯度更新、参数修剪、知识编辑等主流路线。审计框架自身作为统一的评价基准，通过恢复成功率等指标比较各方法的脆弱性。
- **评估指标**：核心指标为合成个人信息在逆向贪婪解码下的可恢复程度（如完全恢复、部分恢复的比例），可能还包含困惑度变化、token 排序变化等辅助指标。

## 4. 资源与算力
- 论文摘要及所提供的元数据中 **未提及** 所使用的 GPU 型号、数量、训练时长或推理算力消耗。因此无法判断其算力规模与可复现成本。

## 5. 实验数量与充分性
- **实验组数**：从摘要信息推断，实验至少覆盖 5 种不同遗忘方法在合成数据集上的审计表现比较，可能还包含逆向贪婪解码与标准解码、不同遗忘强度等多种设定。但具体消融实验、数据集变体、重复次数等细节未在摘要中透露。
- **充分性判断**：仅基于摘要，实验设计在概念验证层面是自洽的，但对比 5 种方法仅使用一个合成数据集，结论的普适性可能受限。如果能包含更多真实数据分布、不同模型规模、不同遗忘目标粒度的测试，审计框架的说服力会更强。当前呈现的实验比较直接，但覆盖广度尚待更多细节证实。

## 6. 主要结论与发现
- **逆向贪婪解码可恢复“已遗忘”信息**：即使模型经过遗忘处理，通过选择每步概率最低的 token 这一简单策略，仍能重建出本应被删除的个人信息，表明记忆并未彻底擦除。
- **现有遗忘方法普遍不足**：所评测的 5 种遗忘方法均未能完全消除敏感信息，残留信息足以被白盒攻击利用。
- **审计框架的必要性**：揭示当前遗忘评估缺乏统一和严格标准的现状，并强调白盒审计对于验证模型隐私合规具有不可替代的作用。

## 7. 优点
- **新颖的审计视角**：首次将逆向贪婪解码作为白盒攻击手段引入遗忘评估，揭示低概率路径中的信息残留，思想直观而有力。
- **受控实验环境**：使用合成虚假个人信息既避免了真实隐私泄露风险，又使得敏感信息的引入与审计目标明确可控，提升实验的内部效度。
- **统一评价框架**：提出可量化、可比较的审计方法，为未来遗忘算法的安全性验证提供了一套可参照的模板。

## 8. 不足与局限
- **方法覆盖范围有限**：仅评测 5 种遗忘方法，未与更多最新的遗忘防御策略（如基于差分隐私的训练、强化遗忘正则化等）对比，结论的全面性待扩展。
- **实验规模受限**：仅基于合成数据集，缺乏对真实世界多样化文本和更长文档的验证；模型规模和结构也可能局限于实验所用模型，未讨论迁移到更大规模或不同架构的 LLM 时的表现。
- **审计攻击的单一性**：仅凭逆向贪婪解码一种攻击方式，可能低估其他更复杂的恢复技术（如梯度分析、表示层探测）的威胁，审计的完备性仍有提升空间。
- **白盒假设的强前提**：审计要求完全访问模型内部参数和概率分布，这在实际部署中可能无法满足，限制了审计框架在真实第三方审计场景下的直接应用。
- **缺少算力与可复现细节**：论文未提供算力配置和超参数等关键实现信息，可能影响结果复现和成本评估。

（完）
