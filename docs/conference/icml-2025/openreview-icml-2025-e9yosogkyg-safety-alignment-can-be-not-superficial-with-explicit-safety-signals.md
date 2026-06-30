---
title: Safety Alignment Can Be Not Superficial With Explicit Safety Signals
title_zh: 加入显式安全信号可使安全对齐不再表面化
authors: "Jianwei Li, Jung-Eun Kim"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=e9YosoGkYg"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过显式安全信号深化大模型安全对齐以抵御对抗攻击
tldr: 本文揭示大模型安全对齐存在的表面性问题，指出安全信号被其他目标稀释导致脆弱。提出引入显式安全信号，使模型在推理时能明确感知并拒绝有害请求。实验表明该方法显著增强了对抗攻击下的鲁棒性，实现了更深层的安全对齐。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有LLM安全对齐仅表面有效，无法真正抵御对抗攻击，亟需可操作的改进方案。
method: 设计显式安全信号融入对齐过程，强化模型对安全决策的明确感知。
result: 模型在对抗攻击下拒绝率大幅提升，安全对齐深度显著增强。
conclusion: 显式安全信号是消除表面化对齐、实现鲁棒防御的有效途径。
---

## Abstract
Recent studies on the safety alignment of large language models (LLMs) have revealed that existing approaches often operate superficially, leaving models vulnerable to various adversarial attacks. Despite their significance, these studies generally fail to offer actionable solutions beyond data augmentation for achieving more robust safety mechanisms. This paper identifies a fundamental cause of this superficiality: existing alignment approaches often presume that models can implicitly learn a safety-related reasoning task during the alignment process, enabling them to refuse harmful requests. However, the learned safety signals are often diluted by other competing objectives, leading models to struggle with drawing a firm safety-conscious decision boundary when confronted with adversarial attacks. Based on this observation, by explicitly introducing a safety-related binary classification task and integrating its signals with our attention and decoding strategies, we eliminate this ambiguity and allow models to respond more responsibly to malicious queries. We emphasize that, with less than 0.2x overhead cost, our approach enables LLMs to assess the safety of both the query and the previously generated tokens at each necessary generating step. Extensive experiments demonstrate that our method significantly improves the resilience of LLMs against various adversarial attacks, offering a promising pathway toward more robust generative AI systems.

---

## 论文详细总结（自动生成）

# 论文总结：加入显式安全信号可使安全对齐不再表面化

## 1. 研究动机与核心问题
- **背景**：大语言模型（LLM）的安全对齐旨在使模型拒绝有害请求，但近期研究表明，现有对齐方法往往停留于表面，模型在面对对抗攻击时依然脆弱。
- **核心问题**：现有安全对齐的根本缺陷在于**安全信号的稀释**。对齐过程隐含地期望模型学会安全推理，但这一安全目标常被其他优化目标（如流畅性、有用性）所冲淡，导致模型无法在对抗环境下形成明确的安全决策边界。
- **含义**：安全对齐的“表面化”并非不可解决，通过向模型注入**显式安全信号**，可以根本性地增强模型对恶意查询的辨识与拒绝能力。

## 2. 方法论
### 核心思想
- 将安全对齐从一个隐式推理任务**重构为显式安全二元分类任务**，使模型在每一步生成时都能明确评估当前查询与已生成内容的安全性。
- 将分类信号融入注意力机制与解码策略，消除安全性判断的模糊性。

### 关键技术细节（基于摘要推断）
1. **显式安全分类任务**：在模型内部（或外部附加）引入一个二元分类器，专门判断输入和已生成 tokens 的有害性。
2. **信号集成**：分类器产生安全信号，与模型的注意力分布和解码过程结合，影响后续 token 的选择（如压制不安全 token 的生成）。
3. **多步感知**：模型在**每个必要的生成步**上都重新评估安全性，而非仅在起始阶段进行一次判断，以应对动态变化的风险。
4. **开销控制**：该方法额外开销不到原推理成本的 **0.2 倍**，具有实用性。

## 3. 实验设计（依据摘要及元数据信息）
- **攻击场景**：覆盖多种对抗攻击方法，具体名称未在摘要中列出，但涵盖使现有对齐失效的各类白盒/黑盒攻击。
- **对比基线**：除原始对齐模型外，应与单纯的数据增强等方案进行对比。
- **评测指标**：重点关注**有害请求拒绝率**等安全指标，展示模型鲁棒性的提升。
- **数据集**：论文很可能采用标准安全评测基准（如 AdvBench、HarmBench 等），但摘要未明确列出。

## 4. 资源与算力
- **文中未明确说明** GPU 型号、数量或训练时长。仅提及额外推理开销 < 0.2x，表明方法对推理资源要求较低，具备实际部署的潜力。

## 5. 实验数量与充分性
- 文中提到进行了 **“广泛实验”** ，表明实验覆盖多种攻击类型与设置。
- 摘要未给出具体实验组数，但预计包含：
  - 多攻击方法的主实验；
  - 消融实验（验证显式信号、多步感知等设计的单独贡献）；
  - 开销分析实验。
- 整体来看，实验设计针对核心主张进行了验证，但限于摘要信息，无法评估具体对照公平性和统计显著性。

## 6. 主要结论与发现
- **显式安全信号**能有效消除对齐的表面化问题，使模型在面对对抗攻击时形成更稳固的安全决策。
- 方法显著提升了模型对各类对抗攻击的**拒绝率与鲁棒性**。
- 极低的额外推理开销（<0.2x）使得该防御机制具备在生成式 AI 系统中落地的可行性。

## 7. 方法亮点
- **直击本质**：将安全问题从隐式学习转为显式任务，解决了安全信号容易“被淹没”的核心矛盾。
- **动态、细粒度防御**：每个生成步都进行安全评估，能应对上下文演变的攻击，而非只在开头做一次性判断。
- **高效率**：几乎不影响推理速度，对实时应用友好。
- **验证全面**：在多种对抗攻击下展示一致性提升，证明方法的普适性。

## 8. 不足与局限
- **技术细节不透明**（基于现有摘要）：未揭示分类器结构、信号集成方式的具体实现，复现难度较高。
- **对新颖攻击的适应性未知**：实验虽覆盖广泛，但对抗攻击是持续演进的，方法能否迁移到未知攻击类型仍需检验。
- **潜在误拒风险**：提高安全性的同时可能增加对合法但敏感查询的拒绝率（过拒），摘要未讨论此权衡。
- **依赖额外标注**：显式分类任务可能需要额外的有害/安全标注数据进行训练，在领域迁移时可能面临数据瓶颈。

---
（完）
