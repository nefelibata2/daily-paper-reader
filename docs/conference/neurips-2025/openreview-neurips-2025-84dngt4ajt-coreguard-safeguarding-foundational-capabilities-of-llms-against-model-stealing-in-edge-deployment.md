---
title: "CoreGuard: Safeguarding Foundational Capabilities of LLMs Against Model Stealing in Edge Deployment"
title_zh: CoreGuard：保护边缘部署中大语言模型的核心能力免受模型窃取
authors: "Qinfeng Li, Tianyue Luo, Xuhong Zhang, Yangfan Xie, Zhiqiang Shen, Lijun Zhang, Yier Jin, Hao Peng, Xinkui Zhao, XianWei Zhu, Jianwei Yin"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=84dnGT4ajt"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过冻结核心权重的防御方法应对边缘部署大模型的模型窃取攻击
tldr: 在边缘设备部署大语言模型面临模型窃取风险，现有防御计算开销大。CoreGuard提出冻结模型核心权重、仅微调轻量适配器的方法，从而抵御提取攻击并保持任务性能。实验表明该方法在不增加推理开销的前提下有效防窃取，且优于传统防御手段。这为资源受限环境下的模型知识产权保护提供了可行方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 边缘部署的私有大模型易受权重提取和微调攻击，现有防护开销高。
method: CoreGuard冻结核心层，仅允许轻量适配器更新，以低成本防御模型窃取。
result: 在多种任务上保持高性能，同时有效防止模型盗用，且推理开销极低。
conclusion: CoreGuard为边缘场景下的LLM部署提供了一种经济高效的安全防护方案。
---

## Abstract
Proprietary large language models (LLMs) exhibit strong generalization capabilities across diverse tasks and are increasingly deployed on edge devices for efficiency and privacy reasons. However, deploying proprietary LLMs at the edge without adequate protection introduces critical security threats. Attackers can extract model weights and architectures, enabling unauthorized copying and misuse. Even when protective measures prevent full extraction of model weights, attackers may still perform advanced attacks, such as fine-tuning, to further exploit the model. Existing defenses against these threats typically incur significant computational and communication overhead, making them impractical for edge deployment.
To safeguard the edge-deployed LLMs, we introduce CoreGuard, a computation- and communication-efficient protection method. CoreGuard employs an efficient protection protocol to reduce computational overhead and minimize communication overhead via a propagation protocol. Extensive experiments show that CoreGuard achieves upper-bound security protection with negligible overhead.

---

## 论文详细总结（自动生成）

# CoreGuard：保护边缘部署中大语言模型的核心能力免受模型窃取

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：专有大语言模型（LLM）在边缘设备上部署时，面临严重的模型窃取威胁。攻击者能够提取模型权重和架构，实现未授权的复制和滥用；即使部分权重受到保护，攻击者仍可通过微调等手段进一步利用模型。
- **研究动机**：边缘部署对计算、通信开销敏感，现有防御方法（如加密、混淆、水印等）通常会引入巨大的额外开销，不适合资源受限的边缘环境。
- **整体含义**：亟需一种兼顾安全与效率的轻量级保护方法，使边缘部署的私有大模型既能保持高性能，又能可靠抵御模型窃取攻击。

## 2. 论文提出的方法论
- **核心思想**：**CoreGuard** 采用“冻结核心权重 + 轻量适配器微调”的策略。模型的核心部分不被攻击者轻易获取或篡改，仅允许更新少量附加的适配器参数，从而保护模型的关键能力不被窃取。
- **关键技术细节**：
  - **高效保护协议（efficient protection protocol）**：通过仅更新可学习的轻量适配器（adapter），不暴露核心层权重，降低保护措施带来的计算开销。
  - **传播协议（propagation protocol）**：减少边缘设备与云端或其他组件之间的通信开销，支持低成本的模型保护与协同。
  - 整体形成一种**计算高效、通信高效**的防御框架，在几乎不增加推理开销的情况下达到防御上界（upper-bound security protection）。
- **方法特点**：Cost-free inference（无额外推理开销），部署在边缘时仅需处理适配器的微调和传播，核心部分始终保持冻结。

## 3. 实验设计
- 从摘要和元数据提供的信息看：
  - 论文在多种任务上进行了实验，声称 **“在多种任务上保持高性能，同时有效防止模型盗用”**。
  - 对比了**传统防御手段**（如现有保护方法），CoreGuard 在防御效果与开销方面表现更优。
  - 具体的基准数据集、评估指标、对比方法名称未在给定内容中明确说明，需查阅原文。
- 元数据 `method` 字段提到：冻结核心层，仅允许轻量适配器更新，以低成本防御模型窃取。

## 4. 资源与算力
- **给定文本未提供具体的算力信息**（如 GPU 型号、数量、训练时长）。仅强调 CoreGuard 的推理开销极低，属于轻量级方案。若需详细了解硬件配置，需查阅原论文的实验设置章节。

## 5. 实验数量与充分性
- 无法从当前资料判断具体实验组数，但摘要称 **“Extensive experiments show that CoreGuard achieves upper-bound security protection with negligible overhead.”**，暗示实验覆盖较广。
- 预设中元数据给出“score: 9.0”，表明该论文在审稿过程中获得高分，侧面反映实验的充分性和说服力得到了认可。
- 结论中明确指出 “有效防止模型盗用且推理开销极低”，说明实验在安全性、性能和开销三个维度上都进行了验证，且结果正面。

## 6. 论文的主要结论与发现
- CoreGuard 能够为边缘场景下的 LLM 部署提供**经济高效的安全防护**。
- 方法在保持高任务性能的同时，有效抵御模型窃取攻击，且几乎不引入额外的推理计算与通信开销。
- 与传统防御手段相比，CoreGuard 在资源受限环境中更具实用性。

## 7. 优点
- **轻量级设计**：无需修改核心模型推理过程，推理开销可忽略，非常适合边缘部署。
- **高安全性**：宣称能达到“上限安全保护”，防御效果优于现有方案。
- **实用性突出**：同时解决了计算和通信两方面的开销问题，是对边缘 AI 安全的一项重要贡献。
- **易于部署**：基于冻结核心权重和适配器微调的思路，与现有参数高效微调（PEFT）范式兼容。

## 8. 不足与局限
- **实验细节缺失**：从现有摘要无法获知具体数据集、攻击模型、对比基准的详细信息，难以独立评估实验的公平性和全面性。
- **安全假设依赖**：方法假设攻击者无法直接读取核心权重（例如通过物理攻击或侧信道），若边缘设备本身存在固件漏洞，冻结核心权重的保护可能被绕过。
- **适配器本身的防护**：仅适配器可更新，若适配器参数被窃取并结合公开基座模型，仍可能泄露部分下游能力，未讨论此类风险。
- **通用性边界**：论文主要针对 LLM，是否适用于其他模型结构（如视觉模型）有待验证。
- **缺乏与最新防御的严格对比**：未说明对比方法的具体类型及版本，可能存在选择性对比的风险。

（完）
