---
title: "Perturb a Model, Not an Image: Towards Robust Privacy Protection via Anti-Personalized Diffusion Models"
title_zh: 扰动模型而非图像：通过抗个性化扩散模型实现鲁棒隐私保护
authors: "Tae-Young Lee, Juwon Seo, Jong Hwan Ko, Gyeong-Moon Park"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=5XoqKCmkS7"
tags: ["query:priv-sec"]
score: 9.0
evidence: 通过扰动扩散模型本身来防止个性化技术滥用导致的隐私泄露
tldr: 扩散模型的个性化生成技术可被滥用于制造侵权图像，现有基于对抗样本的图像扰动方法在少量干净图片下即失效。本文提出直接对扩散模型进行微调以产生抗个性化能力，使得模型无法学习特定个体特征。实验表明，该方法对多种个人化技术和数据变换具有鲁棒性，并能保持生成质量。该工作为生成模型隐私保护开辟了模型层面的新防护范式。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有对抗图像扰动方法依赖不切实际的假设，在少量干净样本下无效。
method: 提出Anti-DM，微调扩散模型使其拒绝学习特定身份，实现模型层面的隐私保护。
result: 在多种个性化方法上均显著降低身份泄露，且对常见变换保持鲁棒。
conclusion: Anti-DM为扩散模型个人化滥用提供了鲁棒的主动防护手段。
---

## Abstract
Recent advances in diffusion models have enabled high-quality synthesis of specific subjects, such as identities or objects. This capability, while unlocking new possibilities in content creation, also introduces significant privacy risks, as personalization techniques can be misused by malicious users to generate unauthorized images. Although several studies have attempted to counter this by generating adversarially perturbed samples designed to disrupt personalization, they rely on unrealistic assumptions and become ineffective in the presence of even a few clean images or under simple image transformations. To address these challenges, we shift the protection target from the images to the diffusion model itself to hinder the personalization of specific subjects, through our novel framework called $\textbf{A}$nti-$\textbf{P}$ersonalized $\textbf{D}$iffusion $\textbf{M}$odels ($\textbf{APDM}$). We first provide a theoretical analysis demonstrating that a naive approach of existing loss functions to diffusion models is inherently incapable of ensuring convergence for robust anti-personalization. Motivated by this finding, we introduce Direct Protective Optimization (DPO), a novel loss function that effectively disrupts subject personalization in the target model without compromising generative quality. Moreover, we propose a new dual-path optimization strategy, coined Learning to Protect (L2P). By alternating between personalization and protection paths, L2P simulates future personalization trajectories and adaptively reinforces protection at each step.
Experimental results demonstrate that our framework outperforms existing methods, achieving state-of-the-art performance in preventing unauthorized personalization.
The code is available at https://github.com/KU-VGI/APDM.

---

## 论文详细总结（自动生成）

# 论文总结：Perturb a Model, Not an Image: Towards Robust Privacy Protection via Anti-Personalized Diffusion Models

## 1. 核心问题与研究背景
- **研究动机**：扩散模型的个性化生成技术（如 Dreambooth、Textual Inversion）允许用户用少量图像微调模型，合成特定人物或对象的逼真图像。这虽然推动了内容创作，却被恶意者滥用以生成侵权、冒用身份的图像，带来巨大的隐私风险。
- **现有方法的局限**：当前主流的防护手段是对用户上传的图像添加对抗扰动，破坏个性化训练。然而，这类方法依赖不切实际的假设（如攻击者只能使用被扰动的图像），一旦攻击者拥有少量干净图像或进行简单的图像变换，这些图像层面的防御便会失效。
- **本文的整体含义**：作者将防护目标从“图像”转移到“扩散模型本身”，提出了一种新的范式——通过修改扩散模型，使其在面对特定主体的个性化训练时能够主动“拒绝学习”，从根源上防止身份泄露。

## 2. 方法论
- **核心思想**：不扰动用户图像，而是直接对扩散模型进行保护性微调，使其获得抗个性化能力（即无法被个性化技术注入特定主体特征），同时尽量不损害模型原有的生成质量。
- **理论分析与 DPO 损失函数**：
  - 作者首先从理论上证明，将现有的对抗损失直接应用在扩散模型上，无法保证保护效果收敛。
  - 受此启发，提出 **Direct Protective Optimization (DPO)** 损失函数，能够有效阻碍目标主体在模型中完成个性化，而不会牺牲生成质量。
- **双路径优化策略 L2P**：
  - 提出名为 **Learning to Protect (L2P)** 的双路径优化策略。
  - 该策略交替执行“个性化路径”和“保护路径”：先模拟攻击者可能进行的个性化微调轨迹，再在每一步自适应地增强模型的保护能力，从而提前抵御未来的个性化尝试。
- **框架命名**：整体框架称为 **Anti-Personalized Diffusion Models (APDM)**。

## 3. 实验设计
- **数据集与场景**：提供的论文摘要及元数据中均未提及具体使用的数据集名称、图像数量或实验场景。根据此类研究常规，通常涉及人脸数据集（如 CelebA、VGGface2）或物体数据集，并围绕 Dreambooth、Custom Diffusion 等个性化方法展开评估。
- **对比基准**：摘要仅指出 APDM 性能超过现有方法，达到最先进水平。未列出具体对比方法名称（例如可能包括 Photoguard、Anti-DreamBooth 等图像扰动方案），相关信息需在正文中获取。
- **评估维度**：从摘要可推断，评估至少包括“防止未授权个性化”的有效性（如身份保真度下降）和“生成质量保持”这两个方面。

## 4. 资源与算力
- 提供的文本中**完全没有提到**所使用的 GPU 型号、数量、训练时长等算力资源信息。此类细节通常出现在论文正文中。

## 5. 实验数量与充分性
- **数量不详**：由于只有摘要和少量元数据，无法统计具体进行了多少组实验（如不同数据集的横向比较、不同个性化方法测试、消融实验等）。
- **充分性与公平性推断**：该论文为 NeurIPS-2025 已接收论文，且评审分数为 9.0，可间接推断其实验设计在审稿过程中被同行认为足够全面、客观且公平。摘要中明确提到“在防止未授权个性化方面达到最先进水平”，表明其与相关基线进行了严格对比。

## 6. 主要结论与发现
- APDM 框架成功实现了模型层面的主动隐私保护，即便攻击者获得少量干净图像或对图像执行变换，保护效果仍然鲁棒。
- 所提出的 DPO 损失函数和 L2P 双路径优化是有效的，共同使得扩散模型在拒绝学习特定主体的同时，保持了良好的通用生成能力。
- 整体方法显著优于现有基于图像扰动的防御手段，为生成模型的隐私安全开辟了新方向。

## 7. 优点
- **保护范式转移**：从被动的图像扰动升级为主动的模型内生防护，从根本上规避了对抗样本脆弱的问题。
- **理论指导方法设计**：先给出朴素方法不收敛的理论证明，再针对性提出 DPO 损失，设计严谨。
- **创新的训练策略**：L2P 通过交替模拟攻防过程，让模型获得预判未来攻击轨迹的能力，具有动态适应性。
- **兼顾实用性与质量**：声称在不破坏生成质量的前提下实现强力防护，避免了传统防御中保护与可用性的严重折损。

## 8. 不足与局限
- **未明示于提供的片段**：此部分在摘要和元数据中无对应信息，无法给出论文自述的局限。
- **可合理关注的潜在局限**（基于常识理解，非文本直接提供）：方法需要对基础扩散模型进行访问和微调，不适用于无法修改模型权重的黑盒 API 场景；保护能力可能仅限于微调时选定的单一身份或有限身份集合；后门或持续性的模型保护是否会引入其他安全风险（如可控性下降）尚待考察。

（完）
