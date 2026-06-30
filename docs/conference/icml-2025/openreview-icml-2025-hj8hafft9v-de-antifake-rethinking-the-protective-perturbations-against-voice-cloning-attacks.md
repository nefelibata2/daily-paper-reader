---
title: "De-AntiFake: Rethinking the Protective Perturbations Against Voice Cloning Attacks"
title_zh: "De-AntiFake: 重新思考针对语音克隆攻击的保护性扰动"
authors: "Wei Fan, Kejiang Chen, Chang Liu, Weiming Zhang, Nenghai Yu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Hj8hAfft9V"
tags: ["query:priv-sec"]
score: 8.0
evidence: 评估对抗性扰动防御生成语音模型的语音克隆攻击。
tldr: 本文首次在包含扰动净化的现实威胁模型下系统评估了语音克隆保护性扰动。研究发现尽管净化方法能中和大部分扰动，但仍会导致语音克隆模型特征空间失真，从而降低克隆性能。该工作揭示了保护措施的实际效能与局限。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 语音生成模型的进步带来了严重的隐私安全问题，现有研究通过对抗性扰动阻止未授权语音克隆，但攻击者可能采用净化手段绕过防护。
method: 在包含扰动净化的现实威胁模型下，首次系统地评估多种保护性扰动的有效性和鲁棒性。
result: 净化能削减大部分扰动，但仍会扭曲语音克隆模型的特征空间，导致克隆质量显著下降。
conclusion: 揭示了保护性扰动在现实攻击下的脆弱性，同时证明了即使不完美，扰动仍能造成潜层特征失真，为后续防御设计提供参考。
---

## Abstract
The rapid advancement of speech generation models has heightened privacy and security concerns related to voice cloning (VC). Recent studies have investigated disrupting unauthorized voice cloning by introducing adversarial perturbations. However, determined attackers can mitigate these protective perturbations and successfully execute VC. In this study, we conduct the first systematic evaluation of these protective perturbations against VC under realistic threat models that include perturbation purification. Our findings reveal that while existing purification methods can neutralize a considerable portion of the protective perturbations, they still lead to distortions in the feature space of VC models, which degrades the performance of VC. From this perspective, we propose a novel two-stage purification method: (1) Purify the perturbed speech; (2) Refine it using phoneme guidance to align it with the clean speech distribution. Experimental results demonstrate that our method outperforms state-of-the-art purification methods in disrupting VC defenses. Our study reveals the limitations of adversarial perturbation-based VC defenses and underscores the urgent need for more robust solutions to mitigate the security and privacy risks posed by VC. The code and audio samples are available at https://de-antifake.github.io.

---

## 论文详细总结（自动生成）

# De-AntiFake: 重新思考针对语音克隆攻击的保护性扰动 — 论文总结

## 1. 研究动机与核心问题
- **背景**: 语音生成模型的快速发展使语音克隆（Voice Cloning, VC）变得高度逼真，由此引发了严重的隐私和安全威胁。未经授权的语音克隆可能被用于欺诈、冒充等恶意场景。
- **现有防御**: 研究人员提出在待保护的语音中注入对抗性扰动（保护性扰动），以破坏 VC 模型的输入，使其无法生成高质量的克隆语音。
- **核心问题**: 现有防御通常假设攻击者不会对受保护的语音进行任何清洗，然而在现实场景中，攻击者完全可以采用扰动净化技术来恢复语音质量并绕过防护。本文首次在包含扰动净化的现实威胁模型下，系统评估对抗性语音扰动的实际防守效能，并重新思考这类防御的可靠性。

## 2. 方法论
论文从攻击者视角出发，设计了旨在破除保护性扰动的净化方法：
- **两阶段净化框架**:
    1. **扰动净化（Purification）**: 采用某种净化器（如基于扩散模型或信号处理方法）去除添加到语音上的显式对抗性扰动，恢复大致干净的语音信号。
    2. **音素引导细化（Phoneme-guided Refinement）**: 利用语音的音素信息作为条件，进一步调整净化后的语音，使其在分布上更接近原始干净语音，从而减轻 VC 模型特征空间的失真。

- **核心思想**: 即使第一阶段无法完全消除扰动，第二阶段通过音素引导，能将净化语音“拉回”干净语音的分布区域，降低保护性扰动对 VC 模型内部表征的扭曲，从而恢复克隆质量。

- **算法要点（文字描述）**:
    - 输入：受对抗性扰动保护的语音 \( x_{adv} \)。
    - 阶段1：使用净化模型 \( \mathcal{P} \) 得到中间结果 \( \hat{x} = \mathcal{P}(x_{adv}) \)。
    - 阶段2：以音素序列为条件，通过细化模型 \( \mathcal{R} \) 生成最终语音 \( x_{ref} = \mathcal{R}(\hat{x}, \text{phonemes}) \)，使 \( x_{ref} \) 与干净语音分布对齐。

## 3. 实验设计
- **数据集/场景**（摘要及公开信息推测）:
    - 论文提及提供了代码和音频样本于项目主页 `https://de-antifake.github.io`，但摘要未明确列出所用语音数据集名称。通常此类研究会使用 LibriTTS、VCTK 或 AISHELL 等多说话人数据集。
    - 评估场景：以多种主流语音克隆模型作为被攻击对象，模拟攻击者先对受保护语音进行净化，再执行 VC 的全流程。

- **基准对比方法**:
    - 对比了当前最优的扰动净化方法（state-of-the-art purification methods），具体名称在摘要中未列出，可能是基于扩散的净化、WaveUNet 等语音增强方法。

- **评估指标**:
    - 克隆语音的质量指标（如 MOS、PESQ、STOI、说话人相似度等），以及扰动在特征层面对 VC 模型的影响程度。

## 4. 资源与算力
- 论文摘要及提供的元数据中**未明确说明**使用的 GPU 型号、数量、训练或推理所需的计算时长。研究主页可能提供补充细节，但基于给定文本无法总结。

## 5. 实验数量与充分性
- **实验量推测**: 摘要描述为“首次系统评估”，暗示实验设计覆盖了多种保护性扰动类型、多种净化方法以及多种 VC 模型的组合，实验量应较为丰富。但具体消融实验、不同设置下的对比表格数量未在摘要中给出。
- **充分性与公平性**: 由于未提供详细实验章节，无法断言实验是否完全公平。但从接受论文（ICML 2025，评分 8.0）的评审倾向来看，实验设计通常被认为具有说服力和全面性。

## 6. 主要结论与发现
- **保护性扰动的脆弱性**: 在包含净化的现实威胁模型下，现有的基于对抗性扰动的语音保护方案可以被大部分中和，验证了其防御效能的局限。
- **特征空间失真的残留影响**: 即使净化能从信号层面移除大量扰动，VC 模型的特征空间仍然会遭受扭曲，导致克隆语音的质量和说话人相似度显著下降。
- **两阶段净化的优越性**: 所提出的音素引导细化方法能进一步缓解上述特征失真，取得优于现有净化方法的克隆恢复效果，从攻击者角度更彻底地瓦解防护。
- **安全启示**: 语音克隆对抗性防御亟需更鲁棒的方案，仅依赖可被净化的表层扰动不足以应对恶意攻击者。

## 7. 优点
- **视角新颖**: 首次在“净化→克隆”的现实攻击模型下重新审视扰动防御，填补了安全评估的空白。
- **方法创新**: 提出将音素引导融入净化后处理的思路，直接对齐干净语音分布，技术上具备针对性。
- **系统性强**: 同时评估多种防护和净化方法，结论具有普适参考价值。
- **开源与可复现性**: 提供代码和音频样本，有利于社区复现与跟进。

## 8. 不足与局限
- **实验细节缺失**（基于现有摘要）: 未给出具体数据集、对比方法的全称、详细超参数，难以独立判断实验的泛化性。
- **净化方法的依赖性**: 两阶段净化可能依赖于准确的音素提取器，实际部署中音素识别误差可能影响最终效果。
- **对未知扰动的鲁棒性**: 实验可能主要针对已知的扰动生成算法，面对自适应或更强的对抗性防御时，该方法是否依然有效尚需验证。
- **仅从攻击者视角出发**: 论文偏向证明现有防御不足，而未提出更鲁棒的防御方案，应用上需结合防御视角共同推进。

（完）
