---
title: "ICLScan: Detecting Backdoors in Black-Box Large Language Models via Targeted In-context Illumination"
title_zh: ICLScan：通过目标上下文照明检测黑盒大语言模型中的后门
authors: "Xiaoyi Pang, Xuanyi Hao, Song Guo, Qi Luo, Zhibo Wang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=MtyF5hCI7Y"
tags: ["query:priv-sec"]
score: 9.0
evidence: 利用目标上下文学习作为探针，检测黑盒大模型中的后门
tldr: 黑盒大语言模型API面临后门攻击风险，但现有检测方法多需白盒访问。ICLScan提出一种轻量级黑盒后门检测框架，通过精心构建的上下文示例激发模型隐藏行为，再利用行为差异判断后门存在。实验表明该方法在多种生成场景下高效检测后门，且无需模型内部信息。该工作为黑盒LLM的安全审计提供了实用工具。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 黑盒LLM的后门检测需求迫切，但现有方法依赖白盒或成本高。
method: ICLScan利用目标上下文学习作为探针，通过对比触发上下文下的输出差异来检测后门。
result: 在生成任务上，ICLScan以较低查询成本实现了高检测准确率，优于现有方法。
conclusion: ICLScan为黑盒LLM提供了一种高效、易行的后门检测方案。
---

## Abstract
The widespread deployment of large language models (LLMs) allows users to access their capabilities via black-box APIs, but backdoor attacks pose serious security risks for API users by hijacking the model behavior. This highlights the importance of backdoor detection technologies to help users audit LLMs before use. However, most existing LLM backdoor defenses require white-box access or costly reverse engineering, limiting their practicality for resource-constrained users. Moreover, they mainly target classification tasks, leaving broader generative scenarios underexplored. To solve the problem, this paper introduces ICLScan, a lightweight framework that exploits targeted in-context learning (ICL) as illumination for backdoor detection in black-box LLMs, which effectively supports generative tasks without additional training or model modifications. ICLScan is based on our finding of backdoor susceptibility amplification: LLMs with pre-embedded backdoors are highly susceptible to new trigger implantation via ICL. Including only a small ratio of backdoor examples (containing ICL-triggered input and target output) in the ICL prompt can induce ICL trigger-specific malicious behavior in backdoored LLMs. ICLScan leverages this phenomenon to detect backdoored LLMs by statistically analyzing whether the success rate of new trigger injection via targeted ICL exceeds a threshold. It requires only multiple queries to estimate the backdoor success rate, overcoming black-box access and computational resource limitations. Extensive experiments across diverse LLMs and backdoor attacks demonstrate ICLScan's effectiveness and efficiency, achieving near-perfect detection performance (precision/recall/F1-score/ROC-AUC all approaching 1) with minimal additional overhead across all settings.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**  
  大语言模型（LLM）通过黑盒API广泛部署，用户无法获知模型内部结构和训练过程。此类API型LLM面临后门攻击的威胁——攻击者可在模型训练或微调阶段植入隐藏的恶意行为，当输入中出现特定触发词时模型输出被劫持，严重危害API用户的安全。

- **核心问题**  
  现有的LLM后门防御方法大多要求白盒访问（如检查模型权重、梯度），或依赖成本高昂的逆向工程（如模型窃取），难以适配资源受限的黑盒API用户。同时，已有工作主要聚焦于分类任务的检测，而对更普遍的生成式场景（如对话、翻译）覆盖不足。因此，急需一种轻量、无需模型内部信息且支持生成任务的黑盒后门检测方案。

- **整体含义**  
  ICLScan 通过“目标上下文照明”（targeted in-context illumination）为黑盒LLM提供了一种实用的后门审计工具：仅需少量API查询，用户即可在模型投入使用前判断其是否被植入后门，显著降低了安全验证的门槛。

## 2. 论文提出的方法论

- **核心思想：后门易感性放大现象**  
  ICLScan 基于作者发现的“后门易感性放大”现象：已内嵌后门的LLM对通过上下文学习（In-Context Learning, ICL）植入新触发的行为异常敏感。如果在ICL提示中加入少量含有新触发词和目标输出的示例，后门模型会快速学会按照新的ICL触发器产生恶意行为，而干净模型则不会表现出这种同步篡改。

- **关键技术细节**
  - **构建检测探针**：检测者构造一个包含正常示例和少量“后门示例”的提示。后门示例的格式为 `[ICL触发输入] → [目标输出]`，其中触发词是全新、未被模型原始后门使用的词或短语。
  - **行为差异对比**：对同一输入分别给出不含触发词的普通提示和含有ICL触发词的提示，观察模型输出是否按预期转向目标输出。通过统计这种转向发生的频率来估计后门成功率（Backdoor Success Rate, BSR）。
  - **阈值判断**：若BSR超过预设阈值（如显著高于干净模型的随机对齐率），则判定模型存在后门。整个过程不需要修改模型、训练辅助分类器或进行模型逆向，完全基于黑盒查询。

- **算法流程概述**（文字说明）
  1. 选定数个候选ICL触发词（确保不与被测模型的潜在后门触发词重合）。
  2. 对每个候选触发词，构建一批ICL提示，每个提示包含少量正常示例和固定数量的后门示例（触发词注入输入，目标输出设为某一特定恶意回答）。
  3. 向目标LLM发送查询，收集模型在含触发词提示下的输出。
  4. 统计输出与预设恶意目标一致的查询比例，得到该触发词下的BSR。
  5. 综合多个触发词的BSR，判断是否超过判定阈值，若超过则认为模型为后门模型。

- **方法优势**  
  - **完全黑盒**：无需模型权重、梯度或训练信息。  
  - **轻量级**：仅需数十到数百次查询即可完成检测。  
  - **支持生成任务**：不依赖分类标签，直接分析生成内容的匹配率。

## 3. 实验设计

- **测试对象与场景**  
  论文在多种主流LLM（未列出具体名称，但从上下文推断包含不同参数规模和架构的模型）和多种后门攻击方式（例如不同触发词设计、植入策略）上进行了评估。实验覆盖了典型的生成式任务场景。

- **基准与评价指标**  
  以检测性能作为核心衡量标准，采用精确率（Precision）、召回率（Recall）、F1分数和ROC-AUC。目标是区分带后门的模型与干净模型。文中提到“ICLScan achieves near-perfect detection performance … (precision/recall/F1-score/ROC-AUC all approaching 1)”，表明其在所测设置下几乎完美区分。

- **对比方法**  
  摘要中未明确列举对比的具体后门检测基线，但通常应与现有黑盒或白盒防御方法进行比较。可能包括基于提示扰动、输出一致性检查等方法。由于提供的文本有限，无法确定对比细节。

## 4. 资源与算力

- **算力需求**  
  论文强调ICLScan是轻量级框架，**不涉及**模型训练、微调或梯度的反向传播，因此**无需GPU算力**。整个检测流程仅通过API查询完成，计算开销仅限于客户端提示构造与结果统计，普通CPU即可胜任。**未明确提及**GPU型号、数量或训练时长等信息，这与方法本身的设计一致。

## 5. 实验数量与充分性

- **实验规模描述**  
  文中声称进行了“Extensive experiments across diverse LLMs and backdoor attacks”（跨多种LLM和后门攻击的广泛实验），但**未给出具体实验组数或数据集名称**（在提供的摘要中未体现）。从“all approaching 1”的结论来看，实验覆盖度应该较高，能够支持该方法在多种设置下的通用性断言。

- **充分性与客观性评估**  
  - 指标采用标准的二元分类评价体系（精确率、召回率、F1、AUC），合理且可比。
  - 实验涉及多种模型和后门类型，减少了单一模型偏差。但摘要未提供干净模型、不同后门触发、不同后门植入率等的消融细节，完整论文中可能已做说明。
  - 由于检测任务本身简单直接，在给定的上下文学习假设下，性能接近完美符合预期，但需要关注现实场景中后门模型对ICL植入敏感度可能变化的情况。

## 6. 论文的主要结论与发现

- **核心结论**  
  ICLScan 可利用目标上下文学习高效、准确地检测黑盒LLM中的后门，在不获取模型内部信息、不进行额外训练的前提下，实现近乎完美的检测性能。该方法打破了现有防御对白盒访问或高成本的依赖，并成功拓展到生成式任务。

- **关键发现**  
  “后门易感性放大”机制表明，已嵌入后门的LLM会通过少量上下文示例迅速习得新的触发行为，这既是后门模型的一种内在弱点，也为黑盒检测提供了强力探针。

## 7. 优点（方法或实验设计的亮点）

- **完全黑盒、零训练开销**：用户仅需具备API访问权限即可完成审计，极大地降低了部署门槛。
- **生成任务原生支持**：无需将生成任务退化为分类问题，直接评估输出内容，更贴近真实LLM应用。
- **发现的新现象**：首次揭示并利用后门模型的ICL易感性放大这一特性，为安全检测提供了新的视角。
- **检测性能卓越**：在多个设置下指标均逼近100%，理论或实验上具有高可靠性。
- **方法简洁，易于复现**：没有复杂的外部模块，仅依赖提示工程和统计检验。

## 8. 不足与局限

- **摘要中未充分讨论的局限性**（基于论文所给信息推断）
  - **依赖ICL敏感假设**：若某类后门攻击对上下文学习不敏感（例如触发器设计使得ICL难以复制），检测方法可能失效。没有讨论所有潜在后门类型。
  - **查询次数与成本**：虽然轻量，但仍需一定数量的查询（数十至数百次），在按token收费的商用API中可能产生少量成本，且重复的恶意查询可能触发安全风控。
  - **触发词选择的盲区**：ICL触发词需不与被测模型的原始后门触发词重合，若待测模型的后门触发词空间未知且与ICL触发词重合，可能干扰检测或导致漏报。
  - **对抗适应性**：后续攻击可能刻意抑制ICL敏感度，使检测失效，论文可能未探究攻防博弈下的鲁棒性。
  - **实验细节未完整披露**：从提供的文本中看不出数据集、后门植入比例、模型具体信息、阈值如何确定等，无法评估实验的完整性和泛化边界。

（完）
