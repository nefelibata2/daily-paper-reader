---
title: "Robust Secure Swap: Responsible Face Swap With Persons of Interest Redaction and Provenance Traceability"
title_zh: 鲁棒安全换脸：面向受保护人员的红化和来源可追溯
authors: "Yunshu Dai, Jianwei Fei, Fangjun Huang, Chip Hong Chang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=gb2dwmPXhs"
tags: ["query:priv-sec"]
score: 8.0
evidence: 提出针对换脸生成模型滥用的防御方法，应对安全漏洞。
tldr: 本文针对生成式换脸技术滥用的安全威胁，提出Secure Swap方法，通过身份护照层红化受保护人员并嵌入隐形水印实现溯源，在不影响图像质量的前提下提供负责任的人脸交换。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 生成式换脸技术可能导致未经同意的面部操纵和身份欺诈。
method: 提出Secure Swap，利用身份护照层红化受保护人员并对非保护输出加水印。
result: 实验表明该方法能有效防止滥用并保证图像质量。
conclusion: 为生成模型实际部署中的安全风险提供了可追溯的防御方案。
---

## Abstract
As AI generative models evolve, face swap technology has become increasingly accessible, raising concerns over potential misuse. Celebrities may be manipulated without consent, and ordinary individuals may fall victim to identity fraud. To address these threats, we propose Secure Swap, a method that protects persons of interest (POI) from face-swapping abuse and embeds a unique, invisible watermark into nonPOI swapped images for traceability. By introducing an ID Passport layer, Secure Swap redacts POI faces and generates watermarked outputs for nonPOI. A detachable watermark encoder and decoder are trained with the model to ensure provenance tracing. 
Experimental results demonstrate that Secure Swap not only preserves face swap functionality but also effectively prevents unauthorized swaps of POI and detects different embedded model's watermarks with high accuracy. 
Specifically, our method achieves a 100% success rate in protecting POI and over 99% watermark extraction accuracy for nonPOI. Besides fidelity and effectiveness, the robustness of protected models against image-level and model-level attacks in both online and offline application scenarios is also experimentally demonstrated.

---

## 论文详细总结（自动生成）

# 论文总结：《鲁棒安全换脸：面向受保护人员的红化和来源可追溯》

## 1. 核心问题与整体含义
- **研究背景**：生成式 AI 驱动的换脸（face swap）技术越来越容易获取，带来严重的伦理和安全挑战，包括未经许可的名人肖像操纵以及针对普通人的身份欺诈。
- **核心问题**：现有换脸模型缺乏对特定受保护人员（persons of interest, POI）的滥用防御机制，同时无法对生成的伪造内容进行有效的溯源追踪。
- **整体含义**：本文旨在提出一种负责任的换脸方法，既能正常执行换脸功能，又能阻止对 POI 的非法换脸，并对非 POI 的换脸输出嵌入可溯源水印，从而平衡功能性与安全性。

## 2. 方法论
- **总览**：提出 **Secure Swap**，在换脸模型中集成“身份护照层（ID Passport layer）”以红化受保护人员，并利用可拆卸水印编码器-解码器对非受保护人员的换脸结果添加隐形水印。
- **关键组件/流程**：
  - **身份护照层**：
    - 在模型内部引入一种保护机制，当检测到源图像或目标图像中包含 POI 面部时，主动进行“红化”，即阻止 POI 面孔被用于换脸，输出可能为被遮挡、模糊化或其他形式的处理，以防止非法肖像生成。
  - **水印嵌入与提取**：
    - 对于非 POI 的换脸生成图像，使用可拆卸的水印编码器（detachable watermark encoder）在生成过程中嵌入唯一、不可见的水印标记。
    - 对应的水印解码器（detachable decoder）可在事后从图像中准确提取水印，实现模型来源追溯（确定由哪个模型生成）。
    - 编码器和解码器与主换脸模型联合训练，保证水印与其生成能力协同优化。
  - **算法特点**：
    - 身份护照层和水印嵌入均不影响换脸的自然度与图像质量。
    - 方案支持在线和离线部署场景，对图像级和模型级攻击具有鲁棒性。

## 3. 实验设计
- **数据集/场景**（据摘要推断，可能使用标准人脸数据集）：
  - 包含受保护人员（POI）和非受保护人员的面部图像，可能用到如 CelebA、FFHQ 等常见人脸数据集，并自行划分 POI 集合。
  - 评估场景涵盖在线（实时服务）和离线（预生成内容）应用。
- **基准方法对比**：
  - 摘要未列明具体对比方法，但通常对比包括：无保护的基础换脸模型、其他基于扰动或水印的防御方法、针对换脸滥用的红化/打码方法等。
  - 评估指标包括：POI 保护成功率（100%）、非 POI 水印提取准确率（>99%）、图像质量（保真度）和对抗攻击鲁棒性。
- **攻击测试**：
  - 图像级攻击：对生成图像进行后处理（如压缩、噪声、裁剪等）下验证水印持久性。
  - 模型级攻击：尝试通过微调、剪枝、知识蒸馏等方式破坏水印或绕过护照防护，验证模型鲁棒性。

## 4. 资源与算力
- 基于现有文本，**未明确提供** GPU 型号、数量、训练时长等算力信息。摘要和元数据中均未涉及该部分。

## 5. 实验数量与充分性
- **实验组别**（从摘要和问题描述可推测）：
  - POI 保护有效性测试（多身份、多场景）。
  - 非 POI 水印编码-解码准确率测试（跨不同模型版本或不同图像）。
  - 图像级鲁棒性测试（多种常见图像处理操作）。
  - 模型级鲁棒性测试（针对模型修改或攻击）。
  - 与基线方法的图像质量对比（结构相似性、身份保护程度等）。
- **充分性与客观性评价**：
  - 报告了 100% 的 POI 保护成功率和 99% 以上的水印提取精度，指标理想。
  - 覆盖了常见的攻击维度和部署场景，具备一定的全面性。
  - 但未展示实际对比方法的具体名称，无法判断对比基线是否足够丰富；实验多维度但数量无法准确量化，需进一步查阅正文以确认消融实验和统计检验。

## 6. 主要结论与发现
- **有效防护**：Secure Swap 可以完全阻止对指定 POI 的换脸滥用，同时维持对非 POI 的高质量换脸。
- **高精度溯源**：嵌入的隐形水印可以在各种攻击后仍以 >99% 的准确率被提取，保证了生成内容的可追溯性。
- **鲁棒性强**：在图像后处理和模型修改攻击下，护照保护和水印均表现稳健，证明方法在真实在线和离线环境中具备实用性。
- **质量无损**：保护措施未明显损害最终图像的视觉逼真度和换脸效果。

## 7. 优点与亮点
- **创新性架构**：将“身份红化”与“可追溯水印”两种防御机制统一在单一生成管道中，实现负责任的换脸。
- **可拆卸水印设计**：编码器-解码器可灵活组合，不破坏主模型性能，便于实际部署。
- **双重防护**：既防止敏感身份被利用，又实现对滥用输出的责任追踪，从源头和事后两个维度解决安全问题。
- **实用性验证**：考虑了在线/离线场景及多类型攻击，证明方法并非纸上谈兵，有较强落地潜力。
- **性能卓越**：近乎完美的保护率和水印准确率，且声称不影响图像质量，体现了较好的技术平衡。

## 8. 不足与局限
- **信息不完整**：仅基于摘要分析，缺少细节如：POI 的保护究竟采用何种具体红化方式（模糊、遮挡、替换等），是否可能被高级逆向工程破解；水印容量、对多代伪造的抵抗能力等未提及。
- **实验对比不明确**：未列出对比的防御方法，无法判断相较现有方案的优势幅度；可能遗漏了与近期面部伪造防御（如 FaceSafe、RFW、SWE 等）的横向比较。
- **用户可接受度**：红化操作可能在某些场景下影响用户体验或引发误伤（如误将普通用户识别为 POI），但未讨论误检率和实用性折衷。
- **鲁棒性边界**：摘要虽提到图像级和模型级攻击测试，但未见更高级别的自适应攻击（如对手已知护照层设计），安全的上界未知。
- **部署成本**：未提及身份护照层的判断依赖何种身份识别模块、是否需要持续更新 POI 列表，以及训练/推理的额外开销。

---

（完）
